<a name="line-undefined"></a>
File `bxr_mouse.h`.

Copyright (c) 2026 nsix. All rights reserved.

# Mouse Handling

The mouse position is tracked in the game's virtual resolution, and the mouse
wheel scroll is tracked in the current frame.

<a name="line-undefined"></a>
## Enums

<a name="line-undefined"></a>
Mouse buttons.

```cpp
typedef enum
{
  BXR_MOUSE_UNKNOWN = 0,
  BXR_MOUSE_LEFT    = SDL_BUTTON_LEFT,
  BXR_MOUSE_MIDDLE  = SDL_BUTTON_MIDDLE,
  BXR_MOUSE_RIGHT   = SDL_BUTTON_RIGHT,
  BXR_MOUSE_X1      = SDL_BUTTON_X1,
  BXR_MOUSE_X2      = SDL_BUTTON_X2,
  BXR_MOUSE_SIZE    = 6,
} bxr_mouse_e
```

---


<a name="line-undefined"></a>
## API

<a name="line-undefined"></a>
Get the position of the mouse cursor in the game's virtual resolution.

`return` the cursor position in virtual resolution coordinates.

```cpp
BXR_API bxr_vec2_t bxr_mouse_pos(void)
```

---


<a name="line-undefined"></a>
Get the current position of the mouse cursor in window coordinates.

`return` the cursor position in window coordinates.

```cpp
BXR_API bxr_vec2_t bxr_mouse_window_pos(void)
```

---


<a name="line-undefined"></a>
Get the position of the mouse cursor in the previous frame in the game's
virtual resolution.

`return` the cursor position in virtual resolution coordinates.

```cpp
BXR_API bxr_vec2_t bxr_mouse_prev_pos(void)
```

---


<a name="line-undefined"></a>
Get the position of the mouse cursor in the previous frame in window
coordinates.

`return` the cursor position in window coordinates.

```cpp
BXR_API bxr_vec2_t bxr_mouse_prev_window_pos(void)
```

---


<a name="line-undefined"></a>
Check if a mouse button is currently held down.

`button` button to check, in `[BXR_MOUSE_LEFT, BXR_MOUSE_X2]`.

`return` true if the button is held, false otherwise.

```cpp
BXR_API bool bxr_mouse_held(bxr_mouse_e button)
```

---


<a name="line-undefined"></a>
Check if a mouse button was pressed during the previous frame.

`button` button to check, in `[BXR_MOUSE_LEFT, BXR_MOUSE_X2]`.

`return` true if the button was just pressed, false otherwise.

```cpp
BXR_API bool bxr_mouse_just_pressed(bxr_mouse_e button)
```

---


<a name="line-undefined"></a>
Check if a mouse button was released during the previous frame.

`button` button to check, in `[BXR_MOUSE_LEFT, BXR_MOUSE_X2]`.

`return` true if the button was just released, false otherwise.

```cpp
BXR_API bool bxr_mouse_just_released(bxr_mouse_e button)
```

---


<a name="line-undefined"></a>
Get the number of clicks for a mouse button.

`button` button to check, in `[BXR_MOUSE_LEFT, BXR_MOUSE_X2]`.

`return` the number of clicks for the button.

```cpp
BXR_API Uint8 bxr_mouse_get_clicks(bxr_mouse_e button)
```

---


<a name="line-undefined"></a>
Check if a mouse button was double clicked during the previous frame.

`button` button to check, in `[BXR_MOUSE_LEFT, BXR_MOUSE_X2]`.

`return` true if the button was double clicked, false otherwise.

```cpp
BXR_API bool bxr_mouse_is_double_click(bxr_mouse_e button)
```

---


<a name="line-undefined"></a>
Get how long a mouse button has been held down.

`button` button to check, in `[BXR_MOUSE_LEFT, BXR_MOUSE_X2]`.

`return` the time since the button was pressed in milliseconds, or 0 if it is
not held.

```cpp
BXR_API Uint64 bxr_mouse_held_time(bxr_mouse_e button)
```

---


<a name="line-undefined"></a>
Get the mouse wheel scroll for the current frame.

`return` the scroll amount in the x and y directions.

```cpp
BXR_API bxr_vec2_t bxr_mouse_wheel(void)
```

---


<a name="line-undefined"></a>
Hide or show the mouse cursor.

`hide` true to hide the cursor, false to show it.

```cpp
BXR_API void bxr_mouse_hide(bool hide)
```

---


<a name="line-undefined"></a>
Check if the mouse cursor is currently visible.

`return` true if the cursor is visible, false otherwise.

```cpp
BXR_API bool bxr_mouse_is_visible(void)
```

---

