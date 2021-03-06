# Contributing to onedark.vim

Please read this document before submitting a Pull Request.

**Pull Requests containing changes to files in the `autoload/` or `colors/` directories without corresponding changes to files in the `build/templates` directory will _not_ be merged.**

## Build System

### Background Information

onedark.vim and its companion [lightline.vim](https://github.com/itchyny/lightline.vim) and [vim-airline](https://github.com/vim-airline/vim-airline) themes are built using a rudimentary templating and build system that allows color definitions to live in a single, central file.

The basic idea is that the theme files are generated by a build tool, which in turn substitutes color values into templates that live in `build/templates`.

Here are the locations of the theme files that are generated by the build system, along with the locations of the corresponding templates they are generated from:

| Theme Location                               | Template Location                        |
|----------------------------------------------|------------------------------------------|
| `colors/onedark.vim`                         | `build/templates/onedark.template.vim`   |
| `autoload/lightline/colorscheme/onedark.vim` | `build/templates/lightline.template.vim` |
| `autoload/airline/themes/onedark.vim`        | `build/templates/airline.template.vim`   |

### Configure It

1) Install [Node.js](https://nodejs.org/en/) (Installing via [nvm](https://github.com/creationix/nvm) or [homebrew](https://brew.sh) are both better options than the official Node.js installer.)

2) Run the following from within the root of this repository. This will install the build system's dependencies and will automatically configure a Git pre-commit hook that runs `npm test` (see below).

```bash
> cd build
> npm install
```

That's it!

### Use It

The build system consists of a single Node.js script, `build.js`, which supports two commands:

* Running `./build.js` or `npm run build` generates theme files from the templates, **overwriting changes to the theme files without confirmation.**
* Running `./build.js check` or `npm test` checks that the theme files match the template-generated output, **without modifying theme files**. This command ensures that the theme files perfectly match the templates they are generated from, which is useful for detecting changes that were made to generated theme files but that should have been made in the templates. (In addition to running `./build.js check`, `npm test` also runs [eslint](http://eslint.org) linting on the build system code to catch and prevent simple problems with changes to that code.)

The basic development workflow looks like this:

1. Make changes to the appropriate template files in `build/templates`, then run `npm run build` from inside the `build` directory.

2. Commit your change in Git. `npm test` will automatically run before your commit is finalized. If the test fails, fix any inconsistencies between the template files and theme files (or linting errors in `build.js` if applicable), then try committing again.

## Style Guidelines

Please match the existing comment and whitespace style in all template files.

For the "Language-Specific Highlighting" portion of onedark.vim, blocks for each language should be organized alphabetically ("Markdown" comes before "PHP").

Any changes to the JavaScript code in the build system should pass against the included eslint rules; you can manually check for linting errors by running `npm test` from inside the `build` directory.

## Thanks!

Thanks very much for contributing to onedark.vim!
