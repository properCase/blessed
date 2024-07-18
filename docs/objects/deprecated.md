## ScrollableBox

__DEPRECATED__ - Use Box with the `scrollable` option instead.

A box with scrollable content.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __baseLimit__ - A limit to the childBase. Default is `Infinity`.
- __alwaysScroll__ - A option which causes the ignoring of `childOffset`. This
  in turn causes the childBase to change every time the element is scrolled.
- __scrollbar__ - Object enabling a scrollbar.
- __scrollbar.style__ - Style of the scrollbar.
- __scrollbar.track__ - Style of the scrollbar track if present (takes regular
  style options).

### Properties:

- Inherits [Box](objects/boxes.md#box).
- __childBase__ - The offset of the top of the scroll content.
- __childOffset__ - The offset of the chosen item/line.

### Events:

- Inherits [Box](objects/boxes.md#box).
- __scroll__ - Received when the element is scrolled.

### Methods:

- __scroll(offset)__ - Scroll the content by a relative offset.
- __scrollTo(index)__ - Scroll the content to an absolute index.
- __setScroll(index)__ - Same as `scrollTo`.
- __setScrollPerc(perc)__ - Set the current scroll index in percentage (0-100).
- __getScroll()__ - Get the current scroll index in lines.
- __getScrollHeight()__ - Get the actual height of the scrolling area.
- __getScrollPerc()__ - Get the current scroll index in percentage.
- __resetScroll()__ - Reset the scroll index to its initial state.


## ScrollableText

__DEPRECATED__ - Use Box with the `scrollable` and `alwaysScroll` options
instead.

A scrollable text box which can display and scroll text, as well as handle
pre-existing newlines and escape codes.

### Options:

- Inherits [~ScrollableBox~](objects/deprecated.md#scrollablebox).
- __mouse__ - Whether to enable automatic mouse support for this element.
- __keys__ - Use predefined keys for navigating the text.
- __vi__ - Use vi keys with the `keys` option.

### Properties:

- Inherits [~ScrollableBox~](objects/deprecated.md#scrollablebox).

### Events:

- Inherits [~ScrollableBox~](objects/deprecated.md#scrollablebox).

### Methods:

- Inherits [~ScrollableBox~](objects/deprecated.md#scrollablebox).
