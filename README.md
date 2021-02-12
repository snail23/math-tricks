# Math Tricks <a href="https://discord.gg/caUF3Pm"><img align="right" src="https://i.imgur.com/DFL4Iss.png"></a>
Some common, some somewhat obscure. Maybe you'll learn something new and increase the performance of your program! Open an issue if you know one that isn't on this list.

Note: your compiler might already be implementing some of these for you so don't panic if you don't see a performance increase.

# Check for zero bytes
|           |                                                                     |
| --------- | ------------------------------------------------------------------- |
| char      | `if(!data)`                                                         |
| short     | `if(!(((data - 0x01010) & ~data) & 0x8080))`                        |
| long      | `if(!(((data - 0x01010101) & ~data) & 0x80808080))`                 |
| long long | `if(!(((data - 0x0101010101010101) & ~data) & 0x8080808080808080))` |

# Division
| Old       | New                                     | Note                                             |
| --------- | --------------------------------------- | ------------------------------------------------ |
|           | c(x) = `round((1 / x) * 0x100000000)`   | Constant used for division tricks                |
| `x / y`   | `(x * c) >> 32`                         | More useful for non-powers of 2                  |
| `x / 2`   | `x >> 1`                                |                                                  |
| `x / 4`   | `x >> 2`                                |                                                  |
| `x / 8`   | `x >> 3`                                |                                                  |
| `x / 10`  | `(x * 0x1999999Aull) >> 32`             |                                                  |
| `x / 16`  | `x >> 4`                                |                                                  |
| `x / 32`  | `x >> 5`                                |                                                  |
| `x / 64`  | `x >> 6`                                |                                                  |
| `x / 128` | `x >> 7`                                |                                                  |
| `x / 256` | `x >> 8`                                |                                                  |

# Modulo
| Old       | New                                     | Note                                             |
| --------- | --------------------------------------- | ------------------------------------------------ |
|           | c(x) = `round((1 / x) * 0x100000000)`   | Constant used for modulo tricks                  |
| `x % y`   | `x & (y - 1)`                           | Powers of 2 only                                 |
| `x % y`   | `x - (((x * c) >> 32) * y)`             | More useful for non-powers of 2                  |

# Multiplication
| Old       | New                                     |
| --------- | --------------------------------------- |
| `x * 2`   | `x << 1`                                |
| `x * 4`   | `x << 2`                                |
| `x * 8`   | `x << 3`                                |
| `x * 16`  | `x << 4`                                |
| `x * 32`  | `x << 5`                                |
| `x * 64`  | `x << 6`                                |
| `x * 128` | `x << 7`                                |
| `x * 256` | `x << 8`                                |

# Swap values with only two variables
```
x ^= y
y ^= x
x ^= y
```
