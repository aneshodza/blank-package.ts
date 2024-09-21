# blank-package.ts
This repostory is a template for npm packages using typescript.
There are a few things you need to change when you make use of this repo, so please **full-text search for every `<TODO>` you can find**. Replace those with what you actually want it to say.

## How To Use
This template has the whole setup needed to make typescript npm libraries.
It comes with a few utilities pre-loaded, to make development easier.
The `package.json` provides a few utility-commands:
```json
...
"scripts": {
    "lint": "eslint 'src/**/*.ts'",
    "fix-lint": "eslint 'src/**/*.ts' --fix",
    "prepare": "husky",
    "build": "npm run build:compile && npm run build:fix",
    "build:fix": "fix-esm-import-path out/*.js",
    "build:compile": "tsc",
    "build:clean": "rm -rf out",
    "test": "jest --coverage",
    "develop": "npx tsc --watch --outDir out/"
},
...
```
All will be explained in the next chapters

### Settings On GitHub
For publishing to work you need to generate an npm Access Token:
1. Navigate to [npmjs.com](https://www.npmjs.com)
2. Go to Settings > Access Tokens
3. Press Generate New Token > Classic Token
4. As the type you should define "Automation"
5. Copy your new access token

Then you need to apply it:
1. Navigate to your repository
2. Go to Settings > Secrets and variables > Actions
3. Click New repository secret and name it `NPM_TOKEN`. In the Secret paste your npmjs token

### Local Development
Development should always be done with a second terminal session using:
```bash
npm run develop
```
This ensures that all written typescript code gets transpiled into the `/out` directory. It automatically creates map files, type files and the javascript files.

#### Linting
Linting is also pre-configured using eslint and tslint. They can be run using:
```bash
npm run lint
```
This will show where `eslint/tslint` found errors.
To autofix simply run:
```bash
npm run fix-lint
```

#### Hooks
A pre-commit hook is defined using `husky`. It automatically gets initialized and run before every commit. In case it finds anything (using the `npm run lint` command), it aborts the commit.

### Testing
The test environment is set up with `jest` and `ts-jest`, meanings it's very easy to write tests.
All tests must follow following pattern in order to be run:
```bash
/tests/**/*.test.ts
```
The `package.json` provides

#### Coverage Reports
After running tests using `npm test` a coverage file will be created unter `/coverage`, showing which lines got ran by the tester.

### Building
To build the project you can use:
```bash
npm run build
```

### CI/CD
CI/CD is all done automatically on GitHub using the defined workflows under `.github/workflows`:
```
.github/
    workflows/
        publish.yml
        tests.yml
```
As the naming makes obvious one file runs tests and the other publishes.

#### How Tests Get Run
The tests get run on every push to any branch. They check the code with our linters first and then run tests. If the tests pass or not will be displayed using a green check or a red cross next to the commit message.  

#### How Publishing works
Publishing automatically gets done when a new tag is pushed to main.
First, the automation checks if the version in your `package.json` matches the tag you just pushed. In case that doesn't match it fails the publish instantly.  
At the same time it runs the whole test CI once more to make sure everything is okay.  
In case all of that comes true, it publishes the package to npmjs.

#### Automated documentation
This repository makes use of `typedoc` to automatically display all `jsdocs` in html. It also takes all Markdown Files under `docs/` and adds those.  
It pushes that website to github pages automatically whenever publishing to the npm registry is done.  
For an example, see [the adt.ts library](https://aneshodza.github.io/adt.ts/)

##### Running it manually
If you want to run it manually just to update the website (which I would disencourage) you can do so. For that navigate to Your Repository > Actions and then select Manually publish docs to gh pages in the left sidebar. You can manually trigger that workflow.

#### The Other Commands
While there are a few other commands namespaced under `build:*` they are just used inside the build. In case you are interested in understanding those, just read them.

== Links below are to be used! Change the credits! ==

---

## Other Links
- [Changelog](./docs/other_links/CHANGELOG.md)
- [Contributing](./docs/other_links/CONTRIBUTING.md)
- [Bugs](./docs/other_links/BUGS.md)
- [Feature requests](./docs/other_links/FEATURE_REQUESTS.md)

#### Credits
This template was written and published by [Anes Hodza](https://www.aneshodza.ch)
<TODO>
