

# Notes


## Windows Compatibility

Currently there is no `mouse` or `resize` event support on Windows.

Windows users will need to explicitly set `term` when creating a screen like so
(__NOTE__: This is no longer necessary as of the latest versions of blessed.
This is now handled automatically):

``` js
var screen = blessed.screen({ terminal: 'windows-ansi' });
```


## Low-level Usage

This will actually parse the xterm terminfo and compile every
string capability to a javascript function:

``` js
var blessed = require('blessed');

var tput = blessed.tput({
  terminal: 'xterm-256color',
  extended: true
});

process.stdout.write(tput.setaf(4) + 'Hello' + tput.sgr0() + '\n');
```

To play around with it on the command line, it works just like tput:

``` bash
$ tput.js setaf 2
$ tput.js sgr0
$ echo "$(tput.js setaf 2)Hello World$(tput.js sgr0)"
```

The main functionality is exposed in the main `blessed` module:

``` js
var blessed = require('blessed')
  , program = blessed.program();

program.key('q', function(ch, key) {
  program.clear();
  program.disableMouse();
  program.showCursor();
  program.normalBuffer();
  process.exit(0);
});

program.on('mouse', function(data) {
  if (data.action === 'mousemove') {
    program.move(data.x, data.y);
    program.bg('red');
    program.write('x');
    program.bg('!red');
  }
});

program.alternateBuffer();
program.enableMouse();
program.hideCursor();
program.clear();

program.move(1, 1);
program.bg('black');
program.write('Hello world', 'blue fg');
program.setx((program.cols / 2 | 0) - 4);
program.down(5);
program.write('Hi again!');
program.bg('!black');
program.feed();
```


## Testing

Most tests contained in the `test/` directory are interactive. It's up to the
programmer to determine whether the test is properly displayed. In the future
it might be better to do something similar to vttest.


## Examples

Examples can be found in `examples/`.


## FAQ

1. Why doesn't the Linux console render lines correctly on Ubuntu?
- You need to install the `ncurses-base` package __and__ the `ncurses-term`
  package. (#98)
2. Why do vertical lines look chopped up in iTerm2?
- All ACS vertical lines look this way in iTerm2 with the default font.
3. Why can't I use my mouse in Terminal.app?
- Terminal.app does not support mouse events.
4. Why doesn't the OverlayImage element appear in my terminal?
- The OverlayImage element uses w3m to display images. This generally only
  works on X11+xterm/urxvt, but it _may_ work on other unix terminals.
5. Why can't my mouse clicks register beyond 255 cells?
- Older versions of VTE do not support any modern mouse protocol. On top of
  that, the old X10 protocol it _does_ implement is bugged. Through several
  workarounds we've managed to get the cell limit from `127` to `255`. If
  you're not happy with this, you may want to look into using xterm or urxvt,
  or a terminal which uses a modern VTE, like gnome-terminal.
6. Is blessed efficient?
- Yes. Blessed implements CSR and uses the painter's algorithm to render the
  screen. It maintains two screen buffers so it only needs to render what
  has changed on the terminal screen.
7. Will blessed work with all terminals?
- Yes. Blessed has a terminfo/termcap parser and compiler that was written
  from scratch. It should work with every terminal as long as a terminfo
  file is provided. If you notice any compatibility issues in your termial,
  do not hesitate to post an issue.
8. What is "curses" and "ncurses"?
- ["curses"][curses] was an old library written in the early days of unix
  which allowed a programmer to easily manipulate the cursor in order to
  render the screen. ["ncurses"][ncurses] is a free reimplementation of
  curses. It improved upon it quite a bit by focusing more on terminal
  compatibility and is now the standard library for implementing terminal
  programs. Blessed uses neither of these, and instead handles terminal
  compatibility itself.
9. What is the difference between blessed and blessed-contrib?
- blessed is a major piece of code which reimplements curses from the ground
  up. A UI API is then layered on top of this. [blessed-contrib][contrib] is
  a popular library built on top of blessed which makes clever use of modules
  to implement useful widgets like graphs, ascii art, and so on.
10. Are there blessed-like solutions for non-javascript platforms?
- Yes. There are some fantastic solutions out there.
    - Perl: [Curses::UI][curses-ui]
    - Python: [Urwid][urwid]
    - Go: [termui][termui] & [termbox-go][termbox]
