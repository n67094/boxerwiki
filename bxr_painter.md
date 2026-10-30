<a name="line-undefined"></a>
File `bxr_painter.h`.

# Boxer's 2D Painter.

Immediate-mode 2D renderer (thin wrapper over SDL_gp).

Public API below may only be called from `bxr_game_update()` or
`bxr_game_render()`.

Default coordinate space: virtual resolution in pixels, origin at the
top-left corner, y pointing down.

Copyright (c) 2026 nsix. All rights reserved.

<a name="line-undefined"></a>
## Public API

<a name="line-undefined"></a>
A vertex with position, texture coordinates and color.

```cpp
typedef struct bxr_vertex_s
```

---


<a name="line-undefined"></a>
A rectangle with a destination region and a source region in the texture.

```cpp
typedef struct bxr_textured_rect_s
```

---


<a name="line-undefined"></a>
Constructs a `bxr_textured_rect_t` compound literal from the `dst`
destination region (in the current coordinate space) and the `src` region
in the texture.

```cpp
#define bxr_textured_rect_create(dst, src)                                     \
```

---


<a name="line-undefined"></a>
Set the coordinate space boundaries mapped onto the current viewport.

`left` and `right` the x coordinates of the left and right edges.
`bottom` and `top` the y coordinates of the bottom and top edges.

```cpp
BXR_API void
```

---


<a name="line-undefined"></a>
Reset the projection to the default coordinate space: viewport pixels,
origin at the top-left corner, y pointing down.

```cpp
BXR_API void bxr_painter_reset_projection(void)
```

---


<a name="line-undefined"></a>
Save the current transform matrix on the transform stack.

Every push must be matched by a `bxr_painter_pop_transform()` in the same
frame.

```cpp
BXR_API void bxr_painter_push_transform(void)
```

---


<a name="line-undefined"></a>
Restore the transform matrix saved by the last
`bxr_painter_push_transform()`.

```cpp
BXR_API void bxr_painter_pop_transform(void)
```

---


<a name="line-undefined"></a>
Reset the current transform matrix to identity.

```cpp
BXR_API void bxr_painter_reset_transform(void)
```

---


<a name="line-undefined"></a>
Translate the coordinate space of subsequent draws.

`x` and `y` the translation along each axis, in current units.

```cpp
BXR_API void bxr_painter_translate(float x, float y)
```

---


<a name="line-undefined"></a>
Rotate the coordinate space of subsequent draws around the origin.

`angle` the angle in radians. Positive is clockwise on screen with the
default y-down projection.

```cpp
BXR_API void bxr_painter_rotate(float angle)
```

---


<a name="line-undefined"></a>
Rotate the coordinate space of subsequent draws around a point.

`angle` the angle in radians. Positive is clockwise on screen with the
default y-down projection.
`ax` and `ay` the pivot, in current coordinates.

```cpp
BXR_API void bxr_painter_rotate_at(float angle, float ax, float ay)
```

---


<a name="line-undefined"></a>
Scale the coordinate space of subsequent draws around the origin.

`sx` and `sy` the scale factors along each axis. Negative values mirror.

```cpp
BXR_API void bxr_painter_scale(float sx, float sy)
```

---


<a name="line-undefined"></a>
Scale the coordinate space of subsequent draws around a point.

`sx` and `sy` the scale factors along each axis. Negative values mirror.
`ax` and `ay` the pivot, in current coordinates.

```cpp
BXR_API void bxr_painter_scale_at(float sx, float sy, float ax, float ay)
```

---


<a name="line-undefined"></a>
Set the pipeline used by subsequent draws.

`pipeline` a pipeline from `bxr_pipeline_create()`; ownership stays with
the caller, who must keep it alive until the frame is flushed.

```cpp
BXR_API void bxr_painter_set_pipeline(bxr_pipeline_t pipeline)
```

---


<a name="line-undefined"></a>
Reset to the builtin pipeline. Also clears the current uniform data.

```cpp
BXR_API void bxr_painter_reset_pipeline(void)
```

---


