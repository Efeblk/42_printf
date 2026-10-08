# ft_printf

A small C implementation of the core `printf` conversions, kept as a 42 project repository. The public function writes to standard output and returns its character count.

```c
int ft_printf(const char *format, ...);
```

## Supported conversions

| Conversion | Output |
| --- | --- |
| `%c` | A single character |
| `%s` | A string |
| `%p` | A pointer value in hexadecimal with a `0x` prefix |
| `%d`, `%i` | A signed decimal integer |
| `%u` | An unsigned decimal integer |
| `%x` | An unsigned hexadecimal integer, lowercase |
| `%X` | An unsigned hexadecimal integer, uppercase |
| `%%` | A literal percent sign |

The implementation does not parse field width, precision, length modifiers, or formatting flags. The root Makefile has no bonus target.

## Build

Requires GCC, Make, `ar`, and a system providing POSIX `write`.

**Current source note:** `ft_printf.c` begins with a stray comma before its opening comment. A source rebuild requires removing that comma first; the commands below describe the existing Makefile after that correction.

```sh
git clone https://github.com/Efeblk/42_printf.git
cd 42_printf
make re
```

The Makefile compiles with `-Wall -Wextra -Werror` and creates `libftprintf.a`.

| Command | Purpose |
| --- | --- |
| `make` | Build the library |
| `make clean` | Remove object files |
| `make fclean` | Remove object files and the library |
| `make re` | Rebuild from source |

## Usage

Save this as `main.c` in the repository root:

```c
#include "ft_printf.h"

int main(void)
{
    ft_printf("Hello, %s! Number: %d, hex: %x, progress: 100%%\n",
        "world", 42, 42u);
    return (0);
}
```

After rebuilding the library:

```sh
gcc -Wall -Wextra -Werror main.c libftprintf.a -o example
./example
```

Expected output for this example:

```text
Hello, world! Number: 42, hex: 2a, progress: 100%
```

## Repository guide

- `ft_printf.c` — format scanning and variadic argument dispatch.
- `ft_numbers.c` — decimal, hexadecimal, and pointer output.
- `ft_words.c` — character and string output.
- `ft_printf.h` — public function and helper declarations.
- `printfTester/` — bundled third-party tester; see its [README](printfTester/README.md).

## Credits

The source file headers credit `prossi`. The bundled tester includes its own documentation and credits; preserve those when reusing the project.
