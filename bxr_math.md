<a name="line-1"></a>
File `bxr_math.h`.

Copyright (c) 2025 - 2026 nsix. All rights reserved.

# Math Utilities

2D vector, line, triangle and rectangle types with their helpers, plus
scalar functions (mostly aliases of the SDL math functions).

<a name="line-21"></a>
## Constants

<a name="line-25"></a>

```cpp
#define BXR_PI_D SDL_PI_D
#define BXR_PI_F SDL_PI_F
#define BXR_PI2_F (2.0f * SDL_PI_F)
#define BXR_PI2_D (2.0f * SDL_PI_D)
```

Pi and 2 * pi, in `float` (`_F`) and `double` (`_D`) precision.

---


<a name="line-33"></a>

```cpp
#define BXR_EPSILON SDL_FLT_EPSILON
#define BXR_FLOAT_MIN FLT_MIN
#define BXR_FLOAT_MAX FLT_MAX
```

Smallest positive and largest `float` values, and the tolerance used by
`bxr_equal()`.

---


<a name="line-41"></a>
## Min, Max and Clamp

<a name="line-45"></a>

```cpp
#define bxr_min SDL_min
#define bxr_max SDL_max
#define bxr_clamp SDL_clamp
```

Minimum, maximum and clamping of values of any numeric type.

Aliases of the SDL macros of the same name; arguments may be evaluated more
than once.

---


<a name="line-55"></a>
## Trigonometry

<a name="line-59"></a>

```cpp
#define bxr_cos SDL_cos
#define bxr_cosf SDL_cosf
#define bxr_sin SDL_sin
#define bxr_sinf SDL_sinf
#define bxr_tan SDL_tan
#define bxr_tanf SDL_tanf
#define bxr_acos SDL_acos
#define bxr_acosf SDL_acosf
#define bxr_asin SDL_asin
#define bxr_asinf SDL_asinf
#define bxr_atan SDL_atan
#define bxr_atanf SDL_atanf
#define bxr_atan2 SDL_atan2
#define bxr_atan2f SDL_atan2f
```

Trigonometric functions, angles in radians.

Aliases of the SDL functions of the same name, with the same signature and
behavior. The `f` variants work on `float`, the others on `double`.

---


<a name="line-80"></a>
## Rounding

<a name="line-84"></a>

```cpp
#define bxr_ceil SDL_ceil
#define bxr_ceilf SDL_ceilf
#define bxr_floor SDL_floor
#define bxr_floorf SDL_floorf
#define bxr_trunc SDL_trunc
#define bxr_truncf SDL_truncf
#define bxr_round SDL_round
#define bxr_roundf SDL_roundf
#define bxr_lround SDL_lround
#define bxr_lroundf SDL_lroundf
```

Rounding to an integral value.

Aliases of the SDL functions of the same name, with the same signature and
behavior. The `f` variants work on `float`, the others on `double`.

---


<a name="line-101"></a>
## Powers and Roots

<a name="line-105"></a>

```cpp
#define bxr_pow SDL_pow
#define bxr_powf SDL_powf
#define bxr_exp SDL_exp
#define bxr_expf SDL_expf
#define bxr_sqrt SDL_sqrt
#define bxr_sqrtf SDL_sqrtf
#define bxr_scalbn SDL_scalbn
#define bxr_scalbnf SDL_scalbnf
```

Powers, exponentials and square roots.

Aliases of the SDL functions of the same name, with the same signature and
behavior. The `f` variants work on `float`, the others on `double`.

---


<a name="line-120"></a>
## Floating Point

<a name="line-124"></a>

```cpp
#define bxr_fabs SDL_fabs
#define bxr_fabsf SDL_fabsf
#define bxr_copysign SDL_copysign
#define bxr_copysignf SDL_copysignf
#define bxr_fmod SDL_fmod
#define bxr_fmodf SDL_fmodf
#define bxr_modf SDL_modf
#define bxr_modff SDL_modff
#define bxr_isinf SDL_isinf
#define bxr_isinff SDL_isinff
#define bxr_isnan SDL_isnan
#define bxr_isnanf SDL_isnanf
```

Absolute value, sign copy, remainders, and infinity / NaN checks.

Aliases of the SDL functions of the same name, with the same signature and
behavior. The `f` variants work on `float`, the others on `double`.

---


<a name="line-143"></a>
## Typedefs

<a name="line-147"></a>

```cpp
typedef struct bxr_vec2_s
{
  float x, y;
} bxr_vec2_t
```

2D vector with `x` and `y` components.

---


<a name="line-155"></a>

```cpp
typedef bxr_vec2_t bxr_point_t
```

2D point with `x` and `y` coordinates.

---


<a name="line-160"></a>

