ATK UI Pantry
=============

## Mile High overview
A system made up of grid, border, spacing, positioning, text sizing, and color classes.

## Baseline
Baseline styles, or a simple “reset” 
```
html {
  box-sizing: border-box;
  font-size: 62.5%;
  margin: 0;
  padding: 0;
  
  *,
  *::before,
  *::after {
    box-sizing: inherit;
    -ms-overflow-style: -ms-autohiding-scrollbar;
  }
}

body {
  -moz-osx-font-smoothing: grayscale;
  -ms-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  -webkit-text-size-adjust: 100%;
  margin: 0;
  padding: 0;
}
```

## Browser Queries
If you need to add some browser specific styles, encapsulate them in the following mixins:
```
@mixin browser($browser) {
  @if $browser == 'firefox' {
    @-moz-document url-prefix() {
      @content;
    }
  }

  @if $browser == 'ie-10-11' {
    @media screen and (-ms-high-contrast: active), (-ms-high-contrast: none) {
      @content;
    }
  }
}
```

### Usage:
```
@include mq(firefox) {
  Your firefox-only styles here
}
```

##Colors
This controls all of the colors used within the project
```
$my-site-colors: (
  c-dk-brown: #3f2b1e,
  c-lt-brown: #94856b,
  c-dk-tan: #d9cca7,
  c-tan: #fcf9f3,
  c-red: #d73a15,
  c-green: #7ea042
);

$default-site-colors: (
  c-white: #fff,
  c-black: #000,
  c-dk-gray: #b6b6b6,
  c-lt-gray: #c2c2c2
);
```

### Usage

- `.bgc-dk-brown` - Background color dark brown
- `.bc-lt-brown` - Border color light brown
- `.tc-red` - Text color red

```
<div class=”bgc-dk-brown”>
  <p class=”tc-white”>
Background color of this container will be 
dark brown and this text will be white.
  </p>
</div>
```

## Box Shadows
`.box-shadow` - 0 .1rem .2rem 0 rgba(121, 121, 121, 0.5)

## Grid
Grid classes are closely linked to design based grids, and are platform specific. The pattern for grid classes is:

### Grid Alignment Classes:
These are additional classes that can be added to the grid container, or a child cell container. All the classes can also be isolated for tablet and desktop by adding @tablet or @desktop to the end of the following class names.

#### Direction
Row .fd-r or .fd-r@tablet or .fd-r@destkop 
Row reverse .fd-rr[@tablet, @desktop]
Column .fd-c
Column Reverse .fd-cr

#### Wrap
No wrap .fw-nw
Wrap .fw-w
Wrap reverse .fw-wr

#### Justify Content
Center .jc-c
Flex Start .jc-fs
Flex End .jc-fe
Space Between .jc-sb
Space Around .jc-sa
Space Evenly .jc-sa

#### Align Content
Flex start .ac-fs
Flex end .ac-fe
Center .ac-c
Stretch .ac-s
Space Between .ac-sb
Space Around .ac-sa

#### Align Items
Flex start .ai-fs
Flex end .ai-fe
Center .ai-c
Stretch .ai-s
Baseline .ai-b
Align Self (for child cells)
Auto .as-a
Flex start .as-fs
Flex end .as-fe
Center .as-c
Baseline .as-b
Stretch  .as-s

````
<div class=”grid gw-nw gw-w@tablet”>
  // will be set to grid-wrap: no-wrap on mobile and 
  // grid-wrap: wrap on tablet
  <div class=”cell-full cell-1/2@tablet cell-1/4@desktop”>
    This container on mobile is full width
    This container on tablet is 50% the width of the container
    This container on desktop is 25% the width of the container
  </div>
  <div class=”cell-full cell-1/2@tablet cell-1/4@desktop”></div>
  <div class=”cell-full cell-1/2@tablet cell-1/4@desktop”></div>
  <div class=”cell-full cell-1/2@tablet cell-1/4@desktop”></div>
</div>
````

#### Grid Gotchas

##### Images
Images should not be direct children of grid items. They should be wrapped in another div.

_Bad_
```
<div class=”grid gw-nw gw-w@tablet”>
  <div class=”cell-full cell-1/2@tablet cell-1/4@desktop”>
    <img src=”pic.jpg” alt=”” >
  </div>
</div>
```

_Good_:
```
<div class=”grid gw-nw gw-w@tablet”>
  <div class=”cell-full cell-1/2@tablet cell-1/4@desktop”>
    <div class=”cell-image”><img src=”pic.jpg” alt=”” ></div>
  </div>
</div>
```

#### Auto Width Cells

If you want a cell to fill the remaining width of a container, you can remove the cell class altogether. 

```
<div class=”grid gw-nw gw-w@tablet”>
  <div class=”cell-full cell-1/2@tablet cell-1/4@desktop”>
    <img src=”pic.jpg” alt=”” >
  </div>
  <div class=”cell-full cell-auto@tablet ml-md@tablet”>
    Will be set to auto width at the tablet breakpoint and a left margin of 16px.
    See spacing section below
  </div>
</div>
```

## Spacing
Spacing and borders loop over the following regions that represent the box model. 
```
$box-regions: (
  t: 'top',
  r: 'right',
  b: 'bottom',
  l: 'left',
  v: 'vertical',
  h: 'horizontal'
);
```

Vertical represents both left and right
Horizontal represents both top and bottom.

