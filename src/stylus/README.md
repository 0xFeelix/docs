---
sidebar: auto
---

# Stylus cheatsheet

## Main

### CSS syntax

```css
.box {
  color: blue;

  .button {
    color: red;
  }
}
```

Stylus is a CSS pre-processor.

---

### Indent syntax

```stylus
.box
  color: blue

  .button
    color: red
```

Also works! The colon is optional, as well. This is typically the syntax used with Stylus documents.

## Mixins

### Without arguments

```stylus
red-border()
  border: solid 2px red

//------------------//

div
  red-border()
```

---

### With arguments

```stylus
border-radius(n)
  -webkit-border-radius: n
  border-radius: n

//------------------//

div
  border-radius: 2px
  border-radius(2px)
```

Mixins can be applied in two different ways.

---

### Argument defaults

```stylus
border-radius(n = 2px)
  -webkit-border-radius: n
```

---

### Block mixins

```stylus
mobile()
  @media (max-width: 480px)
    {block}

//------------------//

+mobile()
  width: 10px
```

---

### Rest params

```stylus
shadow(offset-x, args...)
  box-shadow: offset-x args
  margin-top: offset-x

//------------------//

#login
  shadow: 1px 2px 5px #eee
```

## Functions

### Functions

```stylus
add(a, b)
  a + b

//------------------//

body
  padding: add(10px, 5)
```

---

### Arguments defaults

```stylus
add(a, b = 2)
  a + b
```

---

### Named parameters

```stylus
shadow(x, y)
  x y (y * 1.5) #000

//------------------//

.button
  box-shadow: shadow(x: 2, y: 4)
```

---

### Multiple return values

```stylus
sizes()
  8px 16px

//------------------//

sizes()[0]  // → 8px
sizes()[1]  // → 16px
```

## Values

### Conditional assigment

```stylus
royal-blue = #36a
royal-blue ?= #89f

//------------------//

div
  color: royal-blue  // #36a
```
?= will only set a variable if it’s previously unset.

---

### Property lookup 

```stylus
.logo
  width: w = 150
  margin-left: -(w / 2)
  // or
  height: 80px
  margin-top: -(@height / 2)
```

---

### Interpolation

```stylus
-{prefix}-border-radius: 2px
```

---

### Color operators

```stylus
#888 + 50%    // → #c3c3c3 (lighten)
#888 - 50%    // → #444 (darken)
#f00 + 50deg  // → #ffd500 (hue)
```

---

### Lookup 

```stylus
light-blue = #3bd
name = 'blue'
lookup('light-' + name)
```

---

### Casting

```stylus
n = 5px

foo: (n)em
foo: (n * 5)%
```

## Advanced features

### Conditional

```stylus
if color == blue
  display: block
else if true and true
  display: inline
else if 'hey' is not 'bye'
  display: flex
else
  display: none

//------------------//

Aliases:

==	   is
!=	   is not
!=	   isnt
```

---

### For loops

```stylus
n = 5px

foo: (n)em
foo: (n * 5)%
```

---

### Definition check

```stylus
if ohnoes is defined
  color: blue
```

---

### False values

```stylus
0
null
false
''
```

---

### Type check

```stylus
if val is a 'string'
if val is a 'ident'
if #fff is a 'rgba'    // → true
```


## Built-in functions

### Color functions

``` stylus
alpha(#fff)   //→ 1
alpha(rgba(0, 0, 0, 0.2))   //→ 0.2

dark(black)  //→ true
light(black) //→ false

hue(#0a0)         //→ 50deg
saturation(#f00)  //→ 100%
lightness(#f00)   //→ 50%
luminosity(#f00)  //→ 0.2126

hue(#0a0, 0deg)
saturation(#f00, 50%)
lightness(#f00)

lighten(color, 10%)
darken(color, 10%)
saturate(color, 10%)
desaturate(color, 10%)
invert(color)

tint(color, 50%)  // mix with white
shade(color, 50%) // mix with black

unquote(string)
```

---

### Image size

``` stylus
width:  image-size('tux.png')[0]
height: image-size('tux.png')[1]
```

---

### Caching

``` stylus
size($width)
  +cache('w' + $width)
    width: $width
.a { size: 10px }
.b { size: 10px }


// yields: .a, b { width: 10px }
```

---

### Add property

``` stylus
gradient(color)
  add-property('background-image', linear-gradient(top, color, darken(color, 20%)))
  color

body
  background: gradient(red)
```

---

### Embed URL

``` stylus
background: embedurl('logo.png')
// → background: url("data:image/png;base64,…")
```

---

### sprintf

``` stylus
'-webkit-gradient(%s, %s, %s)' % (linear (0 0) (0 100%))
// → -webkit-gradient(linear, 0 0, 0 100%)

s("rgba(0, 0, 0, %s)", 0.3)

```

---

[<Blog](/blog/)