<a name="line-1"></a>
# Program Entry Point

Defines the program entry point (through SDL main callbacks) and connects it
to the `bxr_game_*()` callbacks from `bxr_game.h`.

Include it in exactly one source file of your game, usually the one that
implements the `bxr_game_*()` callbacks:

```cpp
#include <boxer/bxr.h>
#include <boxer/bxr_main.h>
```

The entry point lives in the game executable rather than in the library, so
boxer can be linked either statically or as a shared library (`.so`,
`.dylib` or `.dll`).

**NOTE:** like `SDL_main.h`, which it includes, it defines functions, so
including it in more than one source file fails to link.
