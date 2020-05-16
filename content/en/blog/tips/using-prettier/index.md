---
title: "Prettier in your projects"
linkTitle: "Prettier in your projects"
date: 2020-05-16
author: "Eduardo Asenjo"
description: >
  How to setup your **Prettier** config per project *(or per folder)*
---

## What is Prettier?

Prettier is an opionated code formatter with support for multipple languages.

It removes all original styling and ensures that all outputted code conforms to a consistent style.

Prettier takes your code and reprints it from scratch by taking the line length into account.

For example, take the following code:

```javascript
foo(arg1, arg2, arg3, arg4);
```

It fits in a single line so it's going to stay as is. However, we've all run into this situation:

```js
foo(reallyLongArg(), omgSoManyParameters(), IShouldRefactorThis(), isThereSeriouslyAnotherOne());
```
Suddenly our previous format for calling function breaks down because this is too long. Prettier is going to do the painstaking work of reprinting it like that for you:

```js
foo(
  reallyLongArg(),
  omgSoManyParameters(),
  IShouldRefactorThis(),
  isThereSeriouslyAnotherOne()
);
```

Prettier enforces a consistent code style (i.e. code formatting that won't affect the AST) across your entire codebase because it disregards the original styling by parsing it away and re-printing the parsed AST with its own rules that take the maximum line length into account, wrapping code when necessary.

{{% alert title="Check Prettier.io" color="info" %}}
There is much more information about Prettier in [Prettier.io](https://prettier.io/docs/en/index.html)
{{% /alert %}}


## Can we use it in Salesforce development?

Prettier code formatter supports Aura and Lightning Web Components (LWC) as well as standard file formats such as JSON, Markdown, HTML, and JavaScript. Prettier can also support Apex if you [install Prettier Apex plugin](https://developer.salesforce.com/tools/vscode/en/user-guide/prettier/) authored by Dang Mai.

##### Sample `.prettierrc` file

```json
{
	"trailingComma": "none",
	"overrides": [
		{
			"files": "**/lwc/**/*.html",
			"options": { "parser": "lwc" }
		},
		{
			"files": "*.{cmp,page,component}",
			"options": { "parser": "html" }
		}
	],
	"printWidth": 120,
	"tabWidth": 4,
	"useTabs": true,
	"semi": true,
	"singleQuote": false,
	"quoteProps": "as-needed",
	"bracketSpacing": true,
	"arrowParens": "always",
	"requirePragma": false,
	"insertPragma": false,
	"endOfLine": "lf"
}
```
{{% alert color="info" %}}
More options available in [Prettier documentation](https://prettier.io/docs/en/options.html)
{{% /alert %}}
Basically the [official Salesforce documentation](https://developer.salesforce.com/tools/vscode/en/user-guide/prettier/) teaches you to install and start from the scratch with it, but what about a project that already has a `.prettierrc` file?

This plugin is a **npm** package, therefore you might need **Node** and **npm** installed; any project where you want to use **Prettier** must be initialized as a **Node** project. 

This is really easy to identify, just take a look at the project and check if there is a `package.json` file in it. Probably if the project contains a `.prettierrc` file it should potentially have `prettier` and `prettier-plugin-apex` packages in the `devDependencies` key inside the `package.json`

If you are not familiar with **Node** and **npm** packages, the next step right before you want to start working with your project or a recently cloned project is to run the command `npm install`. This will install the current package, `dependencies` & `devDependencies` defined in the existing `package.json` file in the context folder.

You will notice a folder `node_modules` is created, is where all the info about the packages and dependencies related are stored. Usually we always might want to ignore it with `.gitignore`

## How do we use it in Raspi's Dojo?

All our projects probably will have a `.prettierrc` file and the necessary dependencies for development defined in the `package.json` *(unless we forgot about it)* in order to make sure every contributor can easily follow the same rules and all our projects and code-base is structured in the same format, making it easier to read and follow.

We always will try to provide scripts in the **npm** `package.json` to run automatically **Prettier** and other necessary tools from your favourite console or text editor. 

We will use these scripts as well in our automated pipelines in order to make sure everyone if following these rules and avoid manual review of style conventions.