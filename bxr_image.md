<a name="line-1"></a>
File `bxr_image.h`.

Copyright (c) 2025 - 2026 nsix. All rights reserved.

# Image

Images are handles (`bxr_image_t`) created from asset files mounted with the
`bxr_asset.h` API or from raw pixels in memory, and released with
`bxr_image_destroy()`. A handle whose `id` is `BXR_IMAGE_INVALID_ID` is
invalid.

Typical usage:

```cpp
_img = bxr_image_create("title/background.png");
if (!bxr_image_is_valid(_img)) {
  BXR_LOG_ERROR("%s", bxr_get_error());
}

int w = bxr_image_get_width(_img);
int h = bxr_image_get_height(_img);

...

bxr_image_destroy(_img);
```

<a name="line-38"></a>

```cpp
#define BXR_IMAGE_INVALID_ID 0
```


---


<a name="line-41"></a>
## Typedefs

<a name="line-45"></a>

```cpp
typedef struct bxr_image_s
{
  Uint32 id;
} bxr_image_t
```

Handle to an image.

---


<a name="line-53"></a>
## API

<a name="line-57"></a>

```cpp
BXR_API bxr_image_t bxr_image_create(const char *path)
```

Load a PNG image from a mounted asset file.

The pixels are converted to the swapchain format and uploaded to the GPU.

`path` path of the file, relative to the mounted directories. Must not be
`NULL` and must end with `.png` or `.bmp`.

`return` the image, or an image with id `BXR_IMAGE_INVALID_ID` on failure.

Call `bxr_get_error()` for more information.

**Note**: the caller must destroy the result with `bxr_image_destroy()`.

---


<a name="line-73"></a>

```cpp
BXR_API bxr_image_t bxr_image_create_mem(int width, int height, bxr_pixel_format_e format, void *pixels, int pitch)
```

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

---


<a name="line-100"></a>

```cpp
BXR_API int bxr_image_get_width(bxr_image_t image)
```

Get the width of an image.

`image` image to query.

`return` the width in pixels, or 0 if the image id is `BXR_IMAGE_INVALID_ID`.

---


<a name="line-109"></a>

```cpp
BXR_API int bxr_image_get_height(bxr_image_t image)
```

Get the height of an image.

`image` image to query.

`return` the height in pixels, or 0 if the image id is
`BXR_IMAGE_INVALID_ID`.

---


<a name="line-119"></a>

```cpp
BXR_API bool bxr_image_is_valid(bxr_image_t image)
```

Check if an image handle is valid.

`image` image to check.

`return` true if the image id is not `BXR_IMAGE_INVALID_ID`, false otherwise.

---


<a name="line-128"></a>

```cpp
BXR_API void bxr_image_destroy(bxr_image_t image)
```

Destroy an image and release its GPU texture.

`image` image to destroy.

---

