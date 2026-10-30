<a name="line-undefined"></a>
File `bxr_config.h`.

# Boxer's Configuration.

Copyright (c) 2025 nsix. All rights reserved.

<a name="line-undefined"></a>
## Global Configuration

<a name="line-undefined"></a>
Max length of a file path in bytes, including the NUL terminator.

```cpp
#define BXR_PATH_MAX_LENGTH 512
```

---


<a name="line-undefined"></a>
Max length of an error message in bytes, including the NUL terminator.
Longer messages are truncated.

```cpp
#define BXR_ERROR_MAX_LENGTH 1024
```

---


<a name="line-undefined"></a>
## Painter Configuration

<a name="line-undefined"></a>
Max number of painter states that can be used at the same time (per frame).

```cpp
#define BXR_PAINTER_MAX_STATE 16
```

---


<a name="line-undefined"></a>
Max number of textures that can be bound at the same time (per draw call).

```cpp
#define BXR_PAINTER_MAX_TEXTURE_SLOTS 4
```

---


<a name="line-undefined"></a>
Max number of transforms that can be pushed at the same time (per frame).

```cpp
#define BXR_PAINTER_MAX_TRANSFORMS 64
```

---


<a name="line-undefined"></a>
Max number of float (4 bytes) uniforms that can be set in a shader.

```cpp
#define BXR_PAINTER_MAX_UNIFORM_FLOATS 8
```

---


<a name="line-undefined"></a>
Max number of draw call that are looked back and batched together.

```cpp
#define BXR_PAINTER_MAX_OPTIMIZER_DEPTH 8
```

---


<a name="line-undefined"></a>
## Painter Resources Configuration

<a name="line-undefined"></a>
Max texture width or height in pixels.

```cpp
#define BXR_PAINTER_MAX_TEXTURE_SIZE (16 * 1024 * 1024) // 16 mb
```

---


<a name="line-undefined"></a>
Max number of images that can be loaded at the same time.

```cpp
#define BXR_PAINTER_MAX_IMAGE 64
```

---


<a name="line-undefined"></a>
Max number of shaders that can be loaded at the same time.

```cpp
#define BXR_PAINTER_MAX_SHADER 8
```

---


<a name="line-undefined"></a>
Max number of pipelines that can be created at the same time.

```cpp
#define BXR_PAINTER_MAX_PIPELINE 64
```

---


<a name="line-undefined"></a>
## Audio Configuration

<a name="line-undefined"></a>
Max number of audio that can be loaded at the same time.

```cpp
#define BXR_AUDIO_MAX 32
```

---


<a name="line-undefined"></a>
Max number of voices that can be played at the same time.

```cpp
#define BXR_AUDIO_MAX_VOICES 32
```

---


<a name="line-undefined"></a>
Max number of tags that can be associated with a voice.

```cpp
#define BXR_AUDIO_MAX_TAGS 8
```

---


<a name="line-undefined"></a>
Size of the audio chunk fed to a playing voice's stream.

2048 frames * 2 channels * 4 bytes = 16 KB per chunk.

```cpp
#define BXR_AUDIO_LOAD_FRAMES 2048
```

---


<a name="line-undefined"></a>
## INI Reader/Writer Configuration

<a name="line-undefined"></a>
Initial capacity in bytes of the INI writer buffer. The buffer doubles in
size when it is full.

```cpp
#define BXR_INI_DEFAULT_DATA_CAPACITY 512
```

---


<a name="line-undefined"></a>
## ECS Configuration

<a name="line-undefined"></a>
Initial entity capacity used by `bxr_ecs_create()` when `entity_count` is 0.

```cpp
#define BXR_ECS_DEFAULT_ENTITY 256
```

---


<a name="line-undefined"></a>
Max number of components that can be registered in an ECS instance.

```cpp
#define BXR_ECS_MAX_COMPONENT 32
```

---


<a name="line-undefined"></a>
Max number of systems that can be registered in an ECS instance.

```cpp
#define BXR_ECS_MAX_SYSTEM 16
```

---

