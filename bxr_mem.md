<a name="line-1"></a>
File `bxr_mem.h`.

Copyright (c) 2025 - 2026 nsix. All rights reserved.

# Memory Utilities

Memory allocation and memory manipulation utilities.

<a name="line-16"></a>
## Macros

<a name="line-20"></a>

```cpp
#define BXR_ALLOC(nbytes)
```

Allocate uninitialized memory.

`nbytes` size of the block in bytes.

`return` the new pointer, or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

---


<a name="line-31"></a>

```cpp
#define BXR_CALLOC(count, nbytes)
```

Allocate zero-initialized memory for an array.

`count` number of elements.

`nbytes` size of one element in bytes.

`return` the new pointer, or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

---


<a name="line-44"></a>

```cpp
#define BXR_NEW(ptr)
```

Allocate one uninitialized object of the type pointed to by `ptr`.

`ptr` typed pointer lvalue receiving the allocated object.

`return` the new pointer (also stored in `ptr`), or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

---


<a name="line-55"></a>

```cpp
#define BXR_NEW0(ptr)
```

Allocate one zero-initialized object of the type pointed to by `ptr`.

`ptr` typed pointer lvalue receiving the allocated object.

`return` the new pointer (also stored in `ptr`), or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

---


<a name="line-66"></a>

```cpp
#define BXR_FREE(ptr)
```

Free memory and set `ptr` to NULL.

`ptr` lvalue pointing to memory from the BXR allocation macros, NULL is
allowed.

---


<a name="line-74"></a>

```cpp
#define BXR_RESIZE(ptr, nbytes)
```

Resize a block of memory.

`ptr` pointer to the block to resize, NULL behaves like `BXR_ALLOC()`.

`nbytes` new size of the block in bytes.

`return` the new pointer, or NULL on failure.

**Note**: the caller must free the result with `BXR_FREE()`.

---


<a name="line-87"></a>

```cpp
#define BXR_MEMSET(ptr, value, nbytes)
```

Fill `nbytes` of memory at `ptr` with the byte `value`.

`return` `ptr`.

---


<a name="line-95"></a>

```cpp
#define BXR_MEMCPY(dest, src, nbytes)
```

Copy `nbytes` from `src` to `dest`, the regions must not overlap.

`return` `dest`.

---


<a name="line-103"></a>

```cpp
#define BXR_MEMMOVE(dest, src, nbytes)
```

Copy `nbytes` from `src` to `dest`, the regions may overlap.

`return` `dest`.

---


<a name="line-111"></a>

```cpp
#define BXR_MEMCMP(ptr1, ptr2, nbytes)
```

Compare the first `nbytes` of two memory regions.

`return` 0 if equal, a negative or positive value if the first differing
byte in `ptr1` is lower or greater than the one in `ptr2`.

---

