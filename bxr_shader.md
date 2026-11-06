<a name="line-1"></a>
# Shaders

shaders loaded from bytecode files in the mounted asset directories.

Shader files are read with the `bxr_asset.h` API and must be named
`<name>.<stage>.<format>`, where:

- `<name>` is the name of the shader (e.g. "basic", "sprite").
- `<stage>` is "vert" for a vertex shader or "frag" for a fragment shader.
- `<format>` is the bytecode format: "spv" (SPIR-V), "msl" (Metal Shading
Language), "dxil" or "dxbc". It is picked at runtime from the formats
supported by the GPU device, in that order of preference.

Example: "shaders/basic.vert.spv" is a vertex shader named "basic" in SPIR-V.

See `bxr_pipeline.h` for a typical usage example.

<a name="line-31"></a>

```cpp
#define BXR_SHADER_INVALID_ID 0
```


---


<a name="line-34"></a>
## Enums

<a name="line-38"></a>

```cpp
typedef enum
{
  BXR_SHADER_STAGE_VERTEX   = SDL_GPU_SHADERSTAGE_VERTEX,
  BXR_SHADER_STAGE_FRAGMENT = SDL_GPU_SHADERSTAGE_FRAGMENT,
  BXR_SHADER_STAGE_SIZE     = 2,
} bxr_shader_stage_e
```


---


<a name="line-46"></a>
## Typedefs

<a name="line-50"></a>

```cpp
typedef struct bxr_shader_s
{
  size_t id;
} bxr_shader_t
```

Handle to a GPU shader.

---


<a name="line-58"></a>

```cpp
typedef struct bxr_shader_desc_s
{
  const char *name;
  const char *entrypoint;
  bxr_shader_stage_e stage;
  Uint32 num_samplers;
  Uint32 num_storage_textures;
  Uint32 num_storage_buffers;
  Uint32 num_uniform_buffers;
} bxr_shader_desc_t
```

Shader creation parameters.

`name` asset path without the format extension (e.g. "shaders/basic.vert").
Must not be NULL.

`entrypoint` name of the entry function in the bytecode (e.g. "main").

`stage` must match the `<stage>` part of `name`.

`num_*` number of resources of each kind used by the shader.

---


<a name="line-81"></a>
## API

<a name="line-85"></a>

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


<a name="line-99"></a>

```cpp
BXR_API SDL_GPUShader *bxr_shader_get_sdl(bxr_shader_t shader)
```

Get the underlying SDL GPU shader.

`shader` a shader from `bxr_shader_create()`.

`return` the SDL shader, or NULL if `shader` is invalid.

**Note**: the returned pointer is owned by boxer and stays valid until
`bxr_shader_destroy()` is called on `shader`.

---


<a name="line-111"></a>

```cpp
BXR_API bool bxr_shader_is_valid(bxr_shader_t shader)
```

Check if a shader handle is valid.

`shader` a shader from `bxr_shader_create()`.

`return` true if the shader is valid, false otherwise.

---


<a name="line-120"></a>

```cpp
BXR_API void bxr_shader_destroy(bxr_shader_t shader)
```

Destroy a shader and release its GPU resources.

Invalid or already destroyed shaders are ignored.

`shader` a shader from `bxr_shader_create()`. Pipelines already created from
it remain valid.

---

