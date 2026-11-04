<a name="line-undefined"></a>
File `bxr_sampler.h`.

Copyright (c) 2026 nsix. All rights reserved.

# Samplers

samplers used to sample textures in shaders.

Create a sampler from one of the `bxr_sampler_e` presets, bind it with
`bxr_painter_set_sampler()`, and release it with `bxr_sampler_destroy()`.

<a name="line-undefined"></a>
## Enums

<a name="line-undefined"></a>

```cpp
typedef enum
{
  BXR_SAMPLER_POINT_CLAMP = 0,
  BXR_SAMPLER_POINT_WRAP,
  BXR_SAMPLER_LINEAR_CLAMP,
  BXR_SAMPLER_LINEAR_WRAP,
  BXR_GP_SAMPLER_SIZE,
} bxr_sampler_e
```

Sampler presets: filtering (point = nearest, linear) and address mode
(clamp to edge, wrap = repeat) applied on all axes.

---


<a name="line-undefined"></a>
## Typedefs

<a name="line-undefined"></a>

```cpp
typedef struct bxr_sampler_s
{
  SDL_GPUSampler *sampler;
} bxr_sampler_t
```

Handle to a GPU sampler.

---


<a name="line-undefined"></a>
## API

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

