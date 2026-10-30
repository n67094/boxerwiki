<a name="line-undefined"></a>
File `bxr_game.h`.

# Boxer's Game Lifecycle.

Copyright (c) 2026 nsix. All rights reserved.

<a name="line-undefined"></a>
Boxer configuration.

`name` application name, also used to build the save directory
(e.g. `~/.local/share/<name>/` on Linux). Must not be `NULL` and must stay
valid until exit since only the pointer is kept (e.g. a string literal).

`title` window title. Must not be `NULL` and must stay valid until exit
(e.g. a string literal).

`width` and `height` initial window size in window coordinates, > 0.

`virtual_width` and `virtual_height` resolution the game draws in, > 0 and
not larger than `width` and `height`.

`fullscreen` create the window in fullscreen mode.

`resizable` allow the user to resize the window.

```cpp
typedef struct bxr_game_config_s
```

---


<a name="line-undefined"></a>
Provide the game configuration, implemented by the user.

Called once at startup, before SDL and any subsystem are initialized, so it
must not call any boxer function.

`return` the configuration, must not be `NULL`. Its fields are copied right
after the call, so a `static` variable is enough and nothing is freed.

```cpp
extern const bxr_game_config_t *bxr_game_config(void)
```

---


<a name="line-undefined"></a>
Initialize the game state, implemented by the user.

Called once after every boxer subsystem are ready, so assets, audio and input
can be used here.

```cpp
extern void bxr_game_setup(void)
```

---


<a name="line-undefined"></a>
Advance the game logic by one fixed step, implemented by the user.

Called zero or more times per frame, at a fixed rate matching the display
refresh rate (60 Hz if it can't be queried). When the game falls behind,
at most 5 steps are caught up and the remaining lag is dropped.

`delta_ms` duration of the fixed step in milliseconds (e.g. 16.67 at
60 Hz), the same value on every call until the refresh rate changes.

**NOTE:** Input state is refreshed before each step.

```cpp
extern void bxr_game_update(double delta_ms)
```

---


<a name="line-undefined"></a>
Draw the current game state, implemented by the user.

Called once per frame after the updates. Drawing
coordinates are in the virtual resolution from the configuration.

`alpha_ms` how far the current time is between the last update and the next
one, in [0, 1), used to interpolate between the previous and current update
state for smooth rendering.

```cpp
extern void bxr_game_render(double alpha_ms)
```

---


<a name="line-undefined"></a>
Release the game resources, implemented by the user.

Called once on exit, before boxer subsystems are torn down, so they are
still usable here.

**NOTE:** this is also called when engine startup failed, possibly before
`bxr_game_setup()` ran, so it must handle a partially or not initialized
state.

```cpp
extern void bxr_game_teardown(void)
```

---

