
# Data Display


## ProgressBar

A progress bar allowing various styles. This can also be used as a form input.

### Options:

- Inherits [Input](objects/forms.md#input).
- __orientation__ - Can be `horizontal` or `vertical`.
- __style.bar__ - Style of the bar contents itself.
- __pch__ - The character to fill the bar with (default is space).
- __filled__ - The amount filled (0 - 100).
- __value__ - Same as `filled`.
- __keys__ - Enable key support.
- __mouse__ - Enable mouse support.

### Properties:

- Inherits [Input](objects/forms.md#input).

### Events:

- Inherits [Input](objects/forms.md#input).
- __reset__ - Bar was reset.
- __complete__ - Bar has completely filled.

### Methods:

- Inherits [Input](objects/forms.md#input).
- __progress(amount)__ - Progress the bar by a fill amount.
- __setProgress(amount)__ - Set progress to specific amount.
- __reset()__ - Reset the bar.

----
## Log

A log permanently scrolled to the bottom.

### Options:

- Inherits [~ScrollableText~](objects/deprecated.md#scrollabletext).
- __scrollback__ - Amount of scrollback allowed. Default: Infinity.
- __scrollOnInput__ - Scroll to bottom on input even if the user has scrolled
  up. Default: false.

### Properties:

- Inherits [~ScrollableText~](objects/deprecated.md#scrollabletext).
- __scrollback__ - Amount of scrollback allowed. Default: Infinity.
- __scrollOnInput__ - Scroll to bottom on input even if the user has scrolled
  up. Default: false.

### Events:

- Inherits [~ScrollableText~](objects/deprecated.md#scrollabletext).
- __log__ - Emitted on a log line. Passes in line.

### Methods:

- Inherits [~ScrollableText~](objects/deprecated.md#scrollabletext).
- __log/add(text)__ - Add a log line.

----
## Table

A stylized table of text elements.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __rows/data__ - Array of array of strings representing rows.
- __pad__ - Spaces to attempt to pad on the sides of each cell. `2` by default:
  one space on each side (only useful if the width is shrunken).
- __noCellBorders__ - Do not draw inner cells.
- __fillCellBorders__ - Fill cell borders with the adjacent background color.
- __style.header__ - Header style.
- __style.cell__ - Cell style.

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __setRows/setData(rows)__ - Set rows in table. Array of arrays of strings.
``` js
  table.setData([
    [ 'Animals',  'Foods'  ],
    [ 'Elephant', 'Apple'  ],
    [ 'Bird',     'Orange' ]
  ]);
```

