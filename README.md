# 14721-yarn-lockfile-parser-unconventional-semver

This repo reproduces a bug in the `yarn.lock` parser for nx@15.6.x.

https://github.com/nrwl/nx/issues/14721

## Steps to reproduce

1. Clone this repo
2. Run `yarn install`
3. Run `nx g @nrwl/js:lib example --compiler=tsc --buildable --publishable --importPath=@my-ns/example`
4. Run `yarn config set npmScopes.gitlab-examples.npmRegistryServer "https://gitlab.com/api/v4/packages/npm/"`
5. Run `cd libs/example`
6. Run `yarn add @gitlab-examples/semantic-release-npm`
7. Run `cd - && nx build example`


Observe generated package.json in `dist/libs/example` now uses an unconventional semver for `@gitlab-examples/semantic-release-npm`.
This breaks installation for consumers of the library using npm.
   