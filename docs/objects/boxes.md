## Box

A box element which draws a simple box containing `content` or other elements.

### Options:

- Inherits [Element](base/element.md).

### Properties:

- Inherits [Element](base/element.md).

### Events:

- Inherits [Element](base/element.md).

### Methods:

- Inherits [Element](base/element.md).

----
## BigText

A box which can render content drawn as 8x14 cell characters using the terminus
font.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __font__ - bdf->json font file to use (see [ttystudio][ttystudio] for
  instructions on compiling BDFs to JSON).
- __fontBold__ - bdf->json bold font file to use (see [ttystudio][ttystudio]
  for instructions on compiling BDFs to JSON).
- __fch__ - foreground character. (default: `' '`)

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).

-----

## Line

A simple line which can be `line` or `bg` styled.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __orientation__ - Can be `vertical` or `horizontal`.
- __type, bg, fg, ch__ - Treated the same as a border object.
  (attributes can be contained in `style`).

Inherits all options, properties, events, and methods from Box.


-----

## Text

An element similar to Box, but geared towards rendering simple text elements.

### Options:

- Inherits [Element](base/element.md).
- __fill__ - Fill the entire line with chosen bg until parent bg ends, even if
  there is not enough text to fill the entire width. __(deprecated)__
- __align__ - Text alignment: `left`, `center`, or `right`.

Inherits all options, properties, events, and methods from Element.
