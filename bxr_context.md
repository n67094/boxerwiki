<a name="line-1"></a>
# Global Context

Access to the window and GPU device owned by the engine: window and virtual
resolution size, fullscreen and resizable state, and the frame counter.

<a name="line-20"></a>
## API

<a name="line-24"></a>

```cpp
BXR_API SDL_GPUDevice *bxr_context_get_gpu_device(void)
```

Get the GPU device used for rendering.

`return` the GPU device, or `NULL` if not created yet.

**Note**: the device is owned by the engine, the caller must not destroy it.

---


<a name="line-33"></a>

```cpp
BXR_API SDL_Window *bxr_context_get_window(void)
```

Get the game window.

`return` the window, or `NULL` if not created yet.

**Note**: the window is owned by the engine, the caller must not destroy it.

---


<a name="line-42"></a>

```cpp
BXR_API bool bxr_context_set_window_dimensions(int width, int height)
```

Resize the window and store the new size in the configuration.

`width` new width in window coordinates.

`height` new height in window coordinates.

return `true` if the window was resized successfully, `false` otherwise.

Call `bxr_get_error()` for more information.

---


<a name="line-55"></a>

```cpp
BXR_API bxr_vec2_t bxr_context_get_window_dimensions(void)
```

Get the window size stored in the configuration.

`return` the size in window coordinates (x = width, y = height).

---


<a name="line-62"></a>

```cpp
BXR_API void bxr_context_set_virtual_window_dimensions(int width, int height)
```

Set the virtual resolution the game renders at.

Takes effect on the next frame, the window itself is not resized.

`width` virtual width in pixels.

`height` virtual height in pixels.

---


<a name="line-73"></a>

```cpp
BXR_API bxr_vec2_t bxr_context_get_virtual_window_dimensions(void)
```

Get the virtual resolution the game renders at.

`return` the virtual size in pixels (x = width, y = height).

---


<a name="line-80"></a>

```cpp
BXR_API bool bxr_context_set_fullscreen(bool fullscreen)
```

Switch the window between fullscreen and windowed mode.

`fullscreen` `true` for fullscreen, `false` for windowed.

`return` true on success, false on failure.

Call `bxr_get_error()` for more information.

---


<a name="line-91"></a>

```cpp
BXR_API bool bxr_context_is_fullscreen(void)
```

Check whether the window is in fullscreen mode.

`return` true if fullscreen, `false` otherwise.

---


<a name="line-98"></a>

```cpp
BXR_API bool bxr_context_set_resizable(bool resizable)
```

Allow or forbid the user to resize the window.

`resizable` `true` to allow resizing, `false` to forbid it.

`return` true on success, false on failure.

Call `bxr_get_error()` for more information.

---


<a name="line-109"></a>

```cpp
BXR_API bool bxr_context_is_resizable(void)
```

Check whether the window can be resized.

`return` true if the window is resizable, `false` otherwise.

---


<a name="line-116"></a>

```cpp
BXR_API Uint64 bxr_context_get_frame_count(void)
```

Get the number of frames rendered since the application started.

`return` the frame count.

---

