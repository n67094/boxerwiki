<a name="line-undefined"></a>
File `bxr_time.h`.

# Boxer's Time Utilities.

Copyright (c) 2026 nsix. All rights reserved.

<a name="line-undefined"></a>
Get the time elapsed since SDL was initialized.

`return` the number of milliseconds since SDL library initialization.

```cpp
BXR_INLINE Uint64
```

---


<a name="line-undefined"></a>
Call a callback function after a delay, repeatedly if it asks to.

Callback signature:

```c
Uint32 callback(void *udata, bxr_timer_t timer_id, Uint32 interval);
```

The callback returns the delay in milliseconds before its next run, or 0 to
stop the timer. It runs on a separate thread, so it must be thread-safe.

`interval_ms` the delay before the first call, in milliseconds; also passed
to `callback` as `interval`.
`callback` the function to call when the delay has elapsed, must not be NULL.
`udata` a pointer passed to `callback`, may be NULL.

`return` the timer ID on success, or 0 on failure.

**Note**: remove the timer with `bxr_time_remove_timer()` if it does not
stop itself.

```cpp
BXR_INLINE bxr_timer_t
```

---


<a name="line-undefined"></a>
Remove a timer created with `bxr_time_add_timer()`.

`timer_id` the ID of the timer to remove.

```cpp
BXR_INLINE bool
```

---


<a name="line-undefined"></a>
Block the calling thread for at least the given duration.

`ms` the number of milliseconds to wait.

```cpp
BXR_INLINE void
```

---

