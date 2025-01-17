# doc-snippets
`doc-snippets` is a simple tool that allows you to extract and inject snippets from code into markdown files.

## Installation

Using NPM:
```bash
npm install --save-dev doc-snippets
```

Using Yarn:
```bash
yarn add -D doc-snippets
```

## Usage

### Marking and injecting

`doc-snippets` extracts and injects snippets by using tokens (without quotes):
- To mark a snippet:
  - `"$start: snippet-name"` - The start of a snippet and its name (required)
  - `"$end"` - The end of a snippet.
- To inject a snippet:
  - `"$snippet: snippet-name"` - This gets replaced by the snippet with the given name.

Snippets are injected only into `.md` files.

### Running `doc-snippets`

`doc-snippets` comes with a CLI tool which should handle most scenarios.

The CLI `combine` is the only currently supported command, and can be used as follows:

```bash
doc-snippets combine <snippetsDir> <docsDir> <outputDir>

# Extracts snippets from ./snippets and outputs a copy of ./src/docs into ./docs with injected snippets
doc-snippets combine ./snippets ./src/docs ./docs
```

#### Options

- `-i, --ignore <paths...>` - Ignore listed paths. Paths should be formatted according to the [gitignore spec 2.22.1](https://git-scm.com/docs/gitignore/2.22.1)
  - By default, only `node_modules` is ignored.

- `-e, --exts <exts...>` - Parse files with listed extensions
  - By default, files with the following extensions are parsed: `.ts`, `.json`, `.yaml`, `.txt`, `.md`, `.graphql`, and `.cue`

### In your own code

If you want to use `doc-snippets` programatically, it offers two exported functions:

```typescript
import { extractSnippets, injectSnippets } from "doc-snippets"

const snippets = await extractSnippets("./snippets") //Returns a `Record<string, string>` of all snippets found within `./snippets`.

await injectSnippets(snippets, "./dest") //Injects `snippets` into .md files found inside `./dest`
```
