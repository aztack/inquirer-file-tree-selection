## Inquirer Dir Select Prompt

> This repo forked from `https://github.com/anc95/inquirer-file-tree-selection`
> - Add `isShow` options to filter the files and directories.
> - Add ESM+CJS support at the same time

### QuickDemo
![QuickDemo](./example/screenshot.gif)

### Install
```sh
npm install inquirer-dir-select-prompt
```

### Usage
```js
inquirer.registerPrompt('file-tree-selection', inquirerFileTreeSelection)

inquirer.prompt({
  type: 'file-tree-selection',
  isShow(item, parentPath) {
    return item.name !== 'node_modules' && item.name[0] !== '.';
  }
})
```

### Options
Takes `type`, `name`, `message`, [`filter`, `validate`, `transformer`, `default`, `pageSize`, `onlyShowDir`, `onlyShowValid`, `hideChildrenOfValid`, `root`, `hideRoot`, `multiple`, `enableGoUpperDirector`] properties.

The extra options that this plugin provides are:
- `onlyShowDir`:  (Boolean) if true, will only show directory. Default: false.
- `root`: (String) it is the root of file tree. Default: process.cwd().
- `onlyShowValid`: (Boolean) if true, will only show valid files (if `validate` is provided). Default: false.
- `hideChildrenOfValid`: (Boolean) if true, will hide children of valid directories (if `validate` is provided). Default: false.
- `transformer`: (Function) a hook function to transform the display of directory or file name.
- `multiple`: (Boolean) if true, will enable to select multiple files. Default: false.
- `enableGoUpperDirectory`: (Boolean) Show `..` in inside root dir, and the user can press **space** on it to go upper directory. Default: false.
  When `multiple` is enabled, `default` should be `string[]` type, otherwise it's `string` type.

This fork added following options:

- `isShow`: (Function) a hook function to filter the display of directory or file name.
- `i18n`:
```ts
  /* i18n config */
  i18n?: {
    /**
     * .(root directory)
     */
    rootDirectory?: string;
    /**
     * (Press \`Space\` to go parent directory)
     */
    pressSpaceToGoToParentDirectory?: string;
    /**
     * (Use arrow keys, Use space to toggle folder)
     */
    UseArrowKeysUseSpaceToToggleFolder?: string;
    /**
     * '----------------';
     */
    pageSeparator?: string
  };
```

## Symbols customization

```ts
// Builtin symbols
export const figures = {
  arrowDown: '↓',
  arrowRight: '→',
  play: '▶',
  radioOn: '◉',
  radioOff: '◯',
};
```

Customization:

```ts
import {figures} from 'inquirer-file-tree-selection-prompt';
figures.arrowRight = '▶';
```

### Typescript Support

> version >= 1.0.16

1. Install `@types/inquirer`

2. Ensure you have registered with `file-tree-selection`

```js
inquirer.registerPrompt('file-tree-selection', inquirerFileTreeSelection)
```

3. And you will get type support when you code in IDE

![ts](./example/ts.jpeg)

### Example

ESM (version ^2)

```js
import inquirer from 'inquirer'
import inquirerFileTreeSelection from 'inquirer-dir-select-prompt'

inquirer.registerPrompt('file-tree-selection', inquirerFileTreeSelection)

inquirer
  .prompt([
    {
      type: 'file-tree-selection',
      name: 'file'
    }
  ])
  .then(answers => {
    console.log(JSON.stringify(answers))
  });
```

```js
const inquirer = require('inquirer')
const inquirerFileTreeSelection = require('inquirer-dir-select-prompt')

inquirer.registerPrompt('file-tree-selection', inquirerFileTreeSelection)

inquirer
  .prompt([
    {
      type: 'file-tree-selection',
      name: 'file'
    }
  ])
  .then(answers => {
    console.log(JSON.stringify(answers))
  });
```

[More examples](./example/)