# Template Typescript Repository

## Description
This is a repository I use as a base for my typescript libraries. It includes a basic setup for typescript, eslint, prettier, jest and GitHub Actions.

Feel free to use this template, clone it and use it as a base for your own projects.

## Pre-requisites
- Node 16.5.0 or newer

## Setup
- No setup required

## Development
- `npm run lint` - Lint the code and checks types
- `npm run format` - Formats the code using prettier
- `npm test` - Compiles code and runs tests


## Publishing to NPM
1. Compile the code
   2. `npm run build`
3. Publish the package
   4. `npm publish`


## Appendices

### Appendix A: Publishing to private NPM Repository
Once you have setup your private NPM repository, you can publish your package to it by running the following command:
```
npm publish --registry <Your repository URL here>
```

To safeguard for accidentally publishing to the public NPM repository, you can add the following to your package.json, I usually do the following.
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
'release': 'RELEASE_MODE=True npm run build && npm publish --registry <Your repository URL here> && git push --follow-tags',
...,
}
```

Then change any Github actions etc. to use `npm run release` instead of `npm publish`.


