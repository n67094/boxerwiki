<a name="line-undefined"></a>
File `bxr_math.h`.

Copyright (c) 2025 nsix. All rights reserved.

# Math Utilities

<a name="line-undefined"></a>
## Typedefs

<a name="line-undefined"></a>

```cpp
typedef struct bxr_vec2_s
{
  float x, y;
} bxr_vec2_t
```

2D vector with `x` and `y` components.

---


<a name="line-undefined"></a>

```cpp
typedef bxr_vec2_t bxr_point_t
```

2D point with `x` and `y` coordinates.

---


<a name="line-undefined"></a>

```cpp
typedef struct bxr_line_s
{
  bxr_vec2_t a;
  bxr_vec2_t b;
} bxr_line_t
```

2D line segment with endpoints `a` and `b`.

---


<a name="line-undefined"></a>

```cpp
typedef struct bxr_triangle_s
{
  bxr_vec2_t a;
  bxr_vec2_t b;
  bxr_vec2_t c;
} bxr_triangle_t
```

##### 2D triangle with vertices `a`, `b` and `c`.

---


<a name="line-undefined"></a>

```cpp
typedef struct bxr_rect_s
{
  float x, y, w, h;
} bxr_rect_t
```

2D rectangle with top-left corner `(x, y)` and size `(w, h)`.

---


<a name="line-undefined"></a>
## Macros

<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_sign(float val)
{
  return ((0 == val) ? 0.0f : ((val > 0.0f) ? 1.0f : -1.0f));
}
```

Computes the sign of a number.

`return`:

- -1 if `val` is less than zero;
- 0 if `val` is equal to zero;
- 1 if `val` is greater than zero.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bool
bxr_equal(float c1, float c2)
{
  float diff = bxr_fabsf(c1 - c2);

  if (diff <= BXR_EPSILON) // near zero, absolute tolerance
    return true;

  return diff <= BXR_EPSILON * bxr_max(bxr_fabsf(c1), bxr_fabsf(c2));
}
```

Compares two floats with a tolerance of `BXR_EPSILON`.

`return` `true` if the values are within epsilon of one another.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_lerp(float a, float b, float step)
{
  return a + (b - a) * step;
}
```

Linearly interpolates between two values.

`a` the start value, returned when `step` is 0.

`b` the end value, returned when `step` is 1.

`step` the position between the values, usually in [0, 1]; values outside
this range extrapolate.

`return` the interpolated value.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_lerp_angle(float angle1, float angle2, float step)
{
  float diff = bxr_fmodf(angle2 - angle1, BXR_PI2_F); // (-2pi, 2pi)

  if (diff > BXR_PI_F)
    diff -= BXR_PI2_F;
  else if (diff < -BXR_PI_F)
    diff += BXR_PI2_F;

  return angle1 + diff * step;
}
```

Linearly interpolates between two angles along the shortest arc.

`angle1` the start angle in radians.

`angle2` the end angle in radians.

`step` the position between the angles, usually in [0, 1].

