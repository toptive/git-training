# Git Training

[![Netlify Status](https://api.netlify.com/api/v1/badges/c57cec29-7c4e-4ac6-9bc2-d5c0536d8a86/deploy-status)](https://app.netlify.com/sites/focused-chandrasekhar-0cc7c7/deploys)

A Git training for Toptive

## Installation

It is recommended to globally install `docsify-cli` globally, which helps initializing and previewing the website locally.

```shell
npm i -g docsify-cli
```

## Usage

Run the local server with `docsify serve`.

You can preview your site in your browser on `http://localhost:3000`.

```shell
docsify serve docs
```

## Prettier

You can format the code with [Prettier](https://prettier.io). Run this command in the project root:

```bash
npm i -g prettier
prettier --print-width 80 --single-quote --trailing-comma none --write "**/*.{js,ts,jsx,tsx,md,html,css}"
```

## Credits

- [docsify-starter](https://github.com/fvcproductions/docsify-starter) 🍫
