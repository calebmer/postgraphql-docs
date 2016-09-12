# postgraphql-docs

Documentation website for PostGraphQL.

## Getting Started
If you don't have [gatsby][1] installed globally, then do so.
```bash
npm install -g gatsby
```

## Develop
Run the development server
```bash
gatsby develop
```
Open site in browser at `localhost:8000`

Saved changes should reload without refreshing the browser. Until [this issue][2]
gets fixed, if a new file is created, restart `gatsby develop` and then refresh
your browser.

## Build
Build the site
```bash
gatsby build
```
The site is built to the `/public` directory. Test that the build worked by
running `gatsby serve-build` which serves the contents of the `/public` directory.

## Deploy
Deploy to github pages
```bash
npm run deploy
```

[1]: https://github.com/gatsbyjs/gatsby
[2]: https://github.com/webpack/webpack/issues/1162
