<a name="line-undefined"></a>
File `bxr_pool.h`.

Copyright (c) 2026 nsix. All rights reserved.

# Resource Pool

Fixed-size slot pool handing out generational ids, used to manage resources.

Typical usage: create the pool, acquire a slot, generate an id for it and
give the id to callers, check or resolve the id back to its slot, release the
slot, destroy the pool.

<a name="line-undefined"></a>
Create a pool with every slot free.

`number_of_slots` number of slots, valid slot indices are
`[0, number_of_slots)`.

`return` the new pool, or NULL on allocation failure.
Call `bxr_get_error()` for more information.

**Note**: the caller must free the result with `bxr_pool_destroy()`.

```cpp
bxr_pool_t *bxr_pool_create(size_t number_of_slots)
```

---


<a name="line-undefined"></a>
Destroy a pool and free its memory.

Ids generated from the pool must not be used afterwards.

`pool` the pool to destroy, may be NULL.

```cpp
void bxr_pool_destroy(bxr_pool_t *pool)
```

---


<a name="line-undefined"></a>
Take a free slot from the pool.

`pool` the pool. Must not be NULL.

`return` the slot index, or `BXR_POOL_INVALID_SLOT` if the pool is full.

**Note**: the slot must be given back with `bxr_pool_release_slot()`.

```cpp
int bxr_pool_acquire_slot(bxr_pool_t *pool)
```

---


<a name="line-undefined"></a>
Give a slot back to the pool.

Bumps the slot generation, so ids previously generated for it become
invalid.

`pool` the pool. Must not be NULL.
`slot_index` a slot currently acquired from this pool.

```cpp
void bxr_pool_release_slot(bxr_pool_t *pool, int slot_index)
```

---


<a name="line-undefined"></a>
Generate the id of an acquired slot.

Bumps the slot generation, so any id generated earlier for the same slot
becomes invalid. Call it once per acquisition.

`pool` the pool. Must not be NULL.
`slot_index` a slot currently acquired from this pool.

`return` the new id, or BXR_POOL_INVALID_ID (0) on failure.

```cpp
Uint32 bxr_pool_generate_id(bxr_pool_t *pool, int slot_index)
```

---


<a name="line-undefined"></a>
Check that an id refers to the current generation of its slot.

`pool` the pool. Must not be NULL.
`id` the id to check.

`return` true if the id is valid, false otherwise.

```cpp
bool bxr_pool_is_valid_id(bxr_pool_t *pool, Uint32 id)
```

---


<a name="line-undefined"></a>
Get the slot index encoded in an id.

`pool` the pool. Must not be NULL.
`id` a valid id generated from this pool.

`return` the slot index, or `BXR_POOL_INVALID_SLOT` on failure.

```cpp
int bxr_pool_get_slot_from_id(bxr_pool_t *pool, Uint32 id)
```

---

