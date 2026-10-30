<a name="line-undefined"></a>
File `bxr_assert.h`

Copyright (c) 2026 nsix. All rights reserved.

# Assertion

Asserts that an expression is true, and aborts the program if it is false.

<a name="line-undefined"></a>
## Macros

<a name="line-undefined"></a>
Check that `expr` is true, and abort the program if it is false.

```cpp
#define BXR_ASSERT(expr) SDL_assert(expr)
```

---

