<a name="line-undefined"></a>
File `bxr_color.h`.

Copyright (c) 2025 nsix. All rights reserved.

# Color Utilities

<a name="line-undefined"></a>
## Typedefs

<a name="line-undefined"></a>

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


<a name="line-undefined"></a>
## Macros

<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_WHITE (bxr_color_t){ .r = 255, .g = 255, .b = 255, .a = 255 }
```

White

---


<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_BLACK (bxr_color_t){ .r = 0, .g = 0, .b = 0, .a = 255 }
```

Black

---


<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_RED (bxr_color_t){ .r = 255, .g = 0, .b = 0, .a = 255 }
```

Red

---


<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_GREEN (bxr_color_t){ .r = 0, .g = 255, .b = 0, .a = 255 }
```

Green

---


<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_BLUE (bxr_color_t){ .r = 0, .g = 0, .b = 255, .a = 255 }
```

Blue

---


<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_MAGENTA (bxr_color_t){ .r = 255, .g = 0, .b = 255, .a = 255 }
```

Magenta

---


<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_CYAN (bxr_color_t){ .r = 0, .g = 255, .b = 255, .a = 255 }
```

Cyan

---


<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_YELLOW (bxr_color_t){ .r = 255, .g = 255, .b = 0, .a = 255 }
```

Yellow

---


<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_TRANSPARENT (bxr_color_t){ .r = 0, .g = 0, .b = 0, .a = 0 }
```

Transparent

---


<a name="line-undefined"></a>

```cpp
#define bxr_color_create(r, g, b, a) ((const bxr_color_t){ r, g, b, a })
```

Build a color from its channels.

`r` red channel, from 0 to 255.

`g` green channel, from 0 to 255.

`b` blue channel, from 0 to 255.

`a` alpha channel, from 0 (transparent) to 255 (opaque).

`return` a `bxr_color_t` compound literal, by value.

---

