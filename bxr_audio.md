<a name="line-undefined"></a>
File `bxr_audio.h`.

Copyright (c) 2026 nsix. All rights reserved.

# Audio Management and Playback

Typical usage: `bxr_audio_create()`, then `bxr_voice_create()` for as many
voices as you need, then `bxr_voice_play()`, `bxr_voice_pause()`, etc.
Once done, call `bxr_voice_destroy()` and `bxr_audio_destroy()` to free the
resources.

When `BXR_AUDIO_MAX_VOICES` voices are alive, creating a new one stops and
destroys the oldest voice that was not created with `keep_alive` set. If
every voice is kept alive, the creation fails instead.

<a name="line-undefined"></a>
Handle to loaded audio data.

```cpp
typedef struct bxr_audio_s
```

---


<a name="line-undefined"></a>
Handle to a playback voice.

```cpp
typedef struct bxr_voice_s
```

---


<a name="line-undefined"></a>
Parameters for `bxr_voice_create()`.

`audio` the audio to play; must be valid.
`volume` initial volume, clamped to [0.0, 1.0].
`auto_play` start playing immediately when true.
`play_once` play a single time and then destroy the voice automatically;
when false the voice loops.
`keep_alive` never evict this voice when the voice limit is reached.

```cpp
typedef struct bxr_voice_desc_s
```

---


<a name="line-undefined"></a>
## Public API

<a name="line-undefined"></a>
Load a WAV or OGG file into memory.

The format is chosen from the file extension (`.wav` or `.ogg`).

`path` file path relative to the mounted directories; must not be NULL.

`return` the audio handle, or an id of `BXR_AUDIO_INVALID_ID` on failure.
Call `bxr_get_error()` for more information.

**Note**: the caller must free the audio with `bxr_audio_destroy()`.

```cpp
BXR_API bxr_audio_t bxr_audio_create(const char *path)
```

---


<a name="line-undefined"></a>
Get the duration of an audio.

`audio` the audio to query.

`return` the duration in milliseconds, or 0 if the audio is invalid.

```cpp
BXR_API Uint64 bxr_audio_get_length(bxr_audio_t audio)
```

---


<a name="line-undefined"></a>
Free an audio and its sample data.

`audio` the audio to destroy; invalid handles are logged and ignored.

**NOTE**: Every voice playing this audio is destroyed too and their handles
become invalid.

```cpp
BXR_API void bxr_audio_destroy(bxr_audio_t audio)
```

---


<a name="line-undefined"></a>
## Global controls

<a name="line-undefined"></a>
Set the master volume of the playback device.

`volume` gain clamped to [0.0, 1.0].

```cpp
BXR_API void bxr_audio_set_global_volume(float volume)
```

---


<a name="line-undefined"></a>
Get the master volume of the playback device.

`return` the current gain.

```cpp
BXR_API float bxr_audio_get_global_volume(void)
```

---


<a name="line-undefined"></a>
Check whether an audio handle is valid.

`audio` the audio to check.

`return` true if the audio is valid, false otherwise.

```cpp
BXR_API bool bxr_audio_is_valid(bxr_audio_t audio)
```

---


<a name="line-undefined"></a>
## Voice playback

<a name="line-undefined"></a>
Create a voice that plays an audio.

`desc` voice parameters; must not be NULL. Not retained after the call.

`return` the voice handle, or an id of `BXR_VOICE_INVALID_ID` if the audio
is invalid, all `BXR_AUDIO_MAX_VOICES` voices are marked `keep_alive`, or
the stream cannot be created.
Call `bxr_get_error()` for more information.

**Note**: the caller must free the voice with `bxr_voice_destroy()`, unless
`play_once` is set, in which case it is freed automatically once finished.

```cpp
BXR_API bxr_voice_t bxr_voice_create(const bxr_voice_desc_t *desc)
```

---


<a name="line-undefined"></a>
Set the volume of a voice.

`voice` the voice to change.
`volume` gain clamped to [0.0, 1.0].

```cpp
BXR_API void bxr_voice_set_volume(bxr_voice_t voice, float volume)
```

---


<a name="line-undefined"></a>
Get the volume of a voice.

`voice` the voice to query.

`return` the volume in [0.0, 1.0].

