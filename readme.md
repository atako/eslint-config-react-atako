# Eslint and Prettier Setup

## Installing

## Local / Per Project Install

1. If you don't already have a `package.json` file, create one with `npm init`.

2. Then we need to install everything needed by the config:

```
npx install-peerdeps --dev eslint-config-atakoreactconfig
```

3. You can see in your package.json there are now a big list of devDependencies.

4. Create a `.eslintrc` file in the root of your project's directory (it should live where package.json does). Your `.eslintrc` file should look like this:

```json
{
  "extends": [
    "atakoreactconfig"
  ]
}
```

Tip: You can alternatively put this object in your `package.json` under the property `"eslintConfig":`. This makes one less file in your project.

5. You can add two scripts to your package.json to lint and/or fix:

```json
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint . --fix"
},
```

6. Now you can manually lint your code by running `npm run lint` and fix all fixable issues with `npm run lint:fix`. You probably want your editor to do this though.

## Settings

If you'd like to overwrite eslint or prettier settings, you can add the rules in your `.eslintrc` file. The [ESLint rules](https://eslint.org/docs/rules/) go directly under `"rules"` while [prettier options](https://prettier.io/docs/en/options.html) go under `"prettier/prettier"`. Note that prettier rules overwrite anything in my config (trailing comma, and single quote), so you'll need to include those as well. 

```js
{
  "extends": [
    "atakoreactconfig"
  ],
  "rules": {
    "no-console": 2,
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 120,
        "tabWidth": 8,
      }
    ]
  }
}
```

## With VS Code

You should read this entire thing. Serious!

Once you have done one, or both, of the above installs. You probably want your editor to lint and fix for you. Here are the instructions for VS Code:

1. Install the [ESLint package](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
2. Now we need to setup some VS Code settings via `Code/File` → `Preferences` → `Settings`. It's easier to enter these settings while editing the `settings.json` file, so click the `{}` icon in the top right corner:
  ```js
    // These are all my auto-save configs
  "editor.formatOnSave": true,
  // turn it off for JS and JSX, we will do this via eslint
  "[javascript]": {
    "editor.formatOnSave": false
  },
  "[javascriptreact]": {
    "editor.formatOnSave": false
  },
  // tell the ESLint plugin to run on save
  "eslint.autoFixOnSave": true,
  // Optional BUT IMPORTANT: If you have the prettier extension enabled for other languages like CSS and HTML, turn it off for JS since we are doing it through Eslint already
  "prettier.disableLanguages": ["javascript", "javascriptreact"],
  ```

## With Create React App

1. You gotta eject first `npm run eject` or `yarn eject`
1. run `npx install-peerdeps --dev eslint-config-atakoreactconfig`
1. Crack open your `package.json` and replace `"extends": "react-app"` with `"extends": "atakoreactconfig"`

