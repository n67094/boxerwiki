<a name="line-undefined"></a>
File `bxr_image.h`.

Copyright (c) 2026 nsix. All rights reserved.

# Image

Images are handles (`bxr_image_t`) created from asset files mounted with the
`bxr_asset.h` API or from raw pixels in memory, and released with
`bxr_image_destroy()`. A handle whose `id` is `BXR_IMAGE_INVALID_ID` is
invalid.

<a name="line-undefined"></a>
## Typedefs

<a name="line-undefined"></a>
Handle to an image.

```cpp
typedef struct bxr_image_s
{
  Uint32 id;
} bxr_image_t
```

---


<a name="line-undefined"></a>
## API

<a name="line-undefined"></a>
Load a PNG image from a mounted asset file.

The pixels are converted to the swapchain format and uploaded to the GPU.

`path` path of the file, relative to the mounted directories. Must not be
`NULL` and must end with `.png` or `.bmp`.

`return` the image, or an image with id `BXR_IMAGE_INVALID_ID` on failure.

Call `bxr_get_error()` for more information.

**Note**: the caller must destroy the result with `bxr_image_destroy()`.

```cpp
BXR_API bxr_image_t bxr_image_create(const char *path)
```

---


<a name="line-undefined"></a>
Create an image from raw pixels in memory.

The pixels are copied, converted to the swapchain format if needed, and
uploaded to the GPU.

`width` width in pixels.

`height` height in pixels.

`format` pixel format of `pixels` (e.g. `BXR_PIXEL_FORMAT_RGBA32`).

`pixels` pixel data, at least `pitch * height` bytes. Remains owned by the
caller and may be freed once the call returns.

`pitch` bytes per row, or 0 to compute it as `width` times the format's
bytes per pixel.

`return` the image, or an image with id `BXR_IMAGE_INVALID_ID` on failure.

Call `bxr_get_error()` for more information.

**Note**: the caller must destroy the result with `bxr_image_destroy()`.

```cpp
BXR_API bxr_image_t bxr_image_create_mem(
    int width, int height, bxr_pixel_format_e format, void *pixels, int pitch)
```

---


<a name="line-undefined"></a>
Get the width of an image.

`image` image to query.

`return` the width in pixels, or 0 if the image id is `BXR_IMAGE_INVALID_ID`.

```cpp
BXR_API int bxr_image_get_width(bxr_image_t image)
```

---


<a name="line-undefined"></a>
Get the height of an image.

`image` image to query.

`return` the height in pixels, or 0 if the image id is
`BXR_IMAGE_INVALID_ID`.

```cpp
BXR_API int bxr_image_get_height(bxr_image_t image)
```

---


<a name="line-undefined"></a>
Check if an image handle is valid.

`image` image to check.

`return` true if the image id is not `BXR_IMAGE_INVALID_ID`, false otherwise.

```cpp
BXR_API bool bxr_image_is_valid(bxr_image_t image)
```

---


<a name="line-undefined"></a>
Destroy an image and release its GPU texture.

`image` image to destroy.

```cpp
BXR_API void bxr_image_destroy(bxr_image_t image)
```

---

