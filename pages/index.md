---
title: A GraphQL API created by reflection over a PostgreSQL schema.
---

[![Package on npm](https://img.shields.io/npm/v/postgraphql.svg?style=flat)](https://www.npmjs.com/package/postgraphql)
[![Gitter chat room](https://badges.gitter.im/calebmer/postgraphql.svg)](https://gitter.im/calebmer/postgraphql?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

The strongly typed GraphQL data querying language is a revolutionary new way to interact with your server. Similar to how JSON very quickly overtook XML, GraphQL will likely take over REST. Why? Because GraphQL allows us to express our data in the exact same way we think about it.

The PostgreSQL database is the self acclaimed “world’s most advanced open source database” and even after 20 years that still rings true. PostgreSQL is the most feature rich SQL database available and provides an excellent public reflection API giving its users a lot of power over their data. And despite being 20 years old, the database still has frequent releases.

With PostGraphQL, you can access the power of PostgreSQL through a well designed GraphQL server. PostGraphQL uses PostgreSQL reflection APIs to automatically detect primary keys, relationships, types, comments, and more providing a GraphQL server that is highly intelligent about your data.

PostGraphQL holds a fundamental belief that a *well designed database schema should be all you need to serve well thought out APIs*. PostgreSQL already has amazing user management and relationship infrastructure, *why duplicate that logic* in a custom API? PostGraphQL is likely to provide a more performant and standards compliant GraphQL API then any created in house. Focus on your product and let PostGraphQL manage how the data gets to the product.

For a critical evaluation of PostGraphQL to determine if it fits in your tech stack, read the [evaluating PostGraphQL for your project](./guide/evaluating/) section.

## Roadmap
In the future, things PostGraphQL will be able to do will include:

- Authentication using PostgreSQL roles.
- Whitelisted queries in production.
- Subscriptions using the PostgreSQL [`NOTIFY`][pg-notify] feature.

[pg-notify]: http://www.postgresql.org/docs/current/static/sql-notify.html
