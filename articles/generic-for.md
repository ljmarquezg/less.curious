### Deprecated. Use [`less-plugin-lists`](https://github.com/seven-phases-max/less-plugin-lists#features) instead.

---

## Generic `for` Structure in [Less](http://lesscss.org/) Using Mixins

### Basic usage
Less code:
<pre lang="less"><code>@import <a href="../src/for.less">"for"</a>;

#basic-usage {
    .for(6); .-each(@i) {
        i: @i;
    }
}
</code></pre>

CSS output:
```css
basic-usage {
  i: 1;
  i: 2;
  i: 3;
  i: 4;
  i: 5;
  i: 6;
}
```
### More real-world example
Less code:
```less
@grid-columns: 5;

.column {
    .for(@grid-columns); .-each(@i) {
        &-@{i} {width: (@i / @grid-columns * 100%)}
    }
}
```
CSS output:
```css
.column-1 {
  width: 20%;
}
.column-2 {
  width: 40%;
}
.column-3 {
  width: 60%;
}
.column-4 {
  width: 80%;
}
.column-5 {
  width: 100%;
}
```
More examples
---------------------

### Nested loops:
```less
#nested-loops {
    .for(3, 1); .-each(@i) {
        .for(0, 2); .-each(@j) {
            x: (10 * @i + @j);
        }
    }
}
```
output:
```css
#nested-loops {
  x: 30;
  x: 31;
  x: 32;
  x: 20;
  x: 21;
  x: 22;
  x: 10;
  x: 11;
  x: 12;
}
```
### Multiple loops in same scope:
```less
#multiple-loops {
    & {.for(1, 3); .-each(@i) {x: @i}}
    & {.for(4, 6); .-each(@i) {y: @i}}
}
```
output (Less 1.6.2 and higher):
```css
#multiple-loops {
  x: 1;
  x: 2;
  x: 3;
  y: 4;
  y: 5;
  y: 6;
}
```
### Multiple loops in same scope (Alt.):
```less
#multiple-loops-alt {
    .-() {.for(1, 3); .-each(@i) {x: @i}}
    .-() {.for(4, 6); .-each(@i) {y: @i}}
    .-();
}
```
output:
```css
#multiple-loops-alt {
  x: 1;
  x: 2;
  x: 3;
  y: 4;
  y: 5;
  y: 6;
}
```
