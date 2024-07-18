# Lists

## List

A scrollable list which can display selectable items.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __style.selected__ - Style for a selected item.
- __style.item__ - Style for an unselected item.
- __mouse__ - Whether to automatically enable mouse support for this list
  (allows clicking items).
- __keys__ - Use predefined keys for navigating the list.
- __vi__ - Use vi keys with the `keys` option.
- __items__ - An array of strings which become the list's items.
- __search__ - A function that is called when `vi` mode is enabled and the key
  `/` is pressed. This function accepts a callback function which should be
  called with the search string. The search string is then used to jump to an
  item that is found in `items`.
- __interactive__ - Whether the list is interactive and can have items selected
  (Default: true).
- __invertSelected__ - Whether to automatically override tags and invert fg of
  item when selected (Default: `true`).

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).
- __select__ - Received when an item is selected.
- __cancel__ - List was canceled (when `esc` is pressed with the `keys` option).
- __action__ - Either a select or a cancel event was received.

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __add/addItem(text)__ - Add an item based on a string.
- __removeItem(child)__ - Removes an item from the list. Child can be an
  element, index, or string.
- __pushItem(child)__ - Push an item onto the list.
- __popItem()__ - Pop an item off the list.
- __unshiftItem(child)__ - Unshift an item onto the list.
- __shiftItem()__ - Shift an item off the list.
- __insertItem(i, child)__ - Inserts an item to the list. Child can be an
  element, index, or string.
- __getItem(child)__ - Returns the item element. Child can be an element,
  index, or string.
- __setItem(child, content)__ - Set item to content.
- __spliceItem(i, n, item1, ...)__ - Remove and insert items to the list.
- __clearItems()__ - Clears all items from the list.
- __setItems(items)__ - Sets the list items to multiple strings.
- __getItemIndex(child)__ - Returns the item index from the list. Child can be
  an element, index, or string.
- __select(index)__ - Select an index of an item.
- __move(offset)__ - Select item based on current offset.
- __up(amount)__ - Select item above selected.
- __down(amount)__ - Select item below selected.
- __pick(callback)__ - Show/focus list and pick an item. The callback is
  executed with the result.
- __fuzzyFind([string/regex/callback])__ - Find an item based on its text
  content.

----

## FileManager

A very simple file manager for selecting files.

### Options:

- Inherits [List](lists.md#list).
- __cwd__ - Current working directory.

### Properties:

- Inherits [List](lists.md#list).
- __cwd__ - Current working directory.

### Events:

- Inherits [List](lists.md#list).
- __cd__ - Directory was selected and navigated to.
- __file__ - File was selected.

### Methods:

- Inherits [List](lists.md#list).
- __refresh([cwd], [callback])__ - Refresh the file list (perform a `readdir` on `cwd`
  and update the list items).
- __pick([cwd], callback)__ - Pick a single file and return the path in the callback.
- __reset([cwd], [callback])__ - Reset back to original cwd.

----

## ListTable

A stylized table of text elements with a list.

### Options:

- Inherits [List](lists.md#list).
- __rows/data__ - Array of array of strings representing rows.
- __pad__ - Spaces to attempt to pad on the sides of each cell. `2` by default:
  one space on each side (only useful if the width is shrunken).
- __noCellBorders__ - Do not draw inner cells.
- __style.header__ - Header style.
- __style.cell__ - Cell style.

### Properties:

- Inherits [List](lists.md#list).

### Events:

- Inherits [List](lists.md#list).

### Methods:

- Inherits [List](lists.md#list).
- __setRows/setData(rows)__ - Set rows in table. Array of arrays of strings.
``` js
  table.setData([
    [ 'Animals',  'Foods'  ],
    [ 'Elephant', 'Apple'  ],
    [ 'Bird',     'Orange' ]
  ]);
```


#### Listbar

A horizontal list. Useful for a main menu bar.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __style.selected__ - Style for a selected item.
- __style.item__ - Style for an unselected item.
- __commands/items__ - Set buttons using an object with keys as titles of
  buttons, containing of objects containing keys of `keys` and `callback`.
- __autoCommandKeys__ - Automatically bind list buttons to keys 0-9.

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __setItems(commands)__ - Set commands (see `commands` option above).
- __add/addItem/appendItem(item, callback)__ - Append an item to the bar.
- __select(offset)__ - Select an item on the bar.
- __removeItem(child)__ - Remove item from the bar.
- __move(offset)__ - Move relatively across the bar.
- __moveLeft(offset)__ - Move left relatively across the bar.
- __moveRight(offset)__ - Move right relatively across the bar.
- __selectTab(index)__ - Select button and execute its callback.

