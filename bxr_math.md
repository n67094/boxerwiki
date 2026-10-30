<a name="line-undefined"></a>
File `bxr_math.h`.

# Boxer's Math Utilities.

Copyright (c) 2025 nsix. All rights reserved.

<a name="line-undefined"></a>
Aliases for the SDL math functions, see the SDL documentation for details.

```cpp
#define bxr_min SDL_min
```

---


<a name="line-undefined"></a>
## Scalar Functions and Macros

<a name="line-undefined"></a>
Computes the sign of a number.

`return`:

- -1 if `val` is less than zero;
- 0 if `val` is equal to zero;
- 1 if `val` is greater than zero.

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
Compares two floats with a tolerance of `BXR_EPSILON`.

`return` `true` if the values are within epsilon of one another.

```cpp
BXR_INLINE bool
```

---


<a name="line-undefined"></a>
Linearly interpolates between two values.

`a` the start value, returned when `step` is 0.
`b` the end value, returned when `step` is 1.
`step` the position between the values, usually in [0, 1]; values outside
this range extrapolate.

`return` the interpolated value.

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
Linearly interpolates between two angles along the shortest arc.

`angle1` the start angle in radians.
`angle2` the end angle in radians.
`step` the position between the angles, usually in [0, 1].

`return` the interpolated angle in radians.

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
Wraps an angle into [0, 2 * pi).

`angle` the angle in radians.

`return` the equivalent angle in [0, 2 * pi).

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
## Point

<a name="line-undefined"></a>
Constructs a `bxr_point_t` compound literal from `x` and `y`.

```cpp
#define bxr_point_create(x, y) ((const bxr_point_t){ x, y })
```

---


<a name="line-undefined"></a>
## 2D Vector

<a name="line-undefined"></a>
Constructs a `bxr_vec2_t` compound literal from `x` and `y`.

```cpp
#define bxr_vec2_create(x, y) ((const bxr_vec2_t){ x, y })
```

---


<a name="line-undefined"></a>
Compares two vectors component-wise with `bxr_equal()`.

`return` `true` if both components are within epsilon of one another.

```cpp
BXR_INLINE bool
```

---


<a name="line-undefined"></a>
`return` the component-wise sum `v1 + v2`.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the component-wise difference `v1 - v2`.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the component-wise product `v1 * v2`.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the component-wise quotient `v1 / v2`.

**Note**: a zero component in `v2` yields an infinite or NaN component.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` `v` with both components multiplied by `c`.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the dot product of two vectors.

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
`return` the squared length of the vector, cheaper than `bxr_vec2_len()`
when only comparing lengths.

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
`return` the length (magnitude) of the vector.

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
`return` the unit vector with the same direction as `v`, or the zero vector
if the length of `v` is below `BXR_EPSILON`.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the negation of the vector (`-v`).

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` `v` rotated by 90 degrees counter-clockwise (`(-y, x)`).

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
Computes the 2D cross product (the z component of the 3D cross product).

`return` `v1.x * v2.y - v1.y * v2.x`; positive if `v2` is counter-clockwise
from `v1`, negative if clockwise, 0 if they are parallel.

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
`return` the angle in radians between the vector and the positive x axis,
in [-pi, pi].

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
`return` the projection of `v1` onto `v2`.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the distance between the two points.

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
Linearly interpolates between two vectors, component-wise.

`step` the position between `v1` and `v2`, usually in [0, 1].

`return` the interpolated vector.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the zero vector.

```cpp
#define bxr_vec2_zero() (bxr_vec2_create(0.0f, 0.0f))
```

---


<a name="line-undefined"></a>
Builds a vector from polar coordinates.

`angle` the angle in radians from the positive x axis.
`len` the length of the vector.

`return` the vector in cartesian coordinates.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the component-wise minimum of two vectors.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the component-wise maximum of two vectors.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the component-wise floor of the specified vector.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
`return` the component-wise ceiling of the specified vector.

```cpp
BXR_INLINE bxr_vec2_t
```

---


<a name="line-undefined"></a>
## Line

<a name="line-undefined"></a>
Constructs a `bxr_line_t` compound literal from the segment `(ax, ay)` to
`(bx, by)`.

```cpp
#define bxr_line_create(ax, ay, bx, by)                                        \
```

---


<a name="line-undefined"></a>
## Triangle

<a name="line-undefined"></a>
Constructs a `bxr_triangle_t` compound literal from its three vertices.

```cpp
#define bxr_triangle_create(ax, ay, bx, by, cx, cy)                            \
```

---


<a name="line-undefined"></a>
## Rectangle

<a name="line-undefined"></a>
Constructs a `bxr_rect_t` compound literal from its top-left corner
`(x, y)`, width `w` and height `h`.

```cpp
#define bxr_rect_create(x, y, w, h) ((const bxr_rect_t){ x, y, w, h })
```

---


<a name="line-undefined"></a>
`return` the area of the rectangle.

```cpp
BXR_INLINE float
```

---


<a name="line-undefined"></a>
`return` `true` if the rectangles overlap or touch.

```cpp
BXR_INLINE bool
```

---


<a name="line-undefined"></a>
`return` the intersection of the two rectangles. If they do not overlap, the
returned rectangle has an area of 0.

```cpp
BXR_INLINE bxr_rect_t
```

---


<a name="line-undefined"></a>
`return` `true` if `r1` completely contains `r2`, edges included.

```cpp
BXR_INLINE bool
```

---


<a name="line-undefined"></a>
`return` `true` if the rectangle contains the point, edges included.

```cpp
BXR_INLINE bool
```

---


<a name="line-undefined"></a>
`return` `true` if an edge of one rectangle lies on the same line as the
opposite edge of the other.

```cpp
BXR_INLINE bool
```

---


<a name="line-undefined"></a>
`return` the rectangle grown by `amount` on each side, keeping its center.

```cpp
BXR_INLINE bxr_rect_t
```

---


<a name="line-undefined"></a>
`return` the rectangle shrunk by `amount` on each side, keeping its center.

**Note**: the width or height becomes negative when `amount` is greater
than half of it.

```cpp
BXR_INLINE bxr_rect_t
```

---

