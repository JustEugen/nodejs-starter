# nodejs-starter

If you need to write node.js application like express app, you want to make it with Typescript, this repo can be useful for you.

What do we have here:
- Typescript
- Path aliases
- Dotenv support
- File watcher

**Themes**
- [Environment variables using .env files](#environment-variables-using-env-files)
- [How to build?](#how-to-build)
- [How to run in watch/development mode?](#how-to-run-in-watchdevelopment-mode)
- [How to run in production mode?](#how-to-run-in-production-mode)
- [How to use path alias?](#how-to-use-path-alias)

### Environment variables using .env files

Pay attention that there are support `.env` files using `dontenv` plugin, but **ONLY** for development mode. Why? Usually you are not using `.env` files on production due to security risks, but if you need this, modify you `start` script:

```json
{
  ...
  "scripts": {
    ...
    "start": "npm run build && node -r dotenv/config ./build/main.js",
  }

}
```

### How to build?

To build project use next command:
```shell
$ npm run build
```

### How to run in watch/development mode?

To run project in watch mode, that means that it will make rebuild on every change you need to run next command:

```shell
$ npm run start:dev
```

We are using `nodemon` as a watcher, feel free to modify its config `nodemon.json`.

### How to run in production mode?

To run project in production use next command:
```shell
$ npm run start
```

This command will build your project and then run it.

### How to use `path alias`?

This sample has already `path alias` example.

Take a look into `utils/say-hello.ts`:
```ts
export const sayHello = () => {
  console.log('Hello!');
};
```

And how it's imported in `main.ts` file.

```ts
import { sayHello } from '@utils/say-hello';
```

To make `path alias` works, in `main.ts` file, on the very first line you should have next line:

```ts
import 'module-alias/register';
```

Then you need to define your aliases in both `tsconfig.json` and `package.json` files. There are some difference, in `tsconfig.json` you need to define `path` relative to your `src` structure.

`tsconfig.json`
```json
{
  ...
  "paths": {
    "@utils/*": ["utils/*"],
  }
}
```

But in `package.json` - relative to your build folder structure

```json
{
  ...
  "_moduleAliases": {
    "@utils": "./build/utils"
  }
}
```

All in all, they are the same, but in `package.json` you need to add `"./build/"` string.
