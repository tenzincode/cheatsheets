# GraphQL

A shorthand notation to succinctly express the basic shape of your GraphQL schema and its type system.

Example of a typical GraphQL schema expressed in shorthand.

```graphql
interface Entity {
  id: ID!
  name: String
}
type User implements Entity {
  id: ID!
  name: String
  age: Int
  balance: Float
  is_active: Boolean
  friends: [User]!
}
type Root {
   me: User
   users(limit: Int = 10): [User]!
   friends(forUser: ID!, limit: Int = 5): [User]!
}
schema {
  query: Root
  mutation: ...
  subscription: ...
}
```

```
Basics
Schema
=======
GraphQL Schema => schema
Built-in scalar types
=====================
GraphQL Int     => Int
GraphQL Float   => Float
GraphQL String  => String
GraphQL Boolean => Boolean
GraphQL ID      => ID
Type Definitions
================
Scalar Type        => scalar
Object Type        => type
Interface Type     => interface
Union Type         => union
Enum Type          => enum
Input Object Type  => input
Type Markers
============
Non-null Type                    => <type>!     e.g String!
List Type                        => [<type>]    e.g [String]
List of Non-null Types           => [<type>!]   e.g [String!]
Non-null List Type               => [<type>]!   e.g [String]!
Non-null List of Non-null Types  => [<type>!]!  e.g [String!]!
```

Examples
Below are further examples to illustrate how we can use the above Shorthand Notation to describe our schema.

```graphql
Input Arguments
Basic Input
============
type Root {
  users(limit: Int): [User]!
}
Input with default value
=========================
type Root {
  users(limit: Int = 10): [User]!
}
Input with multiple args
=========================
type Root {
  users(limit: Int, sort: String): [User]!
}
Input with multiple args and default values
===========================================
type Root {
  users(limit: Int = 10, sort: String): [User]!
}
or
type Root {
  users(limit: Int, sort: String = "asc" ): [User]!
}
or
type Root {
  users(limit: Int = 10, sort: String = "asc" ): [User]!
}
```

Interfaces

Object implementing an Interface

```graphql
interface Foo {
  is_foo: Boolean
}
type Bar implements Foo {
  is_foo: Boolean
  is_bar: Boolean
}
```

Object implementing multiple Interfaces

```graphql
interface Foo {
  is_foo: Boolean
}
interface Goo {
  is_goo: Boolean
}
type Bar implements Foo, Goo {
  is_bar: Boolean
  is_foo: Boolean
  is_goo: Boolean
}
```

Unions

Union of a single Object

```graphql
type Foo {
  name: String
}
union SingleUnion = Foo
type Root {
  single: SingleUnion
}
```

Union of multiple Objects

```graphql
type Foo {
  name: String
}
type Bar {
  is_bar: String
}
union MultipleUnion = Foo | Bar
type Root {
  multiple: MultipleUnion
}
```

Enums

```graphql
enum RGB {
  RED
  GREEN
  BLUE
}
type Root {
  color: RGB
}
```

Input Object Types

```graphql
input ListUsersInput {
  limit: Int
  since_id: ID
}
type Root {
  users(params: ListUsersInput): [Users]!
}
```

Custom Scalar

```graphql
scalar Url
type User {
  name: String
  homepage: Url
}