```cpp
BXR_API float bxr_voice_get_volume(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Start or resume playback from the current position.

`voice` the voice to play.

```cpp
BXR_API void bxr_voice_play(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Check whether a voice is currently playing.

`voice` the voice to query.

`return` true if the voice is playing, false if it is paused or stopped.

```cpp
BXR_API bool bxr_voice_is_playing(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Pause playback, keeping the current position.

`voice` the voice to pause.

```cpp
BXR_API void bxr_voice_pause(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Check whether a voice is not playing.

`voice` the voice to query.

`return` true if the voice is paused or stopped, false otherwise.

```cpp
BXR_API bool bxr_voice_is_paused(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Stop playback and rewind to the start.

`voice` the voice to stop.

```cpp
BXR_API void bxr_voice_stop(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Check whether a voice is stopped.

`voice` the voice to query.

`return` true if the voice is stopped, false otherwise.

```cpp
BXR_API bool bxr_voice_is_stopped(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Get the playback position of a voice.

`voice` the voice to query.

`return` the position in milliseconds, or 0 on error.

```cpp
BXR_API Uint64 bxr_voice_get_position(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Seek a voice to a position.

`voice` the voice to seek.
`position_ms` target position in milliseconds; must be less than the audio
length.

`return` true on success, false if the position is out of range or the
voice is invalid.
Call `bxr_get_error()` for more information.

```cpp
BXR_API bool bxr_voice_set_position(bxr_voice_t voice, Uint64 position_ms)
```

---


<a name="line-undefined"></a>
Set the playback speed of a voice, which also shifts its pitch.

`voice` the voice to change.
`pitch` frequency ratio clamped to [0.01, 100.0]; 1.0 is normal speed.

`return` true on success, false on failure.
Call `bxr_get_error()` for more information.

```cpp
BXR_API bool bxr_voice_set_pitch(bxr_voice_t voice, float pitch)
```

---


<a name="line-undefined"></a>
Get the pitch of a voice.

`voice` the voice to query.

`return` the frequency ratio; 1.0 is normal speed.

```cpp
BXR_API float bxr_voice_get_pitch(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Set the stereo balance of a voice.

Only mono and stereo sources can be panned. Sources with more channels play
with their own layout.

`voice` the voice to change.
`pan` balance clamped to [-1.0, 1.0]: -1.0 left, 0.0 center, 1.0 right.

`return` true on success, false on failure.
Call `bxr_get_error()` for more information.

**NOTE:** Only mono and stereo sources can be panned.

```cpp
BXR_API bool bxr_voice_set_pan(bxr_voice_t voice, float pan)
```

---


<a name="line-undefined"></a>
Get the stereo balance of a voice.

`voice` the voice to query.

`return` the pan in [-1.0, 1.0].

```cpp
BXR_API float bxr_voice_get_pan(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Check whether a voice handle is valid.

`voice` the voice to check.

`return` true if the voice is valid, false otherwise.

```cpp
BXR_API bool bxr_voice_is_valid(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Stop a voice and free it, removing it from all its tags.

`voice` the voice to destroy.

```cpp
BXR_API void bxr_voice_destroy(bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
## Tags

<a name="line-undefined"></a>
Add a voice to a tag.

`tag_name` the tag; must not be NULL (The string is copied).
`voice` the voice to tag.

`return` true on success or if the voice already has this tag, false on
failure.
Call `bxr_get_error()` for more information.

```cpp
BXR_API bool bxr_audio_tag_add(const char *tag_name, bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
Remove a voice from a tag.

`tag_name` the tag; must not be NULL.
`voice` the voice to untag.

`return` true on success, false if the voice is invalid or was not in the
tag.

```cpp
BXR_API bool bxr_audio_tag_remove(const char *tag_name, bxr_voice_t voice)
```

---


<a name="line-undefined"></a>
## Group playback

<a name="line-undefined"></a>
Set the volume of every voice in a tag.

`tag_name` the tag.
`volume` gain clamped to [0.0, 1.0].

```cpp
BXR_API void bxr_audio_tag_set_volume(const char *tag_name, float volume)
```

---


<a name="line-undefined"></a>
Start or resume every voice in a tag.

`tag_name` the tag.

```cpp
BXR_API void bxr_audio_tag_play(const char *tag_name)
```

---


<a name="line-undefined"></a>
Pause every voice in a tag.

`tag_name` the tag.

```cpp
BXR_API void bxr_audio_tag_pause(const char *tag_name)
```

---


<a name="line-undefined"></a>
Stop and rewind every voice in a tag.

`tag_name` the tag.

```cpp
BXR_API void bxr_audio_tag_stop(const char *tag_name)
```

---

