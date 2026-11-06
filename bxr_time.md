<a name="line-1"></a>
File `bxr_time.h`.

Copyright (c) 2025 - 2026 nsix. All rights reserved.

# Time Utilities

Elapsed time since startup, blocking delays, and timers calling a callback
after a delay.

Typical usage:

```cpp
Uint32 on_tick(void *udata, bxr_timer_t id, Uint32 interval_ms) {
  ...
  return interval_ms; // 0 to stop the timer
}

_timer = bxr_time_add_timer(1000, on_tick, NULL);

...

bxr_time_remove_timer(_timer);
```

<a name="line-34"></a>

```cpp
typedef SDL_TimerID bxr_timer_t
```


---


<a name="line-37"></a>

```cpp
typedef SDL_TimerCallback bxr_timer_cb_t
```


---


<a name="line-40"></a>

```cpp
BXR_INLINE Uint64 bxr_time_get_ticks(void)
```

Get the time elapsed since SDL was initialized.

`return` the number of milliseconds since SDL library initialization.

---


<a name="line-51"></a>

```cpp
BXR_INLINE bxr_timer_t bxr_time_add_timer(Uint32 interval_ms, bxr_timer_cb_t callback, void *udata)
```

Call a callback function after a delay, repeatedly if it asks to.

Callback signature:

```cpp
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

---


<a name="line-81"></a>

```cpp
BXR_INLINE bool bxr_time_remove_timer(bxr_timer_t timer_id)
```

Remove a timer created with `bxr_time_add_timer()`.

`timer_id` the ID of the timer to remove.

---


<a name="line-92"></a>

```cpp
BXR_INLINE void bxr_time_delay(Uint32 ms)
```

Block the calling thread for at least the given duration.

`ms` the number of milliseconds to wait.

---

