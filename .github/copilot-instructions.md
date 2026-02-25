# Copilot Instructions for tree-sitter-mulle-objc

## Project Overview

This repository contains a [tree-sitter](https://tree-sitter.github.io) grammar for [mulle-objc](https://www.mulle-kybernetik.com/de-re-mulle-objc/), a dialect of Objective-C. The grammar extends [tree-sitter-c](https://github.com/tree-sitter/tree-sitter-c) and adds Objective-C and mulle-objc specific constructs.

The grammar is published on npm as [`tree-sitter-mulle-objc`](https://www.npmjs.com/package/tree-sitter-mulle-objc) under the npm account `mulle_nat`, and on PyPI as [`tree-sitter-mulle-objc`](https://pypi.org/project/tree-sitter-mulle-objc/).

## Key Files and Directories

- **`grammar.js`** – The main grammar definition. Extends `tree-sitter-c/grammar` and adds Objective-C and mulle-objc rules.
- **`src/`** – Generated C parser files (`parser.c`, `scanner.c`). Do **not** edit manually; regenerate with `tree-sitter generate`.
- **`queries/`** – Tree-sitter query files: `highlights.scm`, `injections.scm`, `locals.scm`.
- **`test/corpus/`** – Corpus test files in tree-sitter test format. Subdirectory `c/` contains C tests inherited from tree-sitter-c.
- **`bindings/`** – Language bindings: `c`, `go`, `node`, `python`, `rust`, `swift`.
- **`tree-sitter.json`** – Grammar metadata (name, file types, scope, binding flags).

## Building and Testing

Install Node.js dependencies first:

```sh
npm install
```

Generate the parser from `grammar.js` (required after any grammar change):

```sh
npx tree-sitter generate
```

Run the corpus tests:

```sh
npx tree-sitter test
# or
make test
```

Lint `grammar.js`:

```sh
npm run lint
```

Run Node.js binding tests:

```sh
npm test
```

## Coding Conventions

- **Grammar changes** always go in `grammar.js`. Never edit files under `src/` directly.
- After editing `grammar.js`, always regenerate the parser with `tree-sitter generate` and run the test suite.
- Features disabled for mulle-objc are marked with `// MULLE_DISABLED:` comments in `grammar.js`. Do not remove these comments.
- New language constructs should have corpus test cases added in `test/corpus/` using the standard tree-sitter test format (see existing files for examples).
- Query files (`queries/*.scm`) use the [tree-sitter query syntax](https://tree-sitter.github.io/tree-sitter/syntax-highlighting#queries). Keep captures consistent with other tree-sitter grammars.
- The grammar `name` field in `grammar.js` is `'objc'` (not `mulle-objc`); this is intentional for node type compatibility.
