# Styling Content



## Content & Tags

Every element can have text content via `setContent`. If `tags: true` was
passed to the element's constructor, the content can contain tags. For example:

``` js
box.setContent('hello {red-fg}{green-bg}{bold}world{/bold}{/green-bg}{/red-fg}');
```

To make this more concise `{/}` cancels all character attributes.

``` js
box.setContent('hello {red-fg}{green-bg}{bold}world{/}');
```


### Colors

Blessed tags support the basic 16 colors for colors, as well as up to 256
colors.

``` js
box.setContent('hello {red-fg}{green-bg}world{/}');
```

Tags can also use hex colors (which will be reduced to the most accurate
terminal color):

``` js
box.setContent('hello {#ff0000-fg}{#00ff00-bg}world{/}');
```


### Attributes

Blessed supports all terminal attributes, including `bold`, `underline`,
`blink`, `inverse`, and `invisible`.

``` js
box.setContent('hello {bold}world{/bold}');
```


### Alignment

Newlines and alignment are also possible in content.

``` js
box.setContent('hello\n'
  + '{right}world{/right}\n'
  + '{center}foo{/center}\n');
  + 'left{|}right');
```

This will produce a box that looks like:

```
| hello                 |
|                 world |
|          foo          |
| left            right |
```


### Escaping

Escaping can either be done using `blessed.escape()`

```
box.setContent('here is an escaped tag: ' + blessed.escape('{bold}{/bold}'));
```

Or with the special `{open}` and `{close}` tags:

```
box.setContent('here is an escaped tag: {open}bold{close}{open}/bold{close}');
```

Either will produce:

```
here is an escaped tag: {bold}{/bold}
```


### SGR Sequences

Content can also handle SGR escape codes. This means if you got output from a
program, say `git log` for example, you can feed it directly to an element's
content and the colors will be parsed appropriately.

This means that while `{red-fg}foo{/red-fg}` produces `^[[31mfoo^[[39m`, you
could just feed `^[[31mfoo^[[39m` directly to the content.


## Style Object

The style option controls most of the visual aspects of an element.

``` js
  style: {
    fg: 'blue',
    bg: 'black',
    bold: true,
    underline: false,
    blink: false,
    inverse: false,
    invisible: false,
    transparent: false,
    border: {
      fg: 'blue',
      bg: 'red'
    },
    scrollbar: {
      bg: 'blue'
    },
    focus: {
      bg: 'red'
    },
    hover: {
      bg: 'red'
    }
  }
```


### Colors

Colors can be the names of any of the 16 basic terminal colors, along with hex
values (e.g. `#ff0000`) for 256 color terminals. If 256 or 88 colors is not
supported. Blessed with reduce the color to whatever is available.


### Attributes

Blessed supports all terminal attributes, including `bold`, `underline`,
`blink`, `inverse`, and `invisible`. Attributes are represented as bools in the
`style` object.


### Transparency

Blessed can set the opacity of an element to 50% using `style.transparent =
true;`. While this seems like it normally shouldn't be possible in a terminal,
blessed will use a color blending algorithm to blend the element of the
foremost element with the background behind it. Obviously characters cannot be
blended, but background colors can.


### Shadow

Translucent shadows are also an option when it comes to styling an element.
This option will create a 50% opacity 2-cell wide, 1-cell high shadow offset to
the bottom-right.

``` js
shadow: true
```


### Effects

Blessed supports hover and focus styles. (Hover is only useful is mouse input
is enabled).

``` js
  style: {
    hover: {
      bg: 'red'
    },
    focus: {
      border: {
        fg: 'blue'
      }
    }
  }
```


### Scrollbar

On scrollable elements, blessed will support style options for the scrollbar,
such as:

``` js
style: {
  scrollbar: {
    bg: 'red',
    fg: 'blue'
  }
}
```

As a main option, scrollbar will either take a bool or an object:

``` js
scrollbar: {
  ch: ' '
}
```

Or:

``` js
scrollbar: true
```


## Events

Events in Blessed work similar to the traditional node.js model, with one
important difference: they have a concept of a tree and event bubbling.


### Event Bubbling

Events can bubble in blessed. For example:

Receiving all click events for `box` (a normal event listener):

``` js
box.on('click', function(mouse) {
  box.setContent('You clicked ' + mouse.x + ', ' + mouse.y + '.');
  screen.render();
});
```

Receiving all click events for `box`, as well as all of its children:

``` js
box.on('element click', function(el, mouse) {
  box.setContent('You clicked '
    + el.type + ' at ' + mouse.x + ', ' + mouse.y + '.');
  screen.render();
  if (el === box) {
    return false; // Cancel propagation.
  }
});
```

`el` gets passed in as the first argument. It refers to the target element the
event occurred on. Returning `false` will cancel propagation up the tree.


