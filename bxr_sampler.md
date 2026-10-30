<a name="line-undefined"></a>
File `bxr_sampler.h`.

Copyright (c) 2026 nsix. All rights reserved.

# GPU Samplers

GPU samplers used to sample textures in shaders.

Create a sampler from one of the `bxr_sampler_e` presets, bind it with
`bxr_painter_set_sampler()`, and release it with `bxr_sampler_destroy()`.

<a name="line-undefined"></a>

```cpp
typedef enum
```

Sampler presets: filtering (point = nearest, linear) and address mode
(clamp to edge, wrap = repeat) applied on all axes.
---


<a name="line-undefined"></a>
## Internal API

<a name="line-undefined"></a>

```cpp
bool bxr_sampler_setup(void)
```

Initializes the sampler system.
---


<a name="line-undefined"></a>

```cpp
void bxr_sampler_teardown(void)
```

Tears down the sampler system.
---


<a name="line-undefined"></a>
## Public API

<a name="line-undefined"></a>

```cpp
BXR_API bxr_sampler_t bxr_sampler_create(bxr_sampler_e sampler_type)
```

Create a GPU sampler from a preset.

`sampler_type` the preset to use.

`return` the created sampler, or a sampler whose `sampler` field is NULL on
failure.
Call `bxr_get_error()` for more information.

**Note**: the caller owns the sampler and must release it with
`bxr_sampler_destroy()` while the GPU device is still alive.
---


<a name="line-undefined"></a>

```cpp
BXR_API void bxr_sampler_destroy(bxr_sampler_t *sampler)
```

Destroy a GPU sampler and release its GPU resources.

`sampler` the sampler to destroy.
---