```cpp
typedef struct bxr_line_s
{
  bxr_vec2_t a;
  bxr_vec2_t b;
} bxr_line_t
```

2D line segment with endpoints `a` and `b`.

---


<a name="line-169"></a>

```cpp
typedef struct bxr_triangle_s
{
  bxr_vec2_t a;
  bxr_vec2_t b;
  bxr_vec2_t c;
} bxr_triangle_t
```

2D triangle with vertices `a`, `b` and `c`.

---


<a name="line-179"></a>

```cpp
typedef struct bxr_rect_s
{
  float x, y, w, h;
} bxr_rect_t
```

2D rectangle with top-left corner `(x, y)` and size `(w, h)`.

---


<a name="line-187"></a>
## Scalar Helpers

<a name="line-191"></a>

```cpp
BXR_INLINE float bxr_sign(float val)
```

Computes the sign of a number.

`return`:

- -1 if `val` is less than zero;
- 0 if `val` is equal to zero;
- 1 if `val` is greater than zero.

---


<a name="line-206"></a>

```cpp
BXR_INLINE bool bxr_equal(float c1, float c2)
```

Compares two floats with a tolerance of `BXR_EPSILON`.

`return` `true` if the values are within epsilon of one another.

---


<a name="line-222"></a>

```cpp
BXR_INLINE float bxr_lerp(float a, float b, float step)
```

Linearly interpolates between two values.

`a` the start value, returned when `step` is 0.

`b` the end value, returned when `step` is 1.

`step` the position between the values, usually in [0, 1]; values outside
this range extrapolate.

`return` the interpolated value.

---


<a name="line-240"></a>

```cpp
BXR_INLINE float bxr_lerp_angle(float angle1, float angle2, float step)
```

Linearly interpolates between two angles along the shortest arc.

`angle1` the start angle in radians.

`angle2` the end angle in radians.

`step` the position between the angles, usually in [0, 1].

`return` the interpolated angle in radians.

---


<a name="line-264"></a>

```cpp
BXR_INLINE float bxr_normalize_angle(float angle)
```

Wraps an angle into [0, 2 * pi).

`angle` the angle in radians.

`return` the equivalent angle in [0, 2 * pi).

---


<a name="line-287"></a>
## Point

<a name="line-291"></a>

```cpp
#define bxr_point_create(x, y)
```

Constructs a `bxr_point_t` compound literal from `x` and `y`.

---


<a name="line-296"></a>
## 2D Vector

<a name="line-300"></a>

```cpp
#define bxr_vec2_create(x, y)
```

Constructs a `bxr_vec2_t` compound literal from `x` and `y`.

---


<a name="line-305"></a>

```cpp
BXR_INLINE bool bxr_vec2_equal(bxr_vec2_t v1, bxr_vec2_t v2)
```

Compares two vectors component-wise with `bxr_equal()`.

`return` `true` if both components are within epsilon of one another.

---


<a name="line-316"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_add(bxr_vec2_t v1, bxr_vec2_t v2)
```

`return` the component-wise sum `v1 + v2`.

---


<a name="line-325"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_sub(bxr_vec2_t v1, bxr_vec2_t v2)
```

`return` the component-wise difference `v1 - v2`.

---


<a name="line-334"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_mul(bxr_vec2_t v1, bxr_vec2_t v2)
```

`return` the component-wise product `v1 * v2`.

---


<a name="line-343"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_div(bxr_vec2_t v1, bxr_vec2_t v2)
```

`return` the component-wise quotient `v1 / v2`.

**Note**: a zero component in `v2` yields an infinite or NaN component.

---


<a name="line-354"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_scale(bxr_vec2_t v, float c)
```

`return` `v` with both components multiplied by `c`.

---


<a name="line-363"></a>

```cpp
BXR_INLINE float bxr_vec2_dot(bxr_vec2_t v1, bxr_vec2_t v2)
```

`return` the dot product of two vectors.

---


<a name="line-372"></a>

```cpp
BXR_INLINE float bxr_vec2_len2(bxr_vec2_t v)
```

`return` the squared length of the vector, cheaper than `bxr_vec2_len()`
when only comparing lengths.

---


<a name="line-382"></a>

```cpp
BXR_INLINE float bxr_vec2_len(bxr_vec2_t v)
```

`return` the length (magnitude) of the vector.

---


<a name="line-391"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_normalize(bxr_vec2_t v)
```

`return` the unit vector with the same direction as `v`, or the zero vector
if the length of `v` is below `BXR_EPSILON`.

---


<a name="line-406"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_negate(bxr_vec2_t v)
```

`return` the negation of the vector (`-v`).

---


<a name="line-415"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_perp(bxr_vec2_t v)
```

`return` `v` rotated by 90 degrees counter-clockwise (`(-y, x)`).

---


<a name="line-424"></a>