<a name="line-undefined"></a>
Set uniform data for subsequent draws with the current pipeline.

The data is copied. `vs_size + fs_size` must not exceed
`BXR_PAINTER_MAX_UNIFORM_FLOATS * sizeof(float)` bytes (asserted).

`vs_data` vertex stage data. May be NULL only if `vs_size` is 0.
`vs_size` size of `vs_data` in bytes.
`fs_data` fragment stage data. May be NULL only if `fs_size` is 0.
`fs_size` size of `fs_data` in bytes.

```cpp
BXR_API void bxr_painter_set_uniform(const void *vs_data,
```

---


<a name="line-undefined"></a>
Clear the uniform data (no uniforms).

```cpp
BXR_API void bxr_painter_reset_uniform(void)
```

---


<a name="line-undefined"></a>
Set the blend mode used by subsequent draws.

```cpp
BXR_API void bxr_painter_set_blendmode(bxr_blendmode_e blend_mode)
```

---


<a name="line-undefined"></a>
Reset the current blend mode to the default blend mode (no blending).

```cpp
BXR_API void bxr_painter_reset_blendmode(void)
```

---


<a name="line-undefined"></a>
Set the color used by subsequent draws.

```cpp
BXR_API void bxr_painter_set_color(bxr_color_t color)
```

---


<a name="line-undefined"></a>
Get the current draw color.

`return` the color set by `bxr_painter_set_color()`, white by default.

```cpp
BXR_API bxr_color_t bxr_painter_get_color(void)
```

---


<a name="line-undefined"></a>
Reset current color to the default color (white).

```cpp
BXR_API void bxr_painter_reset_color(void)
```

---


<a name="line-undefined"></a>
Bind an image to a texture channel for subsequent draws.

`channel` the texture channel, in `[0, BXR_PAINTER_MAX_TEXTURE_SLOTS)`.
`image` the image to bind. Ownership stays with the caller.

```cpp
BXR_API void bxr_painter_set_image(int channel, bxr_image_t image)
```

---


<a name="line-undefined"></a>
Unbind the image from a texture channel (no texture).

This is the default for every channel except 0.

`channel` the texture channel, in `[0, BXR_PAINTER_MAX_TEXTURE_SLOTS)`.

```cpp
BXR_API void bxr_painter_unset_image(int channel)
```

---


<a name="line-undefined"></a>
Bind the builtin 1x1 white image to a texture channel.

This is the default for channel 0.

`channel` the texture channel, in `[0, BXR_PAINTER_MAX_TEXTURE_SLOTS)`.

```cpp
BXR_API void bxr_painter_reset_image(int channel)
```

---


<a name="line-undefined"></a>
Bind a sampler to a texture channel for subsequent draws.

`channel` the texture channel, in `[0, BXR_PAINTER_MAX_TEXTURE_SLOTS)`.
`sampler` the sampler to bind. Ownership stays with the caller.

```cpp
BXR_API void bxr_painter_set_sampler(int channel, bxr_sampler_t *sampler)
```

---


<a name="line-undefined"></a>
Unbind the sampler from a texture channel (no sampler).

`channel` the texture channel, in `[0, BXR_PAINTER_MAX_TEXTURE_SLOTS)`.

```cpp
BXR_API void bxr_painter_unset_sampler(int channel)
```

---


<a name="line-undefined"></a>
Bind the builtin nearest sampler to a texture channel (the default).

`channel` the texture channel, in `[0, BXR_PAINTER_MAX_TEXTURE_SLOTS)`.

```cpp
BXR_API void bxr_painter_reset_sampler(int channel)
```

---


<a name="line-undefined"></a>
Restrict subsequent draws to a rectangle.

Coordinates are in virtual-resolution pixels, relative to the viewport, and
ignore the projection and transform.

`x` and `y` the top-left corner.
`w` and `h` the size.

```cpp
BXR_API void bxr_painter_scissor(int x, int y, int w, int h)
```

---


<a name="line-undefined"></a>
Remove the clipping rectangle (draw to the whole frame).

