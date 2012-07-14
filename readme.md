# cell-layout.css.scss #

Simple, flexible cell-based layout in SASS that uses mixins to avoid the need for non-semantic class names in your markup.

## Config variables ##

**$width** (default: 960px): Inner width of container (any CSS unit permitted).

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

    $width: 240px;
    $cols: 4;
    $gutter: 10px;
    $direction: left;
    $cellmininnerwidth: 5px;

    .layout { @include cell-container; }
    .cell { @include width(1); }
    .doublecell { @include width(2); }
    .startrow { @include new-line; }
    .indent { @push(1) }
    .outdent { @pull(1) }

### Markup ###

    <div class="layout">
      <div class="cell">Span 1</div>
      <div class="cell">Span 1</div>
      <div class="cell">Span 1</div>
      <div class="cell">Span 1</div>

      <div class="doublecell startrow">Span 2</div>
      <div class="cell indent">Span 1 indented 1</div>

      <div class="doublecell startrow">Span 2</div>
      <div class="doublecell outdent">Span 2 outdented 1 (overlaps previous cell by 1 cell-width)</div>
      <div class="cell">Span 1</div>
    </div>