```cpp
BXR_INLINE float bxr_vec2_cross(bxr_vec2_t v1, bxr_vec2_t v2)
```

Computes the 2D cross product (the z component of the 3D cross product).

`return` `v1.x * v2.y - v1.y * v2.x`; positive if `v2` is counter-clockwise
from `v1`, negative if clockwise, 0 if they are parallel.

---


<a name="line-437"></a>

```cpp
BXR_INLINE float bxr_vec2_angle(bxr_vec2_t v)
```

`return` the angle in radians between the vector and the positive x axis,
in [-pi, pi].

---


<a name="line-447"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_proj(bxr_vec2_t v1, bxr_vec2_t v2)
```

`return` the projection of `v1` onto `v2`.

---


<a name="line-463"></a>

```cpp
BXR_INLINE float bxr_vec2_dist(bxr_vec2_t v1, bxr_vec2_t v2)
```

`return` the distance between the two points.

---


<a name="line-474"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_lerp(bxr_vec2_t v1, bxr_vec2_t v2, float step)
```

Linearly interpolates between two vectors, component-wise.

`step` the position between `v1` and `v2`, usually in [0, 1].

`return` the interpolated vector.

---


<a name="line-492"></a>

```cpp
#define bxr_vec2_zero()
```

`return` the zero vector.

---


<a name="line-497"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_polar(float angle, float len)
```

Builds a vector from polar coordinates.

`angle` the angle in radians from the positive x axis.

`len` the length of the vector.

`return` the vector in cartesian coordinates.

---


<a name="line-512"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_min(bxr_vec2_t v1, bxr_vec2_t v2)
```

`return` the component-wise minimum of two vectors.

---


<a name="line-521"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_max(bxr_vec2_t v1, bxr_vec2_t v2)
```

`return` the component-wise maximum of two vectors.

---


<a name="line-530"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_floor(bxr_vec2_t v)
```

`return` the component-wise floor of the specified vector.

---


<a name="line-539"></a>

```cpp
BXR_INLINE bxr_vec2_t bxr_vec2_ceil(bxr_vec2_t v)
```

`return` the component-wise ceiling of the specified vector.

---


<a name="line-548"></a>
## Line and Triangle

<a name="line-552"></a>

```cpp
#define bxr_line_create(ax, ay, bx, by)
```

Constructs a `bxr_line_t` compound literal from the segment `(ax, ay)` to
`(bx, by)`.

---


<a name="line-559"></a>

```cpp
#define bxr_triangle_create(ax, ay, bx, by, cx, cy)
```

Constructs a `bxr_triangle_t` compound literal from its three vertices.

---


<a name="line-565"></a>
## Rectangle

<a name="line-569"></a>

```cpp
#define bxr_rect_create(x, y, w, h)
```

Constructs a `bxr_rect_t` compound literal from its top-left corner
`(x, y)`, width `w` and height `h`.

---


<a name="line-575"></a>

```cpp
BXR_INLINE float bxr_rect_area(bxr_rect_t rect)
```

`return` the area of the rectangle.

---


<a name="line-584"></a>

```cpp
BXR_INLINE bool bxr_rect_overlap(bxr_rect_t r1, bxr_rect_t r2)
```

`return` `true` if the rectangles overlap or touch.

---


<a name="line-602"></a>

```cpp
BXR_INLINE bxr_rect_t bxr_rect_get_intersection(bxr_rect_t r1, bxr_rect_t r2)
```

`return` the intersection of the two rectangles. If they do not overlap, the
returned rectangle has an area of 0.

---


<a name="line-623"></a>

```cpp
BXR_INLINE bool bxr_rect_contains(bxr_rect_t r1, bxr_rect_t r2)
```

`return` `true` if `r1` completely contains `r2`, edges included.

---


<a name="line-641"></a>

```cpp
BXR_INLINE bool bxr_rect_contains_point(bxr_rect_t rect, bxr_vec2_t point)
```

`return` `true` if the rectangle contains the point, edges included.

---


<a name="line-659"></a>

```cpp
BXR_INLINE bool bxr_rect_adjacent(bxr_rect_t r1, bxr_rect_t r2)
```

`return` `true` if an edge of one rectangle lies on the same line as the
opposite edge of the other.

---


<a name="line-682"></a>

```cpp
BXR_INLINE bxr_rect_t bxr_rect_expand(bxr_rect_t rect, float amount)
```

`return` the rectangle grown by `amount` on each side, keeping its center.

---


<a name="line-694"></a>

```cpp
BXR_INLINE bxr_rect_t bxr_rect_contract(bxr_rect_t rect, float amount)
```

`return` the rectangle shrunk by `amount` on each side, keeping its center.

**Note**: the width or height becomes negative when `amount` is greater
than half of it.

---

