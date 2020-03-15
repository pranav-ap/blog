---
title: "GraphQL"
date: "2020-3-15"
template: "post"
draft: true
slug: "/posts/graphql/"
category: "Web Technologies"
tags:
   - ""
description: ""
---

**GraphQL** is flexible API standard for modern applications. It defines a *query language* and the behavior of a *server-side runtime* for executing these queries.

The query language lets you make precise data requests and the GraphQL server returns exactly what you ask for; nothing more, nothing less.

GraphQL can be used as an API layer over existing servers, databases and third party APIs. This enables developers to group multiple data sources together and provide a unified interface to client applications.

Popular client implementations include Apollo Client and Relay. Popular server implementations include Apollo Server and GraphQL Yoga.

# GraphQL Server

A GraphQL server receives, validates and executes queries from clients. But before a GraphQL server can talk to clients, we need to define a schema.

## Schema Definition

A GraphQL schema is at the center of any GraphQL server implementation and describes the functionality available to the clients which connect to it. The schema describes the API of the server.

A **GraphQL schema** defines two things:

1. A complete description of the available data
1. A description of the operations : reading, writing and subscribing to data changes

Schemas are written using the **Schema Definition Language (SDL)**. The schema for a blogging site could be written as follows:

```graphql
type Post {
  id: ID!
  title: String!
  author: Author!
  comments: [Comment]!
}

type Author {
  id: ID!
  name: String!
}

type Comment {
  id: ID!
  post: ID!
  text: String!
}
```

The core building block within a schema is the **type**. Types provide a wide-range of functionality within a schema, including the ability to:

1. Define data structures and the relationships between them
1. Define which data fetching and manipulation operations can be executed by the client

In the above example, `Post` is a type and `title: String!` is a field.

A type that contains one or more fields is called an **ObjectType**. On the other hand `title` is a **ScalarType** String.

GraphQL comes with a set of scalar types out of the box:

- Int
- Float
- String
- Boolean
- ID

All object types are user-defined, and if necessary there are ways to introduce new scalar types.

Note that these declarations express the relationships and the shape of the data, not where the data comes from or how it might be stored.

### Type Modifiers

- **Non-nullable fields** are denoted by an exclamation mark:

```graphql
name: String!
```

The name field needs to have a value.

- **Lists** are denoted by square brackets:

```graphql
comments: [Comment]!
```

`[Comment]!` indicates that if there are not comments, we must place an empty array as the value, and not *null*.

`[Comment!]!` indicates that none of the items within this array can be *null*.

- An **enum** is a scalar value that has a specified set of possible values.

```graphql
enum Sport {
  FOOTBALL
  CRICKET
  BASKETBALL
}
```

- An **interface** defines a set of fields that a type which implements this interface must include.

```graphql
interface Item {
  name: String!
}

type Shoe implements Item {
  name: String!
  owner: String!
}
```

In the above example, the `Shoe` type implements the `Item` interface.

## Exposing Operations

The schema is not yet complete. It doesn’t expose any functionality to client applications. It simply defines the shape of your data.

In order to add functionality to the API, you need to add three types to the root of the GraphQL schema: *Query*, *Mutation* and *Subscription*.

```graphql
schema {
  query: Query
  mutation: Mutation
  subscription: Subscription
}
```

These are the entry points for reading, editing and subscription operations. Of the three, mutation and subscriptions are optional.

### Query Type

A GraphQL query is used for fetching data. It is similar to the **GET** request in REST APIs.

```graphql
type Query {
  author(id: ID!): Author!
  posts: [Post]!
}
```

This Query type allows the clients to query the author's profile and all their posts.

### Mutation Type

Mutations are operations sent to the server to create, update or delete data. These are comparable to **POST**, **PATCH** and **DELETE** in REST APIs.

```graphql
type Mutation {
  publishPost(post: Post) : Post
}
```

This Mutation type allows clients to add a new post. Once added, it returns a response of type *Post* back to the client.

GraphQL mutations can return any information the developer wishes, but designing mutation responses in a consistent and robust structure makes them more approachable.

- When fields from one or more types are modified, the client can benefit from having updated fields returned from each type.
- If only a portion of a mutation update succeeds, it's important to convey that information to the client to avoid stale local state.

To provide consistent mutation response, we can base all mutations on the following interface.

```graphql
interface MutationResponse {
  code: String!
  success: Boolean!
  message: String!
}
```

The new response type for our *publish post* mutation can be:

```graphql
type PublishPostMutationResponse implements MutationResponse {
  code: String!
  success: Boolean!
  message: String!
  post: Post
}
```

The above Mutation type should be changed to:

```graphql
type Mutation {
  publishPost(post: Post) : PublishPostMutationResponse
}
```

Note that a client may send multiple mutation commands at the same time. But the server will execute them in series, in order to avoid race-conditions.

### Subscription Type

Subscriptions allow a server to send data to its clients when a specific event happens. The client initiates a long-lived connection to the server by sending a subscription request that specifies which event it is interested in.

The server maintains connections with each of its subscribed clients. Every time this event occurs, the server pushes the relevant data to the subscribed clients.

```graphql
type Subscription {
  newPost: Post!
}
```

The above Subscription type allows a client to receive notifications whenever a new post is published.
<!-- How ?? -->

## Resolver Functions : Implementing the API

We now have a complete description of the API. But how do we implement this API? To do this, we need to write functions, called *resolvers*, for each and every field in the schema.

