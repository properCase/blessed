

# Prompts


## Prompt

A prompt box containing a text input, okay, and cancel buttons (automatically
hidden).

### Options:

- Inherits [Box](objects/boxes.md#box).

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __input/setInput/readInput(text, value, callback)__ - Show the prompt and
  wait for the result of the textbox. Set text and initial value.

----

## Question

A question box containing okay and cancel buttons (automatically hidden).

### Options:

- Inherits [Box](objects/boxes.md#box).

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __ask(question, callback)__ - Ask a `question`. `callback` will yield the
  result.

----

## Message

A box containing a message to be displayed (automatically hidden).

### Options:

- Inherits [Box](objects/boxes.md#box).

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __log/display(text, [time], callback)__ - Display a message for a time
  (default is 3 seconds). Set time to 0 for a perpetual message that is
  dismissed on keypress.
- __error(text, [time], callback)__ - Display an error in the same way.

----

## Loading

A box with a spinning line to denote loading (automatically hidden).

### Options:

- Inherits [Box](objects/boxes.md#box).

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __load(text)__ - Display the loading box with a message. Will lock keys until
  `stop` is called.
- __stop()__ - Hide loading box. Unlock keys.

