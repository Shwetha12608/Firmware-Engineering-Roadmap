This project documents the deep-dive into C pointers from a hardware perspective. The focus was shifted from simple syntax to System-Level Architecture, specifically targeting memory safety, pointer levels of indirection, and CPU endianness.

**1. Memory Mapping & Architecture:**
Pointer Sizing: Verified that on 32-bit architectures (e.g., ARM Cortex, ESP32), a pointer occupies exactly 4 bytes. This is a hardware constraint dictated by the address bus width.

Indirection Levels:

- Single Pointer (*p): Efficiently managing data by reference.

- Double Pointer (**q): Utilized for modifying pointer targets across function scopes—critical for RTOS task management and dynamic buffer resets.

**2. Defensive Programming (Corporate Standards):**

- The NULL-Check Protocol: Implemented logic to verify memory addresses before dereferencing. In firmware, an unchecked NULL pointer leads to HardFault exceptions and system hangs.

- Initialization: Adopted the standard of initializing pointers to NULL to prevent Dangling Pointers and unintentional memory corruption.

**3. Hardware Interaction: Byte-Level Inspection:**

- Type Casting: Explored casting int* to char* to bypass data boundaries.

- Endianness Discovery: Used pointer arithmetic to inspect how the CPU stores multi-byte integers.

- Insight: Most modern MCUs use Little-Endian, where the Least Significant Byte (LSB) is stored at the lowest memory address.