Spacing classes are used for margins and padding. They are scalable according to region (top, right, bottom, left, horizontal, and vertical), styles (solid, dashed, etc), widths (at your discretion), platforms (mobile-first, tablet, and desktop):

`.m<direction>-<size><\@platform>`

Example 1:  `.mh-md@desktop`

The above  would add a left and right margin of 8px to a container.

Example 2:  `.bv-d-sm@tablet`

The above would create a 1px dashed, top and bottom border that only displays on tablet.

```
$default-padding: (
 sm: rem(4px),
 md: rem(8px),
 lg: rem(16px)
);
```
<div class=”grid gw-nw gw-w@tablet”>
  <div class=”cell-1/3 cell-1/2@tablet cell-1/3@desktop”></div>
  <div class=”cell-auto ml-md ml-lg@tablet ml-x-lg@desktop”>
    Margin left 8px on mobile
    Margin left 16px on tablet
    Margin left 24px on desktop
  </div>
</div>

## Borders and Outlines
Spacing and borders loop over the following regions that represent the box model. 
```
$box-regions: (
  t: 'top',
  r: 'right',
  b: 'bottom',
  l: 'left',
  v: 'vertical',
  h: 'horizontal'
);
```

Border classes are scalable according to region (top, right, bottom, left, horizontal, and vertical), styles (solid, dashed, etc), widths (at your discretion), platforms (mobile-first, tablet, and desktop):

.b<region>-<styles>-<widths><\@platform>

Example 1:  `.bh-s-sm@desktop`

The above  would create a 1px solid, left and right border that only displays on desktop.

Example 2:  `.bv-d-sm@tablet`

The above would create a 1px (sm) dashed(d), top and bottom (v) border that only displays on tablet.
```
$default-border-styles: (
 s: 'solid'
);

$default-border-widths: (
 sm: rem(1px)
);
```

## Border and Outline colors
Border colors are pulled from the color map above.
```
.bc-dk-brown {
 // border-color light
 border-color: #e1d8bf !important;
}

.olc-dk-brown {
 // border-color light
 outline-color: #e1d8bf !important;
}
```

To remove borders that have been set on mobile:
`.b-n@tablet` or `.b-n@desktop`

## Buttons
Buttons are created to automatically select the appropriate hover state colors and text colors. Pretty rad, right? All you need to do is create a button styles, and add a background color. 

- `.btn` - button class is required for all buttons
- `.btn-block` - set button to 100% of its container


### Button heights
```
$default-button-heights: (
  md: 4rem
);
```

.btn-h-md - button height 4rem;

## Form Elements
<input type=”text” class=”ih-sm”>
Input height, small.

## Typography
- `.ts-sm` - Text size small
- `.t-alt` - Text alt style
- `.tc-dk-brown` - Text color dark brown
- `.lh-lg` - Line height large

## Positioning
```
$default-positions: (
  t: 'top',
  r: 'right',
  b: 'bottom',
  l: 'left'
);
```

- `.pos-abs` - absolute
- `.pos-rel` - relative
- `.pos-b` - bottom
- `.pos-l -left
- `.pos-r` - right
- `.pos-t` - top
- `.pos-f` - fixed
- `.pos-v-c` - vertically centered
- `.pos-h-c` - horizontally centered
- `.pos-h-v-c` - horizontally and vertically centered

```
<div class=”pos-rel”>
  <div class=”pos-b pos-r”>
    This element is positioned at the bottom right of the parent element
  </div>
</div>
```

Positioning can be combined with margins to get a little more control.
```
<div class=”pos-rel”>
  <div class=”pos-b pos-r mb-md mr-md”>
    This element is positioned at the bottom right of the parent element
     It is also 16px to the right and bottom. 
  </div>
</div>
```

## Visibility Classes
- `.mobile-only`
- `.not-mobile`
- `.tablet-only`
- `.desktop-only`
- `.visuallyhidden`
- `.hidden`
- `[aria-hidden]`
- `[aria-hidden="false"]`

## Themes
Need more padding, border and button styles? No worries. Add your style to these maps:
```
$my-bg-colors: (

);
$my-breakpoints: (
  // Be careful here. This can create a lot of unnecessary breakpoint 
  // configurations. Add only the breakpoints you need.
);

$my-button-colors: (
  // Be careful here. This can create a lot of unnecessary button color 
  // options. Add only the colors you need.
  // Example:
  // active: #3b3b3b //returns: .button-active
  // secondary: #efefef //returns: .button-secondary
);

$my-padding: (
  // Be careful here. This can create a lot of unnecessary button color 
  // options. Add only the colors you need.
  xx-lg: 3.2rem //returns: .p-xx-lg<@breakpoint>
);

$my-border-styles: (
  // Be careful here. This can create a lot of unnecessary border styles. Use
  // only the styles you need. Also, consider manually adding a border style 
  // if you only plan to use it in a single location
  // Example
  //d: 'dashed' //returns: .bd-<width><@breakpoint>
);
$my-border-widths: (
  // Be careful here. This can create a lot of unnecessary border widths. Use
  // Only the widths you need. Also, consider manually adding a border width 
  // if you only plan to use it in a single location
  // Example:
  // md: .2rem, //returns: .bs-md<@breakpoint> (border solid 2px wide)
  // lg: .4rem //returns: .bd-lg<@breakpoint> (border dashed 4px wide)
);
```