## Positioning

Offsets may be a number, a percentage (e.g. `50%`), or a keyword (e.g.
`center`).

Dimensions may be a number, or a percentage (e.g. `50%`).

Positions are treated almost _exactly_ the same as they are in CSS/CSSOM when
an element has the `position: absolute` CSS property.

When an element is created, it can be given coordinates in its constructor:

``` js
var box = blessed.box({
  left: 'center',
  top: 'center',
  bg: 'yellow',
  width: '50%',
  height: '50%'
});
```

This tells blessed to create a box, perfectly centered __relative to its
parent__, 50% as wide and 50% as tall as its parent.

Percentages can also have offsets applied to them:

``` js
  ...
  height: '50%-1',
  left: '45%+1',
  ...
```

To access the calculated offsets, relative to the parent:

``` js
console.log(box.left);
console.log(box.top);
```

To access the calculated offsets, absolute (relative to the screen):

``` js
console.log(box.aleft);
console.log(box.atop);
```


### Overlapping offsets and dimensions greater than parents'

This still needs to be tested a bit, but it should work.


## Rendering

To actually render the screen buffer, you must call `render`.

``` js
box.setContent('Hello {#0fe1ab-fg}world{/}.');
screen.render();
```

Elements are rendered with the lower elements in the children array being
painted first. In terms of the painter's algorithm, the lowest indices in the
array are the furthest away, just like in the DOM.


## Artificial Cursors

Terminal cursors can be tricky. They all have different custom escape codes to
alter. As an _experimental_ alternative, blessed can draw a cursor for you,
allowing you to have a custom cursor that you control.

``` js
var screen = blessed.screen({
  cursor: {
    artificial: true,
    shape: 'line',
    blink: true,
    color: null // null for default
  }
});
```

That's it. It's controlled the same way as the regular cursor.

To create a custom cursor:

``` js
var screen = blessed.screen({
  cursor: {
    artificial: true,
    shape: {
      bg: 'red',
      fg: 'white',
      bold: true,
      ch: '#'
    },
    blink: true
  }
});
```


## Multiple Screens

Blessed supports the ability to create multiple screens. This may not seem
useful at first, but if you're writing a program that serves terminal
interfaces over http, telnet, or any other protocol, this can be very useful.

### Server Side Usage

A simple telnet server might look like this (see examples/blessed-telnet.js for
a full example):

``` js
var blessed = require('blessed');
var telnet = require('telnet2');

telnet({ tty: true }, function(client) {
  client.on('term', function(terminal) {
    screen.terminal = terminal;
    screen.render();
  });

  client.on('size', function(width, height) {
    client.columns = width;
    client.rows = height;
    client.emit('resize');
  });

  var screen = blessed.screen({
    smartCSR: true,
    input: client,
    output: client,
    terminal: 'xterm-256color',
    fullUnicode: true
  });

  client.on('close', function() {
    if (!screen.destroyed) {
      screen.destroy();
    }
  });

  screen.key(['C-c', 'q'], function(ch, key) {
    screen.destroy();
  });

  screen.on('destroy', function() {
    if (client.writable) {
      client.destroy();
    }
  });

  screen.data.main = blessed.box({
    parent: screen,
    left: 'center',
    top: 'center',
    width: '80%',
    height: '90%',
    border: 'line',
    content: 'Welcome to my server. Here is your own private session.'
  });

  screen.render();
}).listen(2300);
```

Once you've written something similar and started it, you can simply telnet
into your blessed app:

``` bash
$ telnet localhost 2300
```

Creating a netcat server would also work as long as you disable line buffering
and terminal echo on the commandline via `stty`:
`$ stty -icanon -echo; ncat localhost 2300; stty icanon echo`

Or by using netcat's `-t` option: `$ ncat -t localhost 2300`

Creating a streaming http 1.1 server than runs in the terminal is possible by
curling it with special arguments: `$ curl -sSNT. localhost:8080`.

There are currently no examples of netcat/nc/ncat or http->curl servers yet.

---

The `blessed.screen` constructor can accept `input`, `output`, and `term`
arguments to aid with this. The multiple screens will be managed internally by
blessed. The programmer just has to keep track of the references, however, to
avoid ambiguity, it's possible to explicitly dictate which screen a node is
part of by using the `screen` option when creating an element.

The `screen.destroy()` method is also crucial: this will clean up all event
listeners the screen has bound and make sure it stops listening on the event
loop. Make absolutely certain to remember to clean up your screens once you're
done with them.

A tricky part is making sure to include the ability for the client to send the
TERM which is reset on the serverside, and the terminal size, which is should
also be reset on the serverside. Both of these capabilities are demonstrated
above.

For a working example of a blessed telnet server, see
`examples/blessed-telnet.js`.
