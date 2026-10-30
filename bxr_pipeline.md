<a name="line-undefined"></a>
File `bxr_pipeline.h`.

# Custom Graphics Pipelines for the Painter.

Typical usage: create shaders with `bxr_shader_create()`, combine them with
`bxr_pipeline_create()`, select the pipeline with
`bxr_painter_set_pipeline()`, and release it with `bxr_pipeline_destroy()`.

Copyright (c) 2026 nsix. All rights reserved.

<a name="line-undefined"></a>
## Public API

<a name="line-undefined"></a>
Create a graphics pipeline from a vertex and a fragment shader.

`shader_vert` a vertex shader from `bxr_shader_create()`.
`shader_frag` a fragment shader from `bxr_shader_create()`.
`primitive_type` how vertices are assembled into primitives.
`blend_mode` how fragments are blended with the render target.

`return` the new pipeline, or a pipeline with `id` 0 on failure.
Call `bxr_get_error()` for more information.

**Note**: the caller owns the pipeline and must release it with
`bxr_pipeline_destroy()`. The shaders can be destroyed once the pipeline is
created.

```cpp
BXR_API bxr_pipeline_t bxr_pipeline_create(bxr_shader_t shader_vert,
```

---


<a name="line-undefined"></a>
Check if a graphics pipeline handle is valid.

`pipeline` a pipeline from `bxr_pipeline_create()`.

`return` true if the pipeline is valid, false otherwise.

```cpp
BXR_API bool bxr_pipeline_is_valid(bxr_pipeline_t pipeline)
```

---


<a name="line-undefined"></a>
Destroy a graphics pipeline and release its GPU resources.

`pipeline` a pipeline from `bxr_pipeline_create()`. It must not be in use
by the painter for the current frame.

```cpp
BXR_API void bxr_pipeline_destroy(bxr_pipeline_t pipeline)
```

---

