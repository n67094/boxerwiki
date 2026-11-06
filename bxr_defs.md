<a name="line-1"></a>
# Global Definitions

Export and inline macros, and small helper macros (`BXR_ARRAY_SIZE()`,
`BXR_DEFAULT()`, terminal escape codes, ...) shared by every boxer header.

<a name="line-37"></a>

```cpp
#define BXR_DEFAULT(val, def)
```

Returns `def` if `val` is 0, otherwise returns `val`.

---


<a name="line-42"></a>

```cpp
#define BXR_OFFSET_OF(TYPE, ELEMENT)
```

Returns the offset of `ELEMENT` in `TYPE`, in bytes.

---


<a name="line-47"></a>

```cpp
#define BXR_ARRAY_SIZE(arr)
```

Returns the number of elements in an array. Must not be a pointer.

---


<a name="line-52"></a>

```cpp
#define BXR_TERM_ESC
#define BXR_TERM_RESET
#define BXR_TERM_BOLD
#define BXR_TERM_COLOR_CYAN
#define BXR_TERM_COLOR_GREEN
#define BXR_TERM_COLOR_YELLOW
#define BXR_TERM_COLOR_RED
```

ANSI terminal escape sequences, as string literals to concatenate with
other literals. Always end colored output with `BXR_TERM_RESET`.

---

