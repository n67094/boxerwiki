<a name="line-undefined"></a>
File `bxr_color.h`.

Copyright (c) 2025 nsix. All rights reserved.

# Color Utilities

<a name="line-undefined"></a>

```cpp
typedef struct bxr_color_s
```

RGBA color with 8 bits per channel, from 0 to 255.

`a` is the opacity: 0 is fully transparent, 255 is fully opaque.
---


<a name="line-undefined"></a>

```cpp
#define BXR_COLOR_WHITE (bxr_color_t){ .r = 255, .g = 255, .b = 255, .a = 255 }
```

Predefined opaque colors, plus `BXR_COLOR_TRANSPARENT`.
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

