<a name="line-1"></a>
File `bxr_string.h`.

Copyright (c) 2025 - 2026 nsix. All rights reserved.

# String Utilities

Utilities for character classification, string manipulation, number
conversion and formatting, and pseudo-random number generation.

<a name="line-19"></a>
## Character Classification

<a name="line-23"></a>

```cpp
#define bxr_isalpha SDL_isalpha
#define bxr_isnum SDL_isalnum
#define bxr_isblank SDL_isblank
#define bxr_iscntrl SDL_iscntrl
#define bxr_isdigit SDL_isdigit
#define bxr_isxdigit SDL_isxdigit
#define bxr_ispunct SDL_ispunct
#define bxr_isspace SDL_isspace
#define bxr_isupper SDL_isupper
#define bxr_islower SDL_islower
#define bxr_isprint SDL_isprint
#define bxr_isgraph SDL_isgraph
#define bxr_toupper SDL_toupper
#define bxr_tolower SDL_tolower
```

Character classification and case conversion.

Aliases of the SDL functions of the same name, with the same signature and
behavior.

---


<a name="line-44"></a>
## Wide Strings

<a name="line-48"></a>

```cpp
#define bxr_wcslen SDL_wcslen
#define bxr_wcsnlen SDL_wcsnlen
#define bxr_wcslcpy SDL_wcslcpy
#define bxr_wcslcat SDL_wcslcat
#define bxr_wcsdup SDL_wcsdup
#define bxr_wcsstr SDL_wcsstr
#define bxr_wcsnstr SDL_wcsnstr
#define bxr_wcscmp SDL_wcscmp
#define bxr_wcsncmp SDL_wcsncmp
#define bxr_wcscasecmp SDL_wcscasecmp
#define bxr_wcsncasecmp SDL_wcsncasecmp
#define bxr_wcstol SDL_wcstol
```

Wide character (`wchar_t`) string functions.

Aliases of the SDL functions of the same name, with the same signature and
behavior.

---


<a name="line-67"></a>
## Strings

<a name="line-71"></a>

```cpp
#define bxr_strlen SDL_strlen
#define bxr_strnlen SDL_strnlen
#define bxr_strlcpy SDL_strlcpy
#define bxr_strlcat SDL_strlcat
#define bxr_strdup SDL_strdup
#define bxr_strndup SDL_strndup
#define bxr_strrev SDL_strrev
#define bxr_strupr SDL_strupr
#define bxr_strlwr SDL_strlwr
#define bxr_strchr SDL_strchr
#define bxr_strrchr SDL_strrchr
#define bxr_strstr SDL_strstr
#define bxr_strnstr SDL_strnstr
#define bxr_strcasestr SDL_strcasestr
#define bxr_strpbrk SDL_strpbrk
#define bxr_strtok SDL_strtok_r
```

Length, copy, duplication, in-place transformation and search.

Aliases of the SDL functions of the same name, with the same signature and
behavior.

---


<a name="line-94"></a>
## Number Conversion

<a name="line-98"></a>

```cpp
#define bxr_itoa SDL_itoa
#define bxr_uitoa SDL_uitoa
#define bxr_ltoa SDL_ltoa
#define bxr_ultoa SDL_ultoa
#define bxr_lltoa SDL_lltoa
#define bxr_ulltoa SDL_ulltoa
#define bxr_atoi SDL_atoi
#define bxr_atof SDL_atof
#define bxr_strtol SDL_strtol
#define bxr_strtoul SDL_strtoul
#define bxr_strtoll SDL_strtoll
#define bxr_strtoull SDL_strtoull
#define bxr_strtod SDL_strtod
```

Conversion between numbers and strings.

Aliases of the SDL functions of the same name, with the same signature and
behavior.

---


<a name="line-118"></a>
## Comparison

<a name="line-122"></a>

```cpp
#define bxr_strcmp SDL_strcmp
#define bxr_strncmp SDL_strncmp
#define bxr_strcasecmp SDL_strcasecmp
#define bxr_strncasecmp SDL_strncasecmp
```

String comparison, case-sensitive or not.

Aliases of the SDL functions of the same name, with the same signature and
behavior.

---


<a name="line-133"></a>
## Formatting

<a name="line-137"></a>

```cpp
#define bxr_vsscanf SDL_vsscanf
#define bxr_snprintf SDL_snprintf
#define bxr_swprintf SDL_swprintf
#define bxr_vsnprintf SDL_vsnprintf
#define bxr_vswprintf SDL_vswprintf
#define bxr_asprintf SDL_asprintf
#define bxr_vasprintf SDL_vasprintf
```

Formatted input and output.

Aliases of the SDL functions of the same name, with the same signature and
behavior.

---


<a name="line-151"></a>
## Random Numbers

<a name="line-155"></a>

```cpp
#define bxr_srand SDL_srand
#define bxr_rand SDL_rand
#define bxr_randf SDL_randf
#define bxr_rand_bits SDL_rand_bits
#define bxr_rand_r SDL_rand_r
#define bxr_randf_r SDL_randf_r
#define bxr_rand_bits_r SDL_rand_bits_r
```

Pseudo-random number generation. The `_r` variants use a
caller-provided state instead of the global one.

Aliases of the SDL functions of the same name, with the same signature and
behavior.

---


<a name="line-170"></a>
## Helpers

<a name="line-174"></a>

```cpp
BXR_INLINE char *bxr_strtrim(char *str)
```

Trim leading and trailing whitespace from the given string.

`str` is the string to trim. The string is modified in-place.

`return` the trimmed string, or NULL if the input string is NULL.

---


<a name="line-199"></a>

```cpp
BXR_INLINE size_t bxr_strcspn(const char *str, const char *reject)
```

Get the length of the initial segment of `str` which consists entirely of
characters not in `reject`.

`str` is the string to search through.

`reject` is the string containing the characters to reject.

`return` the length of the initial segment of `str` which consists entirely
of characters not in `reject`.

---

