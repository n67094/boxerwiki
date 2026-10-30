<a name="line-undefined"></a>
File `bxr_mem.h`.

# Memory Utilities.

Memory allocation and memory manipulation utilities.

Copyright (c) 2025 nsix. All rights reserved.

<a name="line-undefined"></a>
Allocate uninitialized memory.

`nbytes` size of the block in bytes.

`return` the new pointer, or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

```cpp
#define BXR_ALLOC(nbytes) SDL_malloc((size_t)(nbytes))
```

---


<a name="line-undefined"></a>
Allocate zero-initialized memory for an array.

`count` number of elements.
`nbytes` size of one element in bytes.

`return` the new pointer, or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

```cpp
#define BXR_CALLOC(count, nbytes) SDL_calloc((size_t)(count), (size_t)(nbytes))
```

---


<a name="line-undefined"></a>
Allocate one uninitialized object of the type pointed to by `ptr`.

`ptr` typed pointer lvalue receiving the allocated object.

`return` the new pointer (also stored in `ptr`), or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

```cpp
#define BXR_NEW(ptr) ((ptr) = BXR_ALLOC(sizeof *(ptr)))
```

---


<a name="line-undefined"></a>
Allocate one zero-initialized object of the type pointed to by `ptr`.

`ptr` typed pointer lvalue receiving the allocated object.

`return` the new pointer (also stored in `ptr`), or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

```cpp
#define BXR_NEW0(ptr) ((ptr) = BXR_CALLOC(1, sizeof *(ptr)))
```

---


<a name="line-undefined"></a>
Free memory and set `ptr` to NULL.

`ptr` lvalue pointing to memory from the BXR allocation macros, NULL is
allowed.

```cpp
#define BXR_FREE(ptr) ((void)(SDL_free(ptr), (ptr) = NULL))
```

---


<a name="line-undefined"></a>
Resize a block of memory.

`ptr` pointer to the block to resize, NULL behaves like `BXR_ALLOC()`.
`nbytes` new size of the block in bytes.

`return` the new pointer, or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

```cpp
#define BXR_RESIZE(ptr, nbytes) SDL_realloc((ptr), (size_t)(nbytes))
```

---


<a name="line-undefined"></a>
Fill `nbytes` of memory at `ptr` with the byte `value`.

`return` `ptr`.

```cpp
#define BXR_MEMSET(ptr, value, nbytes)                                         \
```

---


<a name="line-undefined"></a>
Copy `nbytes` from `src` to `dest`, the regions must not overlap.

`return` `dest`.

```cpp
#define BXR_MEMCPY(dest, src, nbytes)                                          \
```

---


<a name="line-undefined"></a>
Copy `nbytes` from `src` to `dest`, the regions may overlap.

`return` `dest`.

```cpp
#define BXR_MEMMOVE(dest, src, nbytes)                                         \
```

---


<a name="line-undefined"></a>
Compare the first `nbytes` of two memory regions.

`return` 0 if equal, a negative or positive value if the first differing
byte in `ptr1` is lower or greater than the one in `ptr2`.

```cpp
#define BXR_MEMCMP(ptr1, ptr2, nbytes)                                         \
```

---

