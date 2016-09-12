---
title: Evaluating PostGraphQL For Your Project
---

Hopefully you’ve been convinced that PostGraphQL serves an awesome GraphQL API, but now let’s take a more critical look at whether or not you should adopt PostGraphQL for your project.

PostGraphQL’s audience is for people who’s core business is not the API and want to prioritize their product. PostGraphQL allows you to define your content model in the database as you normally would, however instead of building the bindings to the database (your API) PostGraphQL takes care of it.

This takes a huge maintenance burden of your shoulders. Now you don’t have to worry about optimizing the API and the database, instead you can focus on just optimizing your database.

### No Lock In
PostGraphQL does not lock you into using PostGraphQL forever. Its purpose is to help your business in a transitory period. When you feel comfortable with the cost of building your API PostGraphQL is simple to switch with a custom solution.

How is it simple? Well first of all, your PostgreSQL schema is still your PostgreSQL schema. PostGraphQL does not ask you to do anything too divergent with your schema allowing you to take your schema (and all your data) to whatever solution you build next. GraphQL itself provides a simple and clear deprecation path if you want to start using different fields.

Ideally PostGraphQL scales with your company and we would appreciate your contributions to help it scale, however there is a simple exit path even years into the business.

### Schema Driven APIs
If you fundamentally disagree with a one-to-one mapping of a SQL schema to an API (GraphQL or otherwise) this section is for you. First of all, PostGraphQL is not necessarily meant to be a permanent solution. PostGraphQL was created to allow you to focus on your product and not the API. If you want a custom API there is a simple transition path (read [no lock in](#no-lock-in)). If you still can’t get over the one-to-one nature of PostGraphQL consider the following arguments why putting your business logic in PostgreSQL is a good idea:

1. PostgreSQL already has a powerful [user management system][user-management] with fine grained [row level security][row-level-security]. A custom API would mean you have to build your own user management and security.
2. PostgreSQL allows you to hide implementation details with [views][pg-views] of your data. Simple views can even be [auto-updatable][pg-udpatable-views]. This provides you with the same freedom and flexibility as you might want from a custom API except more performant.
3. PostgreSQL gives you automatic relations with the `REFERENCES` constraint and PostGraphQL automatically detects them. With a custom API, you’d need to hardcode these relationships.
4. For what it’s worth, you can write in your favorite scripting language in PostgreSQL including [JavaScript][js-in-pg] and [Ruby][ruby-in-pg].
5. And if you don’t want to write your Ruby in PostgreSQL, you could also use PostgreSQL’s [`NOTIFY`][pg-notify] feature to fire events to a listening Ruby or [JavaScript][node-pg-notify] microservice can listen and respond to PostgreSQL events (this could include email transactions and event reporting).

Still worried about a certain aspect of a schema driven API? Open an issue, confident we can convince you otherwise 😉

[user-management]: http://www.postgresql.org/docs/current/static/user-manag.html
[row-level-security]: http://www.postgresql.org/docs/current/static/ddl-rowsecurity.html
[pg-views]: http://www.postgresql.org/docs/current/static/sql-createview.html
[pg-udpatable-views]: http://www.postgresql.org/docs/current/static/sql-createview.html#SQL-CREATEVIEW-UPDATABLE-VIEWS
[js-in-pg]: https://blog.heroku.com/archives/2013/6/5/javascript_in_your_postgres
[ruby-in-pg]: https://github.com/knu/postgresql-plruby
[pg-notify]: http://www.postgresql.org/docs/current/static/sql-notify.html
[node-pg-notify]: https://www.npmjs.com/package/pg-pubsub
