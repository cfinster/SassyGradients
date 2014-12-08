SassyGradients
==============

Sass helpers to manipulate gradients.

## Instanciate

To instanciate a new [Gradient](https://github.com/HugoGiraudel/SassyGradients/blob/master/TERMINOLOGY.md#gradient), use the exact same syntax as CSS with the `sg-gradient` function.

```scss
$gradient: sg-gradient(to bottom right, red 20%, yellow, green, blue 55%, red 55%, green);
```

## Display

```scss
.selector {
  @include sg-display($gradient);
}
```

```css
.selector {
  background: red;
  background: linear-gradient(to bottom right, red 20%, yellow 31.6666666667%, green 43.3333333333%, blue 55%, red 55%, green 100%);
}
```

As a default, the [fallback](https://github.com/HugoGiraudel/SassyGradients/blob/master/TERMINOLOGY.md#fallback) color is the first color of the [color-stop](https://github.com/HugoGiraudel/SassyGradients/blob/master/TERMINOLOGY.md#color-stop) chain. If you wish to use a custom [color](https://github.com/HugoGiraudel/SassyGradients/blob/master/TERMINOLOGY.md#color), you can pass it as a second parameter to the `sg-display` mixin:

```scss
.selector {
  @include sg-display($gradient, $fallback: blue);
}
```

## Access properties

```scss
$fallback: sg-get($gradient, "fallback");
// red

$direction: sg-get($gradient, "direction");
// to bottom right

$legacy-direction: sg-get($gradient, "legacy-direction");
// top left

$colors: sg-get($gradient, "colors"):
// red, yellow, green, blue, red, green

$color-stops: sg-get($gradient, "color-stops");
// red 20%, yellow 31.6666666667%, green 43.3333333333%, blue 55%, red 55%, green 100%

$authored-color-stops: sg-get($gradient, "authored-color-stops");
// red 20%, yellow, green, blue 55%, red 55%, green

$length: sg-get($gradient, "length");
// 6
```

## Update direction

```scss
$new-gradient: sg-gradient(to bottom, sg-get($gradient, "color-stops"));
```

## Update color-stops

```scss
// Adding a new color-stop
$new-gradient: sg-gradient(sg-get($gradient, "direction"), append(sg-get($gradient, "authored-color-stops"), hotpink, comma)...);

// Brand new color-stops
$new-gradient: sg-gradient(sg-get($gradient, "direction"), yellow, green, blue, purple, magenta);
```

## Debug

```scss
.debug {
  @include gh-debug($gradient);
}
```

```css
@debug-gradient {
  raw: ("fallback": red, "direction": to bottom right, "legacy-direction": top left, "authored-color-stops": (red 20%, yellow, green, blue 55%, red 55%, green), "color-stops": (red 20%, yellow 31.6666666667%, green 43.3333333333%, blue 55%, red 55%, green 100%), "colors": (red, yellow, green, blue, red, green), "length": 6);
  fallback: red;
  direction: to bottom right;
  legacy-direction: top left;
  authored-color-stops: red 20%, yellow, green, blue 55%, red 55%, green;
  color-stops: red 20%, yellow 31.6666666667%, green 43.3333333333%, blue 55%, red 55%, green 100%;
  colors: red, yellow, green, blue, red, green;
  length: 6;
}
```
