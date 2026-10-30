<a name="line-undefined"></a>
File `bxr.h`.

# Boxer's Main Header File.

**NOTE:** Boxer owns the program entry point through SDL main callbacks: do
not write a `main()`, implement the callbacks of `bxr_game.h` instead.

Copyright (c) 2026 nsix. All rights reserved.

<a name="line-undefined"></a>
Request the application to exit.

Asynchronous: pushes an `SDL_EVENT_QUIT` and returns immediately. The
current frame finishes, then `bxr_game_teardown()` and the subsystem
teardowns run before the process exits. Safe to call from any thread.

```cpp
void bxr_quit(void)
```

---

