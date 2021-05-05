# Semantic release config

A config for [semantic-release](https://github.com/semantic-release/semantic-release).

- Adds a few extra commit types
- Creates changelog automatically
- Pushes changelog back into Git repo

## Installation

Install the config and it's peer dependencies.

```bash
pnpm i -D @nick-mazuk/semantic-release-config semantic-release @semantic-release/changelog @semantic-release/git
```

Create a `release.config.js` file in the root of your repo.

```js
module.exports = {
    extends: ['@nick-mazuk/semantic-release-config'],
}
```

## Usage with GitHub Actions

Create a `.github/workflows/release.yml` file.

```yml
name: Release

on:
  push:
    branches:
      - main

jobs:
  release:
    name: Release
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2.1.5
        with:
          node-version: 14
      - name: Install dependencies
        run: npx pnpm i --frozen-lockfile=false
      - name: Release
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
        run: npx semantic-release
```

Add your `NPM_TOKEN` token to your repository's secrets.
