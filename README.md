This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.ts`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

This project uses [`next/font`](https://nextjs.org/docs/basic-features/font-optimization) to automatically optimize and load Inter, a custom Google Font.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.

## Engine Locking

We would like for all developers working on this project to use the same Node engine and package manager we are using. To do that we create two new files:

- `.nvmrc` - Will tell other users of the project which version of Node is used
- `.npmrc` - Will tell other users of the project which package manager is used

We are using `Node v14 Fermium` and `yarn` for this project so we set those values like so:

`.nvmrc`

```.nvmrc
lts/fermium
```

`.npmrc`

```
engine-strict=true
```

The reason we are using v14 instead of v16 for Node is that later in the tutorial we will be deploying on Vercel which unfortunately still does not support Node 16. Perhaps by the time you read this tutorial it might. You can follow the progress [here](https://github.com/vercel/community/discussions/37).

You can check your version of Node with `node --version` and make sure you are setting the correct one. A list of Node version codenames can be found [here](https://github.com/nodejs/Release/blob/main/CODENAMES.md)

Note that the use of `engine-strict` didn't specifically say anything about `yarn`, we do that in `package.json`:

`package.json`

```json
  "name": "nextjs-fullstack-app-template",
  "author": "YOUR_NAME",
  "description": "A tutorial and template for creating a production-ready fullstack Next.js application",
  "version": "0.1.0",
  "private": true,
  "license" : "MIT"
  "homepage": "YOUR_GIT_REPO_URL"
  "engines": {
    "node": ">=14.0.0",
    "yarn": ">=1.22.0",
    "npm": "please-use-yarn"
  },
  ...
```

## Git Setup

This would be a good time to make our first commit to our remote repo, to make sure our changes are backed up, and to follow best practices for keeping related changes grouped within a single commit before moving to something new.

By default your Next.js project will already have a repo initialized. You can check what branch you are on with `git status`. It should say something like:

```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .npmrc
        .nvmrc
```

This tells us we are on the `main` branch and we have not staged or made any commits yet.

Let's commit our changes so far.

```
git add .
git commit -m 'project initialization'
```

The first command will add and stage all files in your project directory that aren't ignored in `.gitignore`. The second will make a commit of the state of your current project with the message we wrote after the `-m` flag.

Hop over to your preferred git hosting provider ([Github](https://github.com) for example) and create a new repository to host this project. Make sure the default branch is se tto the same name as the branch on your local machine to avoid any confusion.

On Github you can change your global default branch name to whatever you like by going to:

### ESLint

We'll begin with ESLint, which is easy because it automatically comes installed and pre-configured with Next.js projects.

We are just going to add a little bit of extra configuration and make it a bit stricter than it is by default. If you disagree with any of the rules it sets, no need to worry, it's very easy to disable any of them manually. We configure everything in `.eslintrc.json` which should already exist in your root directory:

`.eslintrc.js`

```js
module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true,
  },
  extends: [
    'airbnb',
    'prettier',
    'plugin:react/recommended',
    'plugin:import/typescript',
    'plugin:@typescript-eslint/recommended',
    'prettier',
  ],
  settings: {
    'import/resolver': {
      node: {
        extensions: ['.tsx', '.ts', '.js', '.json'],
      },
      alias: [
        ['src', './src'],
        ['server', './server'],
      ],
    },
  },
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 12,
    sourceType: 'module',
  },
  plugins: ['react', '@typescript-eslint', 'react-hooks'],
  rules: {
    semi: 0,
    indent: 0,
    'react/jsx-filename-extension': 0,
    'react/prop-types': 0,
    'react/jsx-props-no-spreading': 0,
    'react/require-default-props': 0,

    'jsx-a11y/click-events-have-key-events': 0,
    'jsx-a11y/no-static-element-interactions': 0,
    'jsx-a11y/no-noninteractive-element-interactions': 0,
    'jsx-a11y/anchor-is-valid': 0,

    'no-use-before-define': 0,
    'no-unused-vars': 0,
    'no-param-reassign': 0,
    'implicit-arrow-linebreak': 0,
    'consistent-return': 0,
    'arrow-parens': 0,
    'object-curly-newline': 0,
    'operator-linebreak': 0,
    'import/no-extraneous-dependencies': 0,
    'import/extensions': 0,
    'import/no-unresolved': 0,
    'import/prefer-default-export': 0,

    '@typescript-eslint/ban-ts-comment': 0,
    '@typescript-eslint/no-var-requires': 0,
    '@typescript-eslint/explicit-module-boundary-types': 0,

    'no-underscore-dangle': 0,
    'react/function-component-definition': 0,
    'react/react-in-jsx-scope': 0,
    '@typescript-eslint/ban-types': 0,
    '@typescript-eslint/no-empty-interface': 0,
    'arrow-body-style': 0,
    '@typescript-eslint/no-explicit-any': 0,
    'no-shadow': 'off',
    '@typescript-eslint/no-shadow': ['error'],
    'import/no-cycle': 0,
    'prefer-arrow-callback': 0,
  },
};
```

```
yarn add eslint-config-airbnb
yarn add eslint-config-next
yarn add eslint-config-prettier
yarn add eslint-import-resolver-alias
yarn add eslint-import-resolver-typescript
yarn add eslint-plugin-import
yarn add eslint-plugin-jest
yarn add eslint-plugin-jsx-a11y
yarn add eslint-plugin-react
yarn add eslint-plugin-react-hooks
yarn add @typescript-eslint/eslint-plugin
yarn add @typescript-eslint/parser
```

In the above small code example we have added a few additional defaults, we have said that `React` will always be defined even if we don't specifically import it, and I have added a personal custom rule that I like which allows you to prefix variables with an underscore \_ if you have declared them but not used them in the code.

I find that scenario comes up often when you are working on a feature and want to prepare variables for use later, but have not yet reached the point of implementing them.

You can test out your config by running:

```
yarn lint
```

You should get a message like:

```
✔ No ESLint warnings or errors
Done in 1.47s.
```

If you get any errors then ESLint is quite good at explaining clearly what they are. If you encounter a rule you don't like you can disable it in "rules" by simply setting it to 1 (warning) or 0 (ignore) like so:

```json
  "rules": {
    "no-unused-vars": 0, // As example: Will never bug you about unused variables again
  }
