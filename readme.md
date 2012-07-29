# cell-layout.css.scss #

Simple, flexible cell-based layout in SASS that uses mixins to avoid the need for non-semantic class names in your markup.

No more nasty, non-semantic "span2" or "offset5" classes.  Adapt the framework to fit your existing markup by adding the width() mixin to your existing CSS classes, instead of having to re-write your markup to change or add classes (Twitter Bootstrap, I'm looking at you ಠ_ಠ).

Inspired by an original proof-of-concept in LESS by [Olly Nevard](http://ollynevard.co.uk/).

## Config variables ##

Passed to various mixins:

**$layoutwidth** (default: 960px): Inner width of container (any CSS unit permitted).

**$cols** (default: 16): Number of horizontal columns in layout.

**$gutter** (default: 10px): Margin between cells and between cell and container edges (any CSS unit permitted).

**$direction** (default: left): Direction of layout - float cells left or right.

**$cellmininnerwidth** (default: 5px): Minimum possible inner width of any cell (cells smaller than this value will be set to this width - any CSS unit permitted).

## Mixins ##

### cell-container ###

Defines the class instantiating this mixin as the container for the whole layout. Sets width of element to `$width`+`$gutter`.  Sets all direct children of this element as cells in the layout.

### width(cols) ###

Sets the width of the instantiating element (in cells).

### new-row ###

Forces the instantiating element to start a new row in the layout.

### push(cols) ###

Indent the instantiating element by the specified distance (in cells).

### pull(cols) ###

Outdent (un-indent) the instantiating element by the specified distance (in cells).

## Example ##

### SCSS ###

    /* Set defaults for a small, simple demo layout */
    $cols: 4;
    $width: 240px;
    $gutter: 10px;
    
    /* Import cell-layout SCSS file */
    @import "cell-layout";

    /* Hook the various mixins up to whatever CSS class(es) you like */
    .layout { @include cell-container($cols, $width, $gutter); }
    .cell { @include width(1, $cols, $width, $gutter); }
    .doublecell { @include width(2, $cols, $width, $gutter); }
    .startrow { @include new-line; }
    .indent { @push(1, $cols, $width, $gutter) }
    .outdent { @pull(1, $cols, $width, $gutter) }

### Markup ###

    <div class="layout">
      <div class="cell">A</div>
      <div class="cell">B</div>
      <div class="cell">C</div>
      <div class="cell">D</div>

      <div class="doublecell startrow">E <!-- 2 cells wide --></div>
      <div class="cell indent">F <!-- Indented by 1 cell-width --></div>

      <div class="doublecell startrow">G</div>
      <div class="doublecell outdent">H <!-- Overlaps previous cell by 1 cell-width --></div>
      <div class="cell">I</div>
    </div>

### Result ###

    [A_____] [B_____] [C_____] [D_____]
    [E______________]          [F_____]
    [G_______[H______________] [I_____]