# pretty-best-effort
This is a pretty printer that doesn't understand the actual syntax of the language but just enough to figure out what groups and separators are. This is useful if you want to display content that looks like code in a tight space but don't have control over and may be using a wide variety of programming languages. This is a single file, 200 lines of code, no dependencies.

## How does it work

The idea is that it's going to try and pretty-print all the groups inline, but if the rendered version is more than 40 characters, then write each element on its own line and indent it. Groups and separators are defined by these characters:

```js
const openGroup = '[{(<';
const closeGroup = ']})>';
const separator = ',;';
```

For example,

```js
{editor: atom$TextEditor, position: {column: number, row: number}}
```

is pretty printed with maxColumnWidth of 40 characters as

```js
{
  editor: atom$TextEditor,
  position: {column: number, row: number}
}
```

The group `{column: number, row: number}` is less than 40 characters so is printed inline but the outer group would be more than 40 characters so each element is printed line by line and indented.

Note that this is just an heuristic that tends to work well in most cases. It is not going to be perfect all the time!

In case an input cannot be parsed based on this grammar, it's going to return the input unchanged.

## How to use

```bash
npm install pretty-best-effort
```

```js
import prettyBestEffort from 'pretty-best-effort';
console.log(prettyBestEffort('{editor: atom$TextEditor, position: {column: number, row: number}}', 40));
// Output:
// `{
//   editor: atom$TextEditor,
//   position: {column: number, row: number}
// }`
```