`return` the interpolated angle in radians.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_normalize_angle(float angle)
{
  float a = bxr_fmodf(angle, BXR_PI2_F);

  // If the input is negative, add 2*pi to wrap it into [0, 2*pi)
  if (a < 0.0f)
    a += BXR_PI2_F
```

Wraps an angle into [0, 2 * pi).

`angle` the angle in radians.

`return` the equivalent angle in [0, 2 * pi).

---


<a name="line-undefined"></a>
## Point

<a name="line-undefined"></a>

```cpp
#define bxr_point_create(x, y) ((const bxr_point_t){ x, y })
```

Constructs a `bxr_point_t` compound literal from `x` and `y`.

---


<a name="line-undefined"></a>
## 2D Vector

<a name="line-undefined"></a>

```cpp
#define bxr_vec2_create(x, y) ((const bxr_vec2_t){ x, y })
```

Constructs a `bxr_vec2_t` compound literal from `x` and `y`.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bool
bxr_vec2_equal(bxr_vec2_t v1, bxr_vec2_t v2)
{
  return bxr_equal(v1.x, v2.x) && bxr_equal(v1.y, v2.y);
}
```

Compares two vectors component-wise with `bxr_equal()`.

`return` `true` if both components are within epsilon of one another.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_add(bxr_vec2_t v1, bxr_vec2_t v2)
{
  return bxr_vec2_create(v1.x + v2.x, v1.y + v2.y);
}
```

`return` the component-wise sum `v1 + v2`.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_sub(bxr_vec2_t v1, bxr_vec2_t v2)
{
  return bxr_vec2_create(v1.x - v2.x, v1.y - v2.y);
}
```

`return` the component-wise difference `v1 - v2`.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_mul(bxr_vec2_t v1, bxr_vec2_t v2)
{
  return bxr_vec2_create(v1.x * v2.x, v1.y * v2.y);
}
```

`return` the component-wise product `v1 * v2`.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_div(bxr_vec2_t v1, bxr_vec2_t v2)
{
  return bxr_vec2_create(v1.x / v2.x, v1.y / v2.y);
}
```

`return` the component-wise quotient `v1 / v2`.

**Note**: a zero component in `v2` yields an infinite or NaN component.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_scale(bxr_vec2_t v, float c)
{
  return bxr_vec2_create(v.x * c, v.y * c);
}
```

`return` `v` with both components multiplied by `c`.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_vec2_dot(bxr_vec2_t v1, bxr_vec2_t v2)
{
  return v1.x * v2.x + v1.y * v2.y;
}
```

`return` the dot product of two vectors.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_vec2_len2(bxr_vec2_t v)
{
  return bxr_vec2_dot(v, v);
}
```

`return` the squared length of the vector, cheaper than `bxr_vec2_len()`
when only comparing lengths.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_vec2_len(bxr_vec2_t v)
{
  return bxr_sqrtf(bxr_vec2_len2(v));
}
```

`return` the length (magnitude) of the vector.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_normalize(bxr_vec2_t v)
{
  float c = bxr_vec2_len(v);

  if (c < BXR_EPSILON)
    return bxr_vec2_create(0.0f, 0.0f);
  else
    return bxr_vec2_scale(v, 1.0f / c);
}
```

`return` the unit vector with the same direction as `v`, or the zero vector
if the length of `v` is below `BXR_EPSILON`.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_negate(bxr_vec2_t v)
{
  return bxr_vec2_scale(v, -1.0f);
}
```

`return` the negation of the vector (`-v`).

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_perp(bxr_vec2_t v)
{
  return bxr_vec2_create(-v.y, v.x);
}
```

`return` `v` rotated by 90 degrees counter-clockwise (`(-y, x)`).

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_vec2_cross(bxr_vec2_t v1, bxr_vec2_t v2)
{
  bxr_vec2_t perp = bxr_vec2_perp(v1);
  return bxr_vec2_dot(perp, v2);
}
```

Computes the 2D cross product (the z component of the 3D cross product).

`return` `v1.x * v2.y - v1.y * v2.x`; positive if `v2` is counter-clockwise
from `v1`, negative if clockwise, 0 if they are parallel.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_vec2_angle(bxr_vec2_t v)
{
  return bxr_atan2f(v.y, v.x);
}
```

`return` the angle in radians between the vector and the positive x axis,
in [-pi, pi].

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_proj(bxr_vec2_t v1, bxr_vec2_t v2)
{
  float len2 = bxr_vec2_len2(v2);

  if (len2 < BXR_EPSILON * BXR_EPSILON)
    return (bxr_vec2_t){ 0.0f, 0.0f };

  float d = bxr_vec2_dot(v1, v2) / bxr_vec2_dot(v2, v2);

  return bxr_vec2_scale(v2, d);
}
```

`return` the projection of `v1` onto `v2`.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_vec2_dist(bxr_vec2_t v1, bxr_vec2_t v2)
{
  bxr_vec2_t v = bxr_vec2_sub(v1, v2);

  return bxr_vec2_len(v);
}
```

`return` the distance between the two points.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_lerp(bxr_vec2_t v1, bxr_vec2_t v2, float step)
{
  bxr_vec2_t out;

  out.x = bxr_lerp(v1.x, v2.x, step);
  out.y = bxr_lerp(v1.y, v2.y, step);

  return out;
}
```

Linearly interpolates between two vectors, component-wise.

`step` the position between `v1` and `v2`, usually in [0, 1].

`return` the interpolated vector.

---


<a name="line-undefined"></a>

```cpp
#define bxr_vec2_zero() (bxr_vec2_create(0.0f, 0.0f))
```

`return` the zero vector.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_polar(float angle, float len)
{
  return bxr_vec2_create(len * bxr_cosf(angle), len * bxr_sinf(angle));
}
```

Builds a vector from polar coordinates.

`angle` the angle in radians from the positive x axis.

`len` the length of the vector.

`return` the vector in cartesian coordinates.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_min(bxr_vec2_t v1, bxr_vec2_t v2)
{
  return bxr_vec2_create(bxr_min(v1.x, v2.x), bxr_min(v1.y, v2.y));
}
```

`return` the component-wise minimum of two vectors.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_max(bxr_vec2_t v1, bxr_vec2_t v2)
{
  return bxr_vec2_create(bxr_max(v1.x, v2.x), bxr_max(v1.y, v2.y));
}
```

`return` the component-wise maximum of two vectors.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_floor(bxr_vec2_t v)
{
  return bxr_vec2_create(bxr_floorf(v.x), bxr_floorf(v.y));
}
```

`return` the component-wise floor of the specified vector.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_vec2_t
bxr_vec2_ceil(bxr_vec2_t v)
{
  return bxr_vec2_create(bxr_ceilf(v.x), bxr_ceilf(v.y));
}
```

`return` the component-wise ceiling of the specified vector.

---


<a name="line-undefined"></a>

```cpp
#define bxr_line_create(ax, ay, bx, by)                                        \
  ((const bxr_line_t){ { ax, ay }, { bx, by } })
```

Constructs a `bxr_line_t` compound literal from the segment `(ax, ay)` to
`(bx, by)`.

---


<a name="line-undefined"></a>

```cpp
#define bxr_triangle_create(ax, ay, bx, by, cx, cy)                            \
  ((const bxr_triangle_t){ { ax, ay }, { bx, by }, { cx, cy } })
```

Constructs a `bxr_triangle_t` compound literal from its three vertices.

---


<a name="line-undefined"></a>

```cpp
#define bxr_rect_create(x, y, w, h) ((const bxr_rect_t){ x, y, w, h })
```

Constructs a `bxr_rect_t` compound literal from its top-left corner
`(x, y)`, width `w` and height `h`.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE float
bxr_rect_area(bxr_rect_t rect)
{
  return rect.w * rect.h;
}
```

`return` the area of the rectangle.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bool
bxr_rect_overlap(bxr_rect_t r1, bxr_rect_t r2)
{
  if (r1.x + r1.w < r2.x) // Check if r1 is fully to the left of r2
    return false;
  if (r2.x + r2.w < r1.x) // Check if r1 is fully to the right of r2
    return false;
  if (r1.y + r1.h < r2.y) // Check if r1 is fully above r2
    return false;
  if (r2.y + r2.h < r1.y) // Check if r1 is fully below r2
    return false;

  return true;
}
```

`return` `true` if the rectangles overlap or touch.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_rect_t
bxr_rect_get_intersection(bxr_rect_t r1, bxr_rect_t r2)
{
  float x = bxr_max(r1.x, r2.x);
  float y = bxr_max(r1.y, r2.y);
  float w = bxr_min(r1.x + r1.w, r2.x + r2.w);
  float h = bxr_min(r1.y + r1.h, r2.y + r2.h);

  if (w < x)
    w = x;

  if (h < y)
    h = y;

  return bxr_rect_create(x, y, w - x, h - y);
}
```

`return` the intersection of the two rectangles. If they do not overlap, the
returned rectangle has an area of 0.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bool
bxr_rect_contains(bxr_rect_t r1, bxr_rect_t r2)
{
  if (r2.x < r1.x)
    return false;
  if (r2.x + r2.w > r1.x + r1.w)
    return false;
  if (r2.y < r1.y)
    return false;
  if (r2.y + r2.h > r1.y + r1.h)
    return false;

  return true;
}
```

`return` `true` if `r1` completely contains `r2`, edges included.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bool
bxr_rect_contains_point(bxr_rect_t rect, bxr_vec2_t point)
{
  if (point.x < rect.x)
    return false;
  if (point.x > rect.x + rect.w)
    return false;
  if (point.y < rect.y)
    return false;
  if (point.y > rect.y + rect.h)
    return false;

  return true;
}
```

`return` `true` if the rectangle contains the point, edges included.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bool
bxr_rect_adjacent(bxr_rect_t r1, bxr_rect_t r2)
{
  bool overlap_x = r1.x <= r2.x + r2.w && r2.x <= r1.x + r1.w;
  bool overlap_y = r1.y <= r2.y + r2.h && r2.y <= r1.y + r1.h;

  // Left or right edges touching
  if (overlap_y
      && (bxr_equal(r1.x + r1.w, r2.x) || bxr_equal(r2.x + r2.w, r1.x)))
    return true;

  // Top or bottom edges touching
  if (overlap_x
      && (bxr_equal(r1.y + r1.h, r2.y) || bxr_equal(r2.y + r2.h, r1.y)))
    return true;

  return false;
}
```

`return` `true` if an edge of one rectangle lies on the same line as the
opposite edge of the other.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_rect_t
bxr_rect_expand(bxr_rect_t rect, float amount)
{
  return bxr_rect_create(rect.x - amount,
                         rect.y - amount,
                         rect.w + 2 * amount,
                         rect.h + 2 * amount);
}
```

`return` the rectangle grown by `amount` on each side, keeping its center.

---


<a name="line-undefined"></a>

```cpp
BXR_INLINE bxr_rect_t
bxr_rect_contract(bxr_rect_t rect, float amount)
{
  return bxr_rect_create(rect.x + amount,
                         rect.y + amount,
                         rect.w - 2 * amount,
                         rect.h - 2 * amount);
}
```

`return` the rectangle shrunk by `amount` on each side, keeping its center.

**Note**: the width or height becomes negative when `amount` is greater
than half of it.

---

