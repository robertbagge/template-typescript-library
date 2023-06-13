# Template Typescript Repository
[NPM Package](https://www.npmjs.com/package/@robertbagge/template-typescript-library)
## Description
This is a repository I use as a base for my typescript libraries. It includes a basic setup for typescript, eslint, prettier, jest and GitHub Actions.

Feel free to use this template, clone it and use it as a base for your own projects.

Always open for feedback if you think this repo can be improved further.

## Table of Contents
- [Description](#description)
- [Table of Contents](#table-of-contents)
- [Pre-requisites](#pre-requisites)
- [Setup](#setup)
- [Development](#development)
- [CI/CD](#cicd)
- [Publishing to NPM](#publishing-to-npm)
- [Appendices](#appendices)
  - [Appendix A: Publishing to private NPM Registry](#appendix-a-publishing-to-private-npm-registry)

## Pre-requisites
- Node 16.5.0 or newer

## Setup
- No setup required

## Development
- `npm run lint` - Lint the code and checks types
- `npm run format` - Formats the code using prettier
- `npm test` - Compiles code and runs tests

## CI/CD
This repo is setup with GitHub Actions to automatically run tests and publish the package to NPM when a new tag is pushed to the repo.

Currently the following actions are run on every commit
- Format code - Formats code with Pretties and commits changes to the repo
- Run tests - Runs tests and reports coverage
- Bump version - Bumps minor version and commits to package.json


## Publishing to NPM manually
- Compile the code
  - `npm run build`
- Publish the package
  - `npm publish`


## Appendices

### Appendix A: Publishing to private NPM Registry
Once you have setup your private NPM registry, you can publish your package to it by running the following command:
```
npm publish --registry <Your registry URL here>
```

To safeguard for accidentally publishing to the public NPM registry, you can add the following to your package.json, I usually do the following.
Add a file pre-publish.js to the root of the project with the following content:

```
const RELEASE_MODE = !!process.env.RELEASE_MODE;

if (!RELEASE_MODE) {
  console.log('Run `npm run release` to publish the package');
  process.exit(1); //which terminates the publish process
}
```

This will enforce the RELEASE_MODE environment variable to be set to true before publishing the package.

Then add a new `release` to the scripts section of your package.json:
```
scripts: {
...,
'release': 'RELEASE_MODE=True npm run build && npm publish --registry <Your registry URL here> && git push --follow-tags',
...,
}
```

Then change any Github actions etc. to use `npm run release` instead of `npm publish`.


