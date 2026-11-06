<a name="line-1"></a>
File `bxr_log.h`.

Copyright (c) 2025 - 2026 nsix. All rights reserved.

# Logging Utilities

The default minimum priority is `BXR_LOG_PRIORITY_DEBUG`, so every level is
shown until `bxr_log_set_priority()` is called.

Typical usage:

```cpp
bxr_log_enable_colors(true); // optional ANSI terminal colors
bxr_log_set_priority(BXR_LOG_PRIORITY_INFO);

BXR_LOG_INFO("Hello, %s!", "world");
BXR_LOG_ERROR("Something went wrong: %s", bxr_get_error());
```

<a name="line-29"></a>
## Enums

<a name="line-33"></a>

```cpp
typedef enum
{
  BXR_LOG_PRIORITY_DEBUG = 0,
  BXR_LOG_PRIORITY_INFO,
  BXR_LOG_PRIORITY_WARN,
  BXR_LOG_PRIORITY_ERROR,
  BXR_LOG_PRIORITY_SIZE
} bxr_log_priority_e
```


---


<a name="line-43"></a>
## API

<a name="line-47"></a>

```cpp
BXR_API void bxr_log(bxr_log_priority_e priority, const char *fmt, ...)
```

Log a printf-style message at the given priority.

`priority` level of the message, in `[0, BXR_LOG_PRIORITY_SIZE)`.

`fmt` printf-style format string, followed by its arguments; must not be
NULL.

---


<a name="line-57"></a>

```cpp
BXR_API void bxr_log_set_priority(bxr_log_priority_e priority)
```

Set the minimum priority; less severe messages are dropped.

Severity  order: DEBUG < INFO < WARN < ERROR.

`priority` minimum level, in `[0, BXR_LOG_PRIORITY_SIZE)`.

---


<a name="line-66"></a>

```cpp
BXR_API void bxr_log_enable_colors(bool enabled)
```

Enable or disable ANSI terminal colors for log messages.

`enabled` true to enable colors, false to disable.

---


<a name="line-73"></a>

```cpp
#define BXR_LOG_ERROR(...)
```

Log a printf-style message at `BXR_LOG_PRIORITY_ERROR`.

`...` printf-style format string followed by its arguments.

---


<a name="line-80"></a>

```cpp
#define BXR_LOG_WARN(...)
```

Log a printf-style message at `BXR_LOG_PRIORITY_WARN`.

`...` printf-style format string followed by its arguments.

---


<a name="line-87"></a>

```cpp
#define BXR_LOG_DEBUG(...)
```

Log a printf-style message at `BXR_LOG_PRIORITY_DEBUG`.

`...` printf-style format string followed by its arguments.

---


<a name="line-94"></a>

```cpp
#define BXR_LOG_INFO(...)
```

Log a printf-style message at `BXR_LOG_PRIORITY_INFO`.

`...` printf-style format string followed by its arguments.

---

