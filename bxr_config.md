<a name="line-undefined"></a>
File `bxr_config.h`.

Copyright (c) 2025 nsix. All rights reserved.

# Configuration

<a name="line-undefined"></a>
## Global Configuration

<a name="line-undefined"></a>

```cpp
#define BXR_PATH_MAX_LENGTH 512
```

Max length of a file path in bytes, including the NUL terminator.
---


<a name="line-undefined"></a>

```cpp
#define BXR_ERROR_MAX_LENGTH 1024
```

Max length of an error message in bytes, including the NUL terminator.
Longer messages are truncated.
---


<a name="line-undefined"></a>
## Painter Configuration

<a name="line-undefined"></a>

```cpp
#define BXR_PAINTER_MAX_STATE 16
```

Max number of painter states that can be used at the same time (per frame).
---


<a name="line-undefined"></a>

```cpp
#define BXR_PAINTER_MAX_TEXTURE_SLOTS 4
```

Max number of textures that can be bound at the same time (per draw call).
---


<a name="line-undefined"></a>

```cpp
#define BXR_PAINTER_MAX_TRANSFORMS 64
```

Max number of transforms that can be pushed at the same time (per frame).
---


<a name="line-undefined"></a>

```cpp
#define BXR_PAINTER_MAX_UNIFORM_FLOATS 8
```

Max number of float (4 bytes) uniforms that can be set in a shader.
---


<a name="line-undefined"></a>

```cpp
#define BXR_PAINTER_MAX_OPTIMIZER_DEPTH 8
```

Max number of draw call that are looked back and batched together.
---


<a name="line-undefined"></a>
## Painter Resources Configuration

<a name="line-undefined"></a>

```cpp
#define BXR_PAINTER_MAX_TEXTURE_SIZE (16 * 1024 * 1024) // 16 mb
```

Max texture width or height in pixels.
---


<a name="line-undefined"></a>

```cpp
#define BXR_PAINTER_MAX_IMAGE 64
```

Max number of images that can be loaded at the same time.
---


<a name="line-undefined"></a>

```cpp
#define BXR_PAINTER_MAX_SHADER 8
```

Max number of shaders that can be loaded at the same time.
---


<a name="line-undefined"></a>

```cpp
#define BXR_PAINTER_MAX_PIPELINE 64
```

Max number of pipelines that can be created at the same time.
---


<a name="line-undefined"></a>
## Audio Configuration

<a name="line-undefined"></a>

```cpp
#define BXR_AUDIO_MAX 32
```

Max number of audio that can be loaded at the same time.
---


<a name="line-undefined"></a>

```cpp
#define BXR_AUDIO_MAX_VOICES 32
```

Max number of voices that can be played at the same time.
---


<a name="line-undefined"></a>

```cpp
#define BXR_AUDIO_MAX_TAGS 8
```

Max number of tags that can be associated with a voice.
---


<a name="line-undefined"></a>

```cpp
#define BXR_AUDIO_LOAD_FRAMES 2048
```

Size of the audio chunk fed to a playing voice's stream.

2048 frames * 2 channels * 4 bytes = 16 KB per chunk.
---


<a name="line-undefined"></a>
## INI Reader/Writer Configuration

<a name="line-undefined"></a>

```cpp
#define BXR_INI_DEFAULT_DATA_CAPACITY 512
```

Initial capacity in bytes of the INI writer buffer. The buffer doubles in
size when it is full.
---


<a name="line-undefined"></a>
## ECS Configuration

<a name="line-undefined"></a>

```cpp
#define BXR_ECS_DEFAULT_ENTITY 256
```

Initial entity capacity used by `bxr_ecs_create()` when `entity_count` is 0.
---


<a name="line-undefined"></a>

```cpp
#define BXR_ECS_MAX_COMPONENT 32
```

Max number of components that can be registered in an ECS instance.
---


<a name="line-undefined"></a>

```cpp
#define BXR_ECS_MAX_SYSTEM 16
```

Max number of systems that can be registered in an ECS instance.
---