The purpose of a **resolver** is to fetch from or manipulate the value of its associated field at its source. If a resolver's associated field is an ObjectType with fields whose data is stored across different databases, then the resolver needs to connect to each of these sources, to fetch or manipulate it.

```js
function (parent, args, context, info) {
  ...
}
```

A resolver function accepts four arguments:

- **parent** - result of the parent resolver's call.
- **args** - parameters of the query, mutation or subscription request.
- **context** - an object that stores connection objects to various backends.
- **info** - an AST representation of the query or mutation.

Consider the following query type:

```graphql
type Query {
  user: User!
}

type User {
  id: ID!
  name: String!
}
```

The user field of `type Query` has a resolver function **A**. Type User has fields id and name. They have resolver functions of their own **B** and **C**.

Since the schema is hierarchial, the resolvers also have a hierarchial relationship. Thus, Resolver **A** is the parent of resolvers **B** and **C**.

If you query for `name`, a chain of function calls are made in the server. Resolver **A** is called first, then Resolver **B** is called.

Now, imagine the server gets a query for a user:

```graphql
query {
  user(id : "123") {
    id,
    name
  }
}
```

This query asks for the user with `id: 123`. The response must contain the id and the username.

The execution of the query is as follows:

1. The query arrives at the server.
1. Resolver **A** is called with `{ id : "123" }` as input argument `args`. It talks to the relevant database(s) and gets a response, `{ id: 123, name: 'James' }`.
1. Now the resolvers of each of its queried fields are called.
1. Resolver **B** is called with `{ id: 123, name: 'James' }` as input argument `parent`. It returns `root.id`.
1. Resolver **C** is called with `{ id: 123, name: 'James' }` as input argument `parent`. It returns `root.name`.
1. The execution is over and the overall result is:

```json
{
  "data": {
    "user": {
      "id": "123",
      "name": "James"
    }
  }
}
```

<figure style="width: 1000px">
	<img src="/media/web tech/resolve.png" alt="Resolve">
	<figcaption>Resolve</figcaption>
</figure>

Note that depending on the GraphQL library you are using, you may not need to write trivial functions like **B** and **C**. The library can resolve it based on the field's name.

# The Query Language

A GraphQL client helps you connect to the GraphQL server. It sends the query to the server, along with any variables required.

Client implementations like the Apollo Client provide a complete solution for local state management. Apollo Client takes care of the request cycle from start to finish, including tracking loading and error states for you.

## Query

```graphql
query GetAuthorProfile {
  author(id : "123") {
    id,
    name
  }
}
```

This query is used to get `{ id, name }` of an author with `id: 123`. Optionally, we can give this query a name, *GetAuthorProfile*.

The response from the server will follow the same structure as the query.

```json
{
  "data": {
    "user": {
      "id": "123",
      "name": "James"
    }
  }
}
```

## Mutation

```graphql
mutation AddNewBook($title: String, $author: String = "Anonymous") {
  addBook(title: $title, author: $author) {
    title
  }
}
```

This mutation adds a new book. The title and author are specified as variables `$title` and `$author`. `$author` has the default value "Anonymous".

The GraphQL client sends the variables to the server along with the mutation request, in JSON format:

```json
{
  "variables": {
    "title": "Game of Thrones",
    "author": "GRRM"
  }
}
```

The response from the server is:

```json
{
  "data": {
    "addBook": {
      "title": "Game of Thrones"
    }
  }
}
```

### Input object type

In the above example, we passed two scalar strings as input arguments. For sending more complex input arguments, we can use a special kind of object type that can be passed in as an argument.

```graphql
input NewBookInput {
  title: String!
  author: String!
}
```

The mutation can be re-written as:

```graphql
mutation AddNewBook($book: NewBookInput!) {
  addBook(book: $book) {
    title
  }
}
```

The variables JSON looks like:

```json
{
  "variables": {
    "book": {
      "title": "Game of Thrones",
      "author": "GRRM"
    }
  }
}
```

### Multiple mutations

You can even send multiple mutations in a single query. But, as previously discussed, the server will not process them simultaneously. It will validate and execute them in series, in order to avoid race-conditions.

```graphql
mutation AddNewBook($book_1: NewBookInput!, $book_2: NewBookInput!) {
  addBook(book: $book_1) {
    title
  }

  addBook(book: $book_2) {
    title
  }
}
```

## Subscription

```graphql
subscription onNewComment($post: String!){
  commentAdded(post: $post){
    id
    text
  }
}
```

The above subscription requests the server to notify the client whenever a new comment is added to a `$post`. The notification includes the `id` and `text` of the new comment.

```json
{
  "data": {
    "commentAdded": {
      "id": "41",
      "text": "Great Post!"
    }
  }
}
```

# References

- [Introduction to GraphQL](https://graphql.org/learn/)
- [How to GraphQL](https://www.howtographql.com/basics/0-introduction/)
- [GraphQL Wikipedia](https://en.wikipedia.org/wiki/GraphQL)
- [Apollo GraphQL](https://www.apollographql.com/docs/tutorial/introduction/)
- [GraphQL SDL — Schema Definition Language](https://www.prisma.io/blog/graphql-sdl-schema-definition-language-6755bcb9ce51)
- [GraphQL Server Basics: GraphQL Schemas, TypeDefs & Resolvers Explained](https://www.prisma.io/blog/graphql-server-basics-the-schema-ac5e2950214e)
- [Principled GraphQL](https://principledgraphql.com/)
- [GraphQL specification](https://spec.graphql.org/)