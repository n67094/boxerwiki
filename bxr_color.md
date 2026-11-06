<a name="line-1"></a>
File `bxr_color.h`.

Copyright (c) 2025 - 2026 nsix. All rights reserved.

# Color Utilities

RGBA color type (`bxr_color_t`), a set of predefined colors
(`BXR_COLOR_WHITE`, `BXR_COLOR_BLACK`, ...) and `bxr_color_create()` to build
your own.

<a name="line-18"></a>
## Typedefs

<a name="line-22"></a>

```cpp
typedef struct bxr_color_s
{
  Uint8 r;
  Uint8 g;
  Uint8 b;
  Uint8 a;
} bxr_color_t
```

RGBA color with 8 bits per channel, from 0 to 255.

`a` is the opacity: 0 is fully transparent, 255 is fully opaque.

---


<a name="line-35"></a>
## Macros

<a name="line-39"></a>

```cpp
#define BXR_COLOR_WHITE
#define BXR_COLOR_BLACK
#define BXR_COLOR_RED
#define BXR_COLOR_GREEN
#define BXR_COLOR_BLUE
#define BXR_COLOR_MAGENTA
#define BXR_COLOR_CYAN
#define BXR_COLOR_YELLOW
#define BXR_COLOR_TRANSPARENT
```


---


<a name="line-50"></a>

```cpp
#define bxr_color_create(r, g, b, a)
```

Build a color from its channels.

`r` red channel, from 0 to 255.

`g` green channel, from 0 to 255.

`b` blue channel, from 0 to 255.

`a` alpha channel, from 0 (transparent) to 255 (opaque).

`return` a `bxr_color_t` compound literal, by value.

---

