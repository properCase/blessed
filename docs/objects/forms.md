# Forms


## Form

A form which can contain form elements.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __keys__ - Allow default keys (tab, vi keys, enter).
- __vi__ - Allow vi keys.

### Properties:

- Inherits [Box](objects/boxes.md#box).
- __submission__ - Last submitted data.

### Events:

- Inherits [Box](objects/boxes.md#box).
- __submit__ - Form is submitted. Receives a data object.
- __cancel__ - Form is discarded.
- __reset__ - Form is cleared.

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __focusNext()__ - Focus next form element.
- __focusPrevious()__ - Focus previous form element.
- __submit()__ - Submit the form.
- __cancel()__ - Discard the form.
- __reset()__ - Clear the form.


----
## Input

A form input.


----
## Textarea

A box which allows multiline text input.

### Options:

- Inherits [Input](objects/forms.md#input).
- __keys__ - Use pre-defined keys (`i` or `enter` for insert, `e` for editor,
  `C-e` for editor while inserting).
- __mouse__ - Use pre-defined mouse events (right-click for editor).
- __inputOnFocus__ - Call `readInput()` when the element is focused.
  Automatically unfocus.

### Properties:

- Inherits [Input](objects/forms.md#input).
- __value__ - The input text. __read-only__.

### Events:

- Inherits [Input](objects/forms.md#input).
- __submit__ - Value is submitted (enter).
- __cancel__ - Value is discard (escape).
- __action__ - Either submit or cancel.

### Methods:

- Inherits [Input](objects/forms.md#input).
- __submit__ - Submit the textarea (emits `submit`).
- __cancel__ - Cancel the textarea (emits `cancel`).
- __readInput(callback)__ - Grab key events and start reading text from the
  keyboard. Takes a callback which receives the final value.
- __readEditor(callback)__ - Open text editor in `$EDITOR`, read the output from
  the resulting file. Takes a callback which receives the final value.
- __getValue()__ - The same as `this.value`, for now.
- __clearValue()__ - Clear input.
- __setValue(text)__ - Set value.


----
## Textbox

A box which allows text input.

### Options:

- Inherits [Textarea](objects/forms.md#textarea).
- __secret__ - Completely hide text.
- __censor__ - Replace text with asterisks (`*`).

### Properties:

- Inherits [Textarea](objects/forms.md#textarea).
- __secret__ - Completely hide text.
- __censor__ - Replace text with asterisks (`*`).

### Events:

- Inherits [Textarea](objects/forms.md#textarea).

### Methods:

- Inherits [Textarea](objects/forms.md#textarea).


----
## Button

A button which can be focused and allows key and mouse input.

### Options:

- Inherits [Input](objects/forms.md#input).

### Properties:

- Inherits [Input](objects/forms.md#input).

### Events:

- Inherits [Input](objects/forms.md#input).
- __press__ - Received when the button is clicked/pressed.

### Methods:

- Inherits [Input](objects/forms.md#input).
- __press()__ - Press button. Emits `press`.


----
## Checkbox

A checkbox which can be used in a form element.

### Options:

- Inherits [Input](objects/forms.md#input).
- __checked__ - Whether the element is checked or not.
- __mouse__ - Enable mouse support.

### Properties:

- Inherits [Input](objects/forms.md#input).
- __text__ - The text next to the checkbox (do not use setContent, use
  `check.text = ''`).
- __checked__ - Whether the element is checked or not.
- __value__ - Same as `checked`.

### Events:

- Inherits [Input](objects/forms.md#input).
- __check__ - Received when element is checked.
- __uncheck__ received when element is unchecked.

### Methods:

- Inherits [Input](objects/forms.md#input).
- __check()__ - Check the element.
- __uncheck()__ - Uncheck the element.
- __toggle()__ - Toggle checked state.


----
## RadioSet

An element wrapping RadioButtons. RadioButtons within this element will be
mutually exclusive with each other.

### Options:

- Inherits [Box](objects/boxes.md#box).

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).


----
## RadioButton

A radio button which can be used in a form element.

### Options:

- Inherits [Checkbox](objects/forms.md#checkbox).

### Properties:

- Inherits [Checkbox](objects/forms.md#checkbox).

### Events:

- Inherits [Checkbox](objects/forms.md#checkbox).

### Methods:

- Inherits [Checkbox](objects/forms.md#checkbox).
