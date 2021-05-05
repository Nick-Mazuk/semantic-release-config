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

## Available commit types

- **build**: Changes that affect the build system (example scopes: gulp, broccoli, npm)
- **bump**: Dependency updates
- **ci**: Changes to our CI configuration files and scripts (example scopes: Circle, BrowserStack, SauceLabs)
- **docs**: Documentation only changes
- **feat**: A new feature
- **fix**: A bug fix
- **perf**: A code change that improves performance
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **test**: Adding missing tests or correcting existing tests
- **style**: A change in CSS
- **BREAKING**: Any breaking change
