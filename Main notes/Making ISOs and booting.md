# General
- The first stage bootloader usually resides in BootROM (Read-Only Memory) on-chip and it initializes hardware then loads the next stage
- The next stage is the first user-controlled bootloader can be multi-stage as well
- U-boot supports loading from various storage types and it supports both raw storage and filesystems
- Also supports network commands but only UDP protocol
- Device trees describe the hardware, it is an acyclic graph where each node represents a specific thing and each property describes aspects of that thing, nodes can also contain child nodes, phandles are references to other nodes
- 

# Le Potato board's case
- `mmc rescan` looks for available eMMC chips or SD cards
- `booti` command for booting from ARM64 images

# Buildroot
- 