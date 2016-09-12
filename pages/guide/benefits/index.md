---
title: Benefits
---

PostGraphQL uses the joint benefits of PostgreSQL and GraphQL to provide a number of key benefits.

### Automatic Relation Detection
Does your table’s `authorId` column reference another table? PostGraphQL knows and will give you a field for easily querying that reference.

A schema like:

```sql
create table post (
  id serial primary key,
  author_id int non null references user(id),
  headline text,
  body text,
  …
);
```

Can query relations like so:

```graphql
{
  postNodes {
    nodes {
      headline
      body
      author: userByAuthorId {
        name
      }
    }
  }
}
```

### Custom Mutations and Computed Columns
Procedures in PostgreSQL are powerful for writing business logic in your database schema, and PostGraphQL allows you to access those procedures through a GraphQL interface. Create a custom mutation, write an advanced SQL query, or even extend your tables with computed columns! Procedures allow you to write logic for your app in SQL instead of in the client all while being accessible through the GraphQL interface.

So a search query could be written like this:

```sql
create function search_posts(search text) returns setof post as $$
  select *
  from post
  where
    headline ilike ('%' || search || '%') or
    body ilike ('%' || search || '%')
$$ language sql stable;
```

And queried through GraphQL like this:

```graphql
{
  searchPosts(search: "Hello world", first: 5) {
    pageInfo {
      hasNextPage
    }
    totalCount
    nodes {
      headline
      body
    }
  }
}
```

For more information, check out our [procedure documentation][] and our [advanced queries documentation][].

[procedure documentation]: ../procedures/
[advanced queries documentation]: ../advanced-queries/

### Fully Documented APIs
Introspection of a GraphQL schema is powerful for developer tooling and one element of introspection is that every type in GraphQL has an associated `description` field. As PostgreSQL allows you to document your database objects, naturally PostGraphQL exposes these documentation comments through GraphQL.

Documenting PostgreSQL objects with the [`COMMENT`][sql-comment] command like so:

```sql
create table user (
  username text non null unique,
  …
);

comment on table user is 'A human user of the forum.';
comment on column user.username is 'A unique name selected by the user to represent them on our site.';
```

Will let you reflect on the schema and get the JSON below:

```graphql
{
  __type(name: "User") { … }
}
```

```json
{
  "__type": {
    "name": "User",
    "description": "A human user of the forum.",
    "fields": {
      "username": {
        "name": "username",
        "description": "A unique name selected by the user to represent them on our site."
      }
    }
  }
}
```

[sql-comment]: http://www.postgresql.org/docs/current/static/sql-comment.html

### UI For Development Comes Standard
[GraphiQL][graphiql] is a great tool by Facebook to let you interactively explore your data. When development mode is enabled in PostGraphQL, the GraphiQL interface will be *automatically* displayed at your GraphQL endpoint.

Just navigate with your browser to the URL printed to your console after starting PostGraphQL and use GraphiQL with your data! Even if you don’t want to use GraphQL in your app, this is a great interface for working with any PostgreSQL database.

Just remember to use the `--development` flag when starting PostGraphQL!

[graphiql]: https://github.com/graphql/graphiql

### Token Based Authorization
PostGraphQL let’s you use token based authentication with [JSON Web Tokens][jwt] (JWT) to secure your API. It doesn’t make sense to redefine your authentication in the API layer, instead just put your authorization logic in the database schema! With an advanced [grants][grants] system and [row level security][row-level-security], authorization in PostgreSQL is more than enough for your needs.

PostGraphQL follows the [PostgreSQL JSON Web Token Serialization Specification][pg-jwt-spec] for serializing JWTs to the database for your use in authorization. The `role` claim of your JWT will become your PostgreSQL role and all other claims can be found under the `jwt.claims` namespace (see [retrieving claims in PostgreSQL][retrieving-claims]).

To enable token based authorization use the `--secret <string>` command line argument with a secure string PostGraphQL will use to sign and verify tokens. And if you don’t want authorization, just don’t set the `--secret` argument and PostGraphQL will ignore all authorization information!

[jwt]: https://jwt.io
[grants]: http://www.postgresql.org/docs/current/static/sql-grant.html
[row-level-security]: http://www.postgresql.org/docs/current/static/ddl-rowsecurity.html
[pg-jwt-spec]: https://github.com/calebmer/postgraphql/blob/master/docs/pg-jwt-spec.md
[retrieving-claims]: https://github.com/calebmer/postgraphql/blob/master/docs/pg-jwt-spec.md#retrieving-claims-in-postgresql

### Cursor Based Pagination For Free
There are some problems with traditional limit/offset pagination and realtime data. For more information on such problems, read [this article][pagination-for-graphql].

PostGraphQL not only provides limit/offset pagination, but it also provides cursor based pagination ordering on the column of your choice. Never again skip an item with free cursor based pagination!

[pagination-for-graphql]: https://medium.com/apollo-stack/understanding-pagination-rest-graphql-and-relay-b10f835549e7#.8ehp4qwsq

### Relay Specification Compliant
You don’t have to use GraphQL with React and Relay, but if you are, PostGraphQL implements the brilliant Relay specifications for GraphQL. Even if you are not using Relay your project will benefit from having these strong, well thought out specifications implemented by PostGraphQL.

The specific specs PostGraphQL implements are:

- [Global Object Identification Specification.](http://facebook.github.io/relay/graphql/objectidentification.htm)
- [Cursor Connections Specification.](http://facebook.github.io/relay/graphql/connections.htm)
- [Input Object Mutations Specification.](http://facebook.github.io/relay/graphql/mutations.htm)
