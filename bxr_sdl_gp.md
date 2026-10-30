<a name="line-undefined"></a>
File `bxr_sdl_gp.h`.

Copyright (c) 2026 nsix. All rights reserved.

# SDL_gp Include

Includes SDL_gp configured with boxer limits from `bxr_config.h`.

Always include this header instead of `<SDL_gp.h>`: the `SDL_GP_*` limits
must be defined before SDL_gp is included, otherwise its defaults are used.
