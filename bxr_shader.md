<a name="line-undefined"></a>
File `bxr_shader.h`.

Copyright (c) 2026 nsix. All rights reserved.

# GPU Shaders

GPU shaders loaded from bytecode files in the mounted asset directories.

Shader files are read with the `bxr_asset.h` API and must be named
`<name>.<stage>.<format>`, where:

- `<name>` is the name of the shader (e.g. "basic", "sprite").
- `<stage>` is "vert" for a vertex shader or "frag" for a fragment shader.
- `<format>` is the bytecode format: "spv" (SPIR-V), "msl" (Metal Shading
Language), "dxil" or "dxbc". It is picked at runtime from the formats
supported by the GPU device, in that order of preference.

Example: "shaders/basic.vert.spv" is a vertex shader named "basic" in SPIR-V.

Typical usage: create a vertex and a fragment shader with
`bxr_shader_create()`, combine them with `bxr_pipeline_create()`, and
release them with `bxr_shader_destroy()`.

<a name="line-undefined"></a>

```cpp
typedef struct bxr_shader_desc_s
```

Shader creation parameters.

`name` asset path without the format extension (e.g. "shaders/basic.vert").
Must not be NULL.
`entrypoint` name of the entry function in the bytecode (e.g. "main").
`stage` must match the `<stage>` part of `name`.
`num_*` number of resources of each kind used by the shader.
---


<a name="line-undefined"></a>
## Internal API

<a name="line-undefined"></a>

```cpp
bool bxr_shader_setup(bxr_context_t *context)
```

Initializes the shader system.

`context` is the bxr context to use for shader operations.
---


<a name="line-undefined"></a>

```cpp
void bxr_shader_teardown(void)
```

Shuts down the shader system.
---


<a name="line-undefined"></a>
## Public API

<a name="line-undefined"></a>

```cpp
BXR_API bxr_shader_t bxr_shader_create(const bxr_shader_desc_t *desc)
```

Load a shader bytecode file and create a GPU shader from it.

`desc` the shader description. Must not be NULL.

`return` the new shader, or a shader with `id` `BXR_SHADER_INVALID_ID` on
failure.
Call `bxr_get_error()` for more information.

**Note**: the caller owns the shader and must release it with
`bxr_shader_destroy()`.
---


<a name="line-undefined"></a>

```cpp
BXR_API SDL_GPUShader *bxr_shader_get_sdl(bxr_shader_t shader)
```

Get the underlying SDL GPU shader.

`shader` a shader from `bxr_shader_create()`.

`return` the SDL shader, or NULL if `shader` is invalid.

**Note**: the returned pointer is owned by boxer and stays valid until
`bxr_shader_destroy()` is called on `shader`.
---


<a name="line-undefined"></a>

```cpp
BXR_API bool bxr_shader_is_valid(bxr_shader_t shader)
```

Check if a shader handle is valid.

`shader` a shader from `bxr_shader_create()`.

`return` true if the shader is valid, false otherwise.
---


<a name="line-undefined"></a>

```cpp
BXR_API void bxr_shader_destroy(bxr_shader_t shader)
```

Destroy a shader and release its GPU resources.

Invalid or already destroyed shaders are ignored.

`shader` a shader from `bxr_shader_create()`. Pipelines already created from
it remain valid.
---

