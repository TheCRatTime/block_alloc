# block_alloc
**block_alloc** - allocate memory by blocks.

## Description
This is a small block allocator, that can allocate and free blocks
without any order. Maximal block size: 16.

### Features
- **C89**/**ANSI C** code standard.
- **stb-style** library.
- **O(1)** allocaton.
- **Clang -Weverything flag quiet**: but with
  - **-Wno-unsafe-buffer-usage**: warning on *buffer[0]* / *ptr + 1*
  (pointer arithmetic).
  - **-Wno-padded**.

### Quick start
```c
#define BLOCK_ALLOC_SOURCE
#include "../include/block_alloc.h"

#include <stdio.h>

int main(void) {
  /* Creating 'plate' */
  PlateStorage plate_storage;
  Plate plate;
  
  int* data1 = NULL;
  int* data2 = NULL;
  int* data3 = NULL;

  InitPlate(&plate, plate_storage.array);

  data1 = PlateAlloc(&plate); /* O(1) allocate */
  data2 = PlateAlloc(&plate); /* O(1) allocate */

  *data1 = 123;
  *data2 = 456;

  printf("data1: 0x%p:%d, data2: 0x%p:%d\n", data1, *data1, data2, *data2);

  /* O(1) free: */
  PlateFree(&plate, data1);

  data3 = (int*)PlateAlloc(&plate);

  *data3 = 789;

  printf("data3: 0x%p:%d\n", data3, *data3);

  /* ... (free) ... */
  return 0;
}
```

### Building
Needed:
- C Compiler
- CMake 3.10 and greater
- GNU Make

```bash
cmake -B build
cd build/
make
```

### Examples
You can find examples in `examples/` directory.

### Authors
TheCRatTime

### License
Project is under Apache 2.0 license
