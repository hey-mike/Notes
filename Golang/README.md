# Golang Notes

## New and make

The main difference between new and make is that variables created with make are properly initialized without just zeroing the allocated memory space. Additionally, make can only be applied to maps, channels, and slices, and it does not return a memory address, which means that make does not return a pointer.
