---
title: JavaScript Ecosystem
draft: false
tags:
  - webdev
  - computer-science
  - js
---
### [ECMAScript](https://en.wikipedia.org/wiki/ECMAScript)(ES) = [JavaScript](https://en.wikipedia.org/wiki/JavaScript) (kind of)

[[JavaScript]] [[Compilers]] are known as [[runtime environments]] ([NodeJS](https://nodejs.org/en), Google Chrome). They are built on top of of [[ECMAScript]] [[Compilers]] ([V8](https://v8.dev/), [nitro](https://nitro.margelo.com/))

## Google [[V8]] Engine

The [[V8]]] Engine is an open-source JS execution engine - [Chronium projects](https://www.chromium.org/chromium-projects/). It can run standalone or extend into any [c++] app as a library.
- It is only a compiler, doesn't include [[I/O]] nor [API]
- It parses, interprets, executes & compiles [[JavaScript]] code.
- It's shipped only with the [API]s that [[ECMAScript]] standard specifies.

## NodeJS

[[JavaScript]] runtime, with [[CLI]], build on the [[V8]] engine.
- [[V8]] only provides core parsing & compiling. Features like async event loop/queue are built on top as part of [[NodeJS]].
- Also ships with [[I/O]] [[API]]s for network, file system operations & concept of modules.

## Google Chrome (or browsers in general)
[[HTML]] and [[CSS]] docs rendered for client-side [[UI]]s.

The [[V8]] engine is a small but critical part of a web browser.

The purpose of [[JavaScript]] execution in the web browser is to:
- Mutate the [[DOM]].
- Make network requests.
- Persist data client-side.

[JEST](https://jestjs.io/) - A testing framework
[NPM](https://www.npmjs.com/) - Node Package Manager, comes with [[NodeJS]]
[YARN](https://yarnpkg.com/) - Similar to [[NPM]], released by Facebook. Seen as significantly faster than npm.

[[package.json]] - it's tied to [NPM](https://www.npmjs.com/), used by both [[NPM]] and [[YARN]] to define metadata.

__Dependency Types__:
- dependencies
- devDependencies
- peerDependencies
- optionalDependencies

__Extensions to package.json__:
- eslintConfig --> used by [eslint](https://eslint.org/) to config linking for app
- browserslist --> specifies what browser types are supported by app