```

Let's make a commit at this point with the message `build: configure eslint`

### Prettier

Prettier will take care of automatically formatting our files for us. Let's add it to the project now.

It's only needed during development, so I'll add it as a `devDependency` with `-D`

```
yarn add -D prettier
```

I also recommend you get the [Prettier VS Code extension](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) so that VS Code can handle the formatting of the files for you and you don't need to rely on the command line tool. Having it installed and configured in your project means that VSCode will use your project's settings, so it's still necessary to add it here.

We'll create two files in the root:

`.prettierrc`

```.prettierrc
{
  "trailingComma": "es5",
  "tabWidth": 2,
  "semi": true,
  "singleQuote": true
}
```

Those values are entirely at your discretion as to what is best for your team and project.

`.prettierignore`

```
.yarn
.next
dist
node_modules
```

## Git Hooks

One more section on configuration before we start getting into component development. Remember you're going to want this project to be as rock solid as possible if you're going to be building on it in the long term, particularly with a team of other developers. It's worth the time to get it right at the start.

We are going to implement a tool called [Husky](https://typicode.github.io/husky/#/)

Husky is a tool for running scripts at different stages of the git process, for example add, commit, push, etc. We would like to be able to set certain conditions, and only allow things like commit and push to succeed if our code meets those conditions, presuming that it indicates our project is of acceptable quality.

To install Husky run

```
yarn add -D husky
npx husky install
```

The second command will create a `.husky` directory in your project. This is where your hooks will live. Make sure this directory is included in your code repo as it's intended for other developers as well, not just yourself.

Add the following script to your `package.json` file:

`package.json`

```
  ...
  "scripts: {
    ...
    "prepare": "husky install"
  }
```

This will ensure Husky gets installed automatically when other developers run the project.

To create a hook run

```
npx husky add .husky/pre-commit "yarn lint"
```

The above says that in order for our commit to succeed, the `yarn lint` script must first run and succeed. "Succeed" in this context means no errors. It will allow you to have warnings (remember in the ESLint config a setting of 1 is a warning and 2 is an error in case you want to adjust settings).

Let's create a new commit with the message `ci: implement husky`. If all has been setup properly your lint script should run before the commit is allowed to occur.

We're going to add another one:

```
npx husky add .husky/pre-push "yarn build"
```

The above ensures that we are not allowed to push to the remote repository unless our code can successfully build. That seems like a pretty reasonable condition doesn't it? Feel free to test it by committing this change and trying to push.

---

Lastly we are going to add one more tool. We have been following a standard convention for all our commit messages so far, let's ensure that everyone on the team is following them as well (including ourselves!). We can add a linter for our commit messages:

```
yarn add -D @commitlint/config-conventional @commitlint/cli
```

To configure it we will be using a set of standard defaults, but I like to include that list explicitly in a `commitlint.config.js` file since I sometimes forget what prefixes are available:

`commitlint.config.js`

```js
// build: Changes that affect the build system or external dependencies (example scopes: gulp, broccoli, npm)
// ci: Changes to our CI configuration files and scripts (example scopes: Travis, Circle, BrowserStack, SauceLabs)
// docs: Documentation only changes
// feat: A new feature
// fix: A bug fix
// perf: A code change that improves performance
// refactor: A code change that neither fixes a bug nor adds a feature
// style: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
// test: Adding missing tests or correcting existing tests
module.exports = {
  extends: ['@commitlint/config-conventional'],
  rules: {
    'body-leading-blank': [1, 'always'],
    'body-max-line-length': [2, 'always', 100],
    'footer-leading-blank': [1, 'always'],
    'footer-max-line-length': [2, 'always', 100],
    'header-max-length': [2, 'always', 100],
    'scope-case': [2, 'always', 'lower-case'],
    'subject-case': [
      2,
      'never',
      ['sentence-case', 'start-case', 'pascal-case', 'upper-case'],
    ],
    'subject-empty': [2, 'never'],
    'subject-full-stop': [2, 'never', '.'],
    'type-case': [2, 'always', 'lower-case'],
    'type-empty': [2, 'never'],
    'type-enum': [
      2,
      'always',
      [
        'build',
        'chore',
        'ci',
        'docs',
        'feat',
        'fix',
        'perf',
        'refactor',
        'revert',
        'style',
        'test',
        'translation',
        'security',
        'changeset',
      ],
    ],
  },
};
```
