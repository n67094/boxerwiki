<a name="line-undefined"></a>
File `bxr_defs.h`.

Copyright (c) 2026 nsix. All rights reserved.

# Global Definitions and Constants

<a name="line-undefined"></a>

```cpp
#if defined(_WIN32)
```

Marks a public function for export from (or import into) the boxer library.

On Windows it expands to `__declspec(dllexport)` when `BOXER_BUILD` is
defined (building boxer) and `__declspec(dllimport)` otherwise. Elsewhere it
expands to `extern`.
---


<a name="line-undefined"></a>

```cpp
#define BXR_DEFAULT(val, def) (((val) == 0) ? (def) : (val))
```

Returns `def` if `val` is 0, otherwise returns `val`.
---


<a name="line-undefined"></a>

```cpp
#define BXR_OFFSET_OF(TYPE, ELEMENT) SDL_offsetof(TYPE, ELEMENT)
```

Returns the offset of `ELEMENT` in `TYPE`, in bytes.
---


<a name="line-undefined"></a>

```cpp
#define BXR_ARRAY_SIZE(arr) (sizeof(arr) / sizeof((arr)[0]))
```

Returns the number of elements in an array. Must not be a pointer.
---


<a name="line-undefined"></a>

```cpp
#define BXR_TERM_ESC "\x1B"
```

ANSI terminal escape sequences, as string literals to concatenate with
other literals. Always end colored output with `BXR_TERM_RESET`.
---

