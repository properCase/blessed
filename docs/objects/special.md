
# Special Elements


## Terminal

A box which spins up a pseudo terminal and renders the output. Useful for
writing a terminal multiplexer, or something similar to an mc-like file
manager. Requires term.js and pty.js to be installed. See
`example/multiplex.js` for an example terminal multiplexer.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __handler__ - Handler for input data.
- __shell__ - Name of shell. `$SHELL` by default.
- __args__ - Args for shell.
- __cursor__ - Can be `line`, `underline`, and `block`.
- __terminal__ - Terminal name (Default: `xterm`).
- __env__ - Object for process env.
- Other options similar to term.js'.

### Properties:

- Inherits [Box](objects/boxes.md#box).
- __term__ - Reference to the headless term.js terminal.
- __pty__ - Reference to the pty.js pseudo terminal.

### Events:

- Inherits [Box](objects/boxes.md#box).
- __title__ - Window title from terminal.
- Other events similar to ScrollableBox.

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __write(data)__ - Write data to the terminal.
- __screenshot([xi, xl, yi, xl])__ - Nearly identical to `element.screenshot`,
  however, the specified region includes the terminal's _entire_ scrollback,
  rather than just what is visible on the screen.
- Other methods similar to ScrollableBox.


## Image

Display an image in the terminal (jpeg, png, gif) using either Blessed's
internal png/gif-to-terminal renderer (using a [ANSIImage element](#ansiimage)) or
using `w3mimgdisplay` (using a [OverlayImage element](#overlayimage)).

### Options:

- Inherits [Box](objects/boxes.md#box).
- __file__ - Path to image.
- __type__ - `ansi` or `overlay`. Whether to render the file as ANSI art or
  using `w3m` to overlay. See the [ANSIImage element](#ansiimage) for
  more information/options. (__default__: `ansi`).

### Properties:

- Inherits [Box](objects/boxes.md#box).
- See [ANSIImage element](#ansiimage)
- See [OverlayImage element](#overlayimage)

### Events:

- Inherits [Box](objects/boxes.md#box).
- See [ANSIImage element](#ansiimage)
- See [OverlayImage element](#overlayimage)

### Methods:

- Inherits [Box](objects/boxes.md#box).
- See [ANSIImage element](#ansiimage)
- See [OverlayImage element](#overlayimage)


## ANSIImage

Convert any `.png` file (or `.gif`, see below) to an ANSI image and display it
as an element. This differs from the `OverlayImage` element in that it uses
Blessed's internal PNG/GIF parser and does not require external dependencies.

Blessed uses an internal from-scratch PNG/GIF reader because no other javascript
PNG reader supports Adam7 interlaced images (much less pass the png test
suite).

The blessed PNG reader supports adam7 deinterlacing, animation (APNG), all
color types, bit depths 1-32, alpha, alpha palettes, and outputs scaled bitmaps
(cellmaps) in blessed for efficient rendering to the screen buffer. It also
uses some code from libcaca/libcucul to add density ASCII characters in order
to give the image more detail in the terminal.

If a corrupt PNG or a non-PNG is passed in, blessed will display error text in
the element.

`.gif` files are also supported via a javascript implementation (they are
internally converted to bitmaps and fed to the PNG renderer). Any other image
format is support only if the user has imagemagick (`convert` and `identify`)
installed.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __file__ - URL or path to PNG/GIF file. Can also be a buffer.
- __scale__ - Scale cellmap down (`0-1.0`) from its original pixel width/height
  (Default: `1.0`).
- __width/height__ - This differs from other element's `width` or `height` in
  that only one of them is needed: blessed will maintain the aspect ratio of
  the image as it scales down to the proper number of cells. __NOTE__: PNG/GIF's
  are always automatically shrunken to size (based on scale) if a `width` or
  `height` is not given.
- __ascii__ - Add various "density" ASCII characters over the rendering to give
  the image more detail, similar to libcaca/libcucul (the library mplayer uses
  to display videos in the terminal).
- __animate__ - Whether to animate if the image is an APNG/animating GIF. If
  false, only display the first frame or IDAT (Default: `true`).
- __speed__ - Set the speed of animation. Slower: `0.0-1.0`. Faster: `1-1000`.
  It cannot go faster than 1 frame per millisecond, so 1000 is the fastest.
  (Default: 1.0)
- __optimization__ - `mem` or `cpu`. If optimizing for memory, animation frames
  will be rendered to bitmaps _as the animation plays_, using less memory.
  Optimizing for cpu will precompile all bitmaps beforehand, which may be
  faster, but might also OOM the process on large images. (Default: `mem`).

### Properties:

- Inherits [Box](objects/boxes.md#box).
- __img__ - Image object from the png reader.
- __img.width__ - Pixel width.
- __img.height__ - Pixel height.
- __img.bmp__ - Image bitmap.
- __img.cellmap__ - Image cellmap (bitmap scaled down to cell size).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __setImage(file)__ - Set the image in the box to a new path. File can be a
  path, url, or buffer.
- __clearImage()__ - Clear the image.
- __play()__ - Play animation if it has been paused or stopped.
- __pause()__ - Pause animation.
- __stop()__ - Stop animation.


## OverlayImage

Display an image in the terminal (jpeg, png, gif) using w3mimgdisplay. Requires
w3m to be installed. X11 required: works in xterm, urxvt, and possibly other
terminals.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __file__ - Path to image.
- __ansi__ - Render the file as ANSI art instead of using `w3m` to overlay
  Internally uses the ANSIImage element. See the [ANSIImage element](#ansiimage) for
  more information/options. (Default: `true`).
- __w3m__ - Path to w3mimgdisplay. If a proper `w3mimgdisplay` path is not
  given, blessed will search the entire disk for the binary.
- __search__ - Whether to search `/usr`, `/bin`, and `/lib` for
  `w3mimgdisplay` (Default: `true`).

### Properties:

- Inherits [Box](objects/boxes.md#box).

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).
- __setImage(img, [callback])__ - Set the image in the box to a new path.
- __clearImage([callback])__ - Clear the current image.
- __imageSize(img, [callback])__ - Get the size of an image file in pixels.
- __termSize([callback])__ - Get the size of the terminal in pixels.
- __getPixelRatio([callback])__ - Get the pixel to cell ratio for the terminal.
- _Note:_ All methods above can be synchronous as long as the host version of
  node supports `spawnSync`.


## Video

A box which spins up a pseudo terminal in order to render a video via `mplayer
-vo caca` or `mpv --vo caca`. Requires `mplayer` or `mpv` to be installed with
libcaca support.

### Options:

- Inherits [Box](objects/boxes.md#box).
- __file__ - Video to play.
- __start__ - Start time in seconds.

### Properties:

- Inherits [Box](objects/boxes.md#box).
- __tty__ - The terminal element running `mplayer` or `mpv`.

### Events:

- Inherits [Box](objects/boxes.md#box).

### Methods:

- Inherits [Box](objects/boxes.md#box).


## Layout

A layout which can position children automatically based on a `renderer` method
(__experimental__ - the mechanics of this element may be changed in the
future!).

By default, the Layout element automatically positions children as if they were
`display: inline-block;` in CSS.

### Options:

- Inherits [Element](base/element.md).
- __renderer__ - A callback which is called right before the children are
  iterated over to be rendered. Should return an iterator callback which is
  called on each child element: __iterator(el, i)__.
- __layout__ - Using the default renderer, it provides two layouts: inline, and
  grid. `inline` is the default and will render akin to `inline-block`. `grid`
  will create an automatic grid based on element dimensions. The grid cells'
  width and height are always determined by the largest children in the layout.

### Properties:

- Inherits [Element](base/element.md).

### Events:

- Inherits [Element](base/element.md).

### Methods:

- Inherits [Element](base/element.md).
- __renderer(coords)__ - A callback which is called right before the children
  are iterated over to be rendered. Should return an iterator callback which is
  called on each child element: __iterator(el, i)__.
- __isRendered(el)__ - Check to see if a previous child element has been
  rendered and is visible on screen. This is __only__ useful for checking child
  elements that have already been attempted to be rendered! see the example
  below.
- __getLast(i)__ - Get the last rendered and visible child element based on an
  index. This is useful for basing the position of the current child element on
  the position of the last child element.
- __getLastCoords(i)__ - Get the last rendered and visible child element coords
  based on an index. This is useful for basing the position of the current
  child element on the position of the last child element. See the example
  below.

### Rendering a Layout for child elements

You must __always__ give `Layout` a width and height. This is a chicken-and-egg
problem: blessed cannot calculate the width and height dynamically _before_ the
children are positioned.

`border` and `padding` are already calculated into the `coords` object the
`renderer` receives, so there is no need to account for it in your renderer.

Try to set position for children using `el.position`. `el.position` is the most
primitive "to-be-rendered" way to set coordinates. Setting `el.left` directly
has more dynamic behavior which may interfere with rendering.

Some definitions for `coords` (otherwise known as `el.lpos`):

- `coords.xi` - the absolute x coordinate of the __left__ side of a rendered
  element. It is absolute: relative to the screen itself.
- `coords.xl` - the absolute x coordinate of the __right__ side of a rendered
  element. It is absolute: relative to the screen itself.
- `coords.yi` - the absolute y coordinate of the __top__ side of a rendered
  element. It is absolute: relative to the screen itself.
- `coords.yl` - the absolute y coordinate of the __bottom__ side of a rendered
  element. It is absolute: relative to the screen itself.

Note again: the `coords` the renderer receives for the Layout already has
border and padding subtracted, so you do not have to account for these. The
children do not.

### Example

Here is an example of how to provide a renderer. Note that this is also the
default renderer if none is provided. This renderer will render each child as
though they were `display: inline-block;` in CSS, as if there were a
dynamically sized horizontal grid from left to right.

``` js
var layout = blessed.layout({
  parent: screen,
  top: 'center',
  left: 'center',
  width: '50%',
  height: '50%',
  border: 'line',
  style: {
    bg: 'red',
    border: {
      fg: 'blue'
    }
  },
  // NOTE: This is already the default renderer if none is provided!
  renderer: function(coords) {
    var self = this;

    // The coordinates of the layout element
    var width = coords.xl - coords.xi
      , height = coords.yl - coords.yi
      , xi = coords.xi
      , xl = coords.xl
      , yi = coords.yi
      , yl = coords.yl;

    // The current row offset in cells (which row are we on?)
    var rowOffset = 0;

    // The index of the first child in the row
    var rowIndex = 0;

    return function iterator(el, i) {
      // Make our children shrinkable. If they don't have a height, for
      // example, calculate it for them.
      el.shrink = true;

      // Find the previous rendered child's coordinates
      var last = self.getLastCoords(i);

      // If there is no previously rendered element, we are on the first child.
      if (!last) {
        el.position.left = 0;
        el.position.top = 0;
      } else {
        // Otherwise, figure out where to place this child. We'll start by
        // setting it's `left`/`x` coordinate to right after the previous
        // rendered element. This child will end up directly to the right of it.
        el.position.left = last.xl - xi;

        // If our child does not overlap the right side of the Layout, set it's
        // `top`/`y` to the current `rowOffset` (the coordinate for the current
        // row).
        if (el.position.left + el.width <= width) {
          el.position.top = rowOffset;
        } else {
          // Otherwise we need to start a new row and calculate a new
          // `rowOffset` and `rowIndex` (the index of the child on the current
          // row).
          rowOffset += self.children.slice(rowIndex, i).reduce(function(out, el) {
            if (!self.isRendered(el)) return out;
            out = Math.max(out, el.lpos.yl - el.lpos.yi);
            return out;
          }, 0);
          rowIndex = i;
          el.position.left = 0;
          el.position.top = rowOffset;
        }
      }

      // If our child overflows the Layout, do not render it!
      // Disable this feature for now.
      if (el.position.top + el.height > height) {
        // Returning false tells blessed to ignore this child.
        // return false;
      }
    };
  }
});

for (var i = 0; i < 10; i++) {
  blessed.box({
    parent: layout,
    width: i % 2 === 0 ? 10 : 20,
    height: i % 2 === 0 ? 5 : 10,
    border: 'line'
  });
}
```
