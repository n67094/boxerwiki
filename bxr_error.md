<a name="line-1"></a>
File `bxr_error.h`.

Copyright (c) 2025 - 2026 nsix. All rights reserved.

# Error Handling

Failing boxer functions store a message describing the error; read it with
`bxr_get_error()`. Only the last error is kept.

<a name="line-19"></a>
## API

<a name="line-23"></a>

```cpp
BXR_API bool bxr_set_error(SDL_PRINTF_FORMAT_STRING const char *fmt, ...) SDL_PRINTF_VARARG_FUNC(1)
```

Set the error message.

Messages longer than `BXR_ERROR_MAX_LENGTH - 1` bytes are truncated.

`fmt` printf-style format string, followed by its arguments; must not be
NULL.

`return` always false, so it can be returned directly from a failing
function.

---


<a name="line-37"></a>

```cpp
BXR_API const char *bxr_get_error(void)
```

Get the last error message.

`return` the message, or an empty string if no error was set. Never NULL.

The string is owned by boxer and stays valid until the next
`bxr_set_error()`.

---


<a name="line-47"></a>

```cpp
BXR_API void bxr_clear_error(void)
```

Clear the error message.

---