```cpp
BXR_API void bxr_painter_reset_scissor(void)
```

---


<a name="line-undefined"></a>
Reset viewport, scissor, projection, transform, blend mode, color, uniform
and pipeline to their defaults.

```cpp
BXR_API void bxr_painter_reset_state(void)
```

---


<a name="line-undefined"></a>
Fill the whole frame with the current color.

Ignores projection and transform, but honors the scissor and the current
blend mode.

```cpp
BXR_API void bxr_painter_clear(void)
```

---


<a name="line-undefined"></a>
Draw raw vertices as the given primitive.

`primitive_type` how vertices are assembled.
`vertices` the vertex array. Must not be NULL if `vertices_count` > 0.
`vertices_count` number of elements in `vertices`.

```cpp
BXR_API void bxr_painter_draw(bxr_primitive_e primitive_type,
```

---


<a name="line-undefined"></a>
Draw points with the current color.

`points` the point array. Must not be NULL if `count` > 0.
`count` number of points.

```cpp
BXR_API void bxr_painter_draw_points(const bxr_vec2_t *points, Uint32 count)
```

---


<a name="line-undefined"></a>
Draw a single point with the current color.

```cpp
BXR_API void bxr_painter_draw_point(bxr_vec2_t point)
```

---


<a name="line-undefined"></a>
Draw independent line segments with the current color.

`lines` the segment array. Must not be NULL if `count` > 0.
`count` number of segments.

```cpp
BXR_API void bxr_painter_draw_lines(const bxr_line_t *lines, Uint32 count)
```

---


<a name="line-undefined"></a>
Draw a single line segment with the current color.

```cpp
BXR_API void bxr_painter_draw_line(bxr_line_t line)
```

---


<a name="line-undefined"></a>
Draw a polyline joining consecutive points with the current color.

`points` the point array. Must not be NULL if `count` > 0.
`count` number of points

```cpp
BXR_API void bxr_painter_draw_lines_strip(const bxr_vec2_t *points,
```

---


<a name="line-undefined"></a>
Draw filled triangles with the current color.

`triangles` the triangle array. Must not be NULL if `count` > 0.
`count` number of triangles.

```cpp
BXR_API void bxr_painter_draw_filled_triangles(const bxr_triangle_t *triangles,
```

---


<a name="line-undefined"></a>
Draw a single filled triangle with the current color.

```cpp
BXR_API void bxr_painter_draw_filled_triangle(bxr_triangle_t triangle)
```

---


<a name="line-undefined"></a>
Draw a filled triangle strip with the current color.

`points` the strip vertices. Must not be NULL if `count` > 0.
`count` number of points.

```cpp
BXR_API void bxr_painter_draw_filled_triangles_strip(const bxr_vec2_t *points,
```

---


<a name="line-undefined"></a>
Draw filled rectangles with the current color.

`rects` the rectangle array. Must not be NULL if `count` > 0.
`count` number of rectangles.

```cpp
BXR_API void bxr_painter_draw_filled_rects(const bxr_rect_t *rects,
```

---


<a name="line-undefined"></a>
Draw a single filled rectangle with the current color.

```cpp
BXR_API void bxr_painter_draw_filled_rect(bxr_rect_t rect)
```

---


<a name="line-undefined"></a>
Draw rectangles textured from the image bound to a channel, tinted by the
current color.

`channel` the texture channel, in `[0, BXR_PAINTER_MAX_TEXTURE_SLOTS)`; an
image must be bound to it.
`rects` the rectangle array. Must not be NULL if `count` > 0.
`count` number of rectangles.

```cpp
BXR_API void bxr_painter_draw_textured_rects(int channel,
```

---


<a name="line-undefined"></a>
Draw a single rectangle textured from the image bound to a channel, tinted
by the current color.

`channel` the texture channel, in `[0, BXR_PAINTER_MAX_TEXTURE_SLOTS)`; an
image must be bound to it.
`rect` the rectangle to draw.

```cpp
BXR_API void bxr_painter_draw_textured_rect(int channel,
```

---

