# Code Formatting

Here is how I setup Code Formatting for our projects, you don't have to do anything, just to get more knowledge when you have to setup a new project

### Install dependencies

In this project, we use Eslint and Prettier to check for bad syntax and bad formatting

These packages must be installed as dev dependencies

```
pnpm i -D eslint eslint-config-prettier lint-staged prettier husky
```

Let's explain a little bit:

* **ESLint**: Find and fix problems in your JavaScript code
* **Prettier**: A code formatter that supports many languages and integrates with most editors
* **lint-staged**: Run linters against staged git files and don't let 💩 slip into your code base!
* **husky**: You can use it to **lint your commit messages**, **run tests**, **lint code**, etc... when you commit or push. Husky supports [all Git hooks](https://git-scm.com/docs/githooks).

### Configs for ESLint

Create a config file `.eslintrc.js` on the root folder

```
module.exports = {
    extends: ['react-app', 'react-app/jest', 'prettier'],
    parser: '@typescript-eslint/parser',
    parserOptions: {
        ecmaFeatures: {
            jsx: true,
        },
        ecmaVersion: 'latest',
        sourceType: 'module',
    },
    plugins: ['react', '@typescript-eslint'],
    rules: {
        "jsx-a11y/anchor-is-valid": "off",
        'max-len': [
            'warn',
            {
                code: 360,
            },
        ],
        'max-lines': [
            'warn',
            {
                max: 480,
                skipComments: true,
            },
        ],
    },
}

```

### Configs for Prettier

Create a configs file `.prettierrc`

```
{
    "trailingComma": "es5",
    "tabWidth": 4,
    "semi": false,
    "singleQuote": true,
    "printWidth": 120,
    "jsxSingleQuote": false,
    "bracketSpacing": true,
    "bracketSameLine": false,
    "arrowParens": "avoid",
    "singleAttributePerLine": false,
    "useTabs": false,
    "overrides": [
        {
            "files": "*.json",
            "options": {
                "tabWidth": 2
            }
        }
    ]
}
```

Create a file `.prettierignore` to ignore formatting code for some folders or files

```
# Ignore artifacts:
build
coverage
public
config
```

### Update `package.json`

```
{
  ...,
  "lint-staged": {
    "**/*.{ts,tsx,js,jsx}": [
      "prettier --write"
    ]
  }
}
```

This will format all staged files when you commit code

### Setup husky

Open `pre-commit` inside `.husky` folder (can be found in the project root)

By default, it should look like this

```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

```

Add this line to run `lint-staged` before code commited

```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

cd src/next && npx lint-staged
```

:tada::tada::tada: **Enjoy the new code formatter** :tada::tada::tada:



\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

#### In case you want to format code without committing or while coding, you can follow this way:

### Setup Prettier for your editor

#### For Visual Studio Code users, please navigate to extensions install this extension

![](<../../.gitbook/assets/image (1).png>)

{% hint style="info" %}
Shortcut:

* Mac: `Shift + Option + F`
* Windows: `Shift + Alt + F`
{% endhint %}



#### For Webstorm users, Prettier is default installed in your plugins, you just need to enable it to use

{% hint style="info" %}
Shortcut:

* Mac: `Ctrl + Option + L`
* Windows: ...
{% endhint %}



## **Coding Styles**

ESLint with `react-app` rules

**Rule #1: Always define your function/component type**

And put it into `src/types` folder

**Rule #2: Commenting your code**

Please read this article to see how to documenting your code: https://react-styleguidist.js.org/docs/documenting.html

**Rule #3: Write test for your code**

Resource: https://jestjs.io/docs/en/getting-started.html

**Rule #4: Separation of Concerns**

* Do not write Logic, UI view, Data in one single file, we have to separate it into Components/Custom Hooks/ Stores,...
* Limiting usage of state-full component since it storing data and View in one file. The better way to do it is using hook & custom hook.
* Each code file should not contain more than 300 line of code, we should break it down to a smaller file.
