<a name="line-undefined"></a>
File `bxr_error.h`.

# Boxer's Error Handling.

Copyright (c) 2026 nsix. All rights reserved.

<a name="line-undefined"></a>
## Public API

<a name="line-undefined"></a>
Set the error message.

Messages longer than `BXR_ERROR_MAX_LENGTH - 1` bytes are truncated.

`fmt` printf-style format string, followed by its arguments; must not be
NULL.

`return` always false, so it can be returned directly from a failing
function.

```cpp
BXR_API bool bxr_set_error(SDL_PRINTF_FORMAT_STRING const char *fmt, ...)
```

---


<a name="line-undefined"></a>
Get the last error message.

`return` the message, or an empty string if no error was set. Never NULL.

The string is owned by boxer and stays valid until the next
`bxr_set_error()`.

```cpp
BXR_API const char *bxr_get_error(void)
```

---


<a name="line-undefined"></a>
Clear the error message.

```cpp
BXR_API void bxr_clear_error(void)
```

---

