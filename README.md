# XV6 File Size Extension Project

## Description

This README documents the successful completion of the XV6 file size extension project. The objective was to increase the maximum size of an XV6 file from 71,680 bytes to approximately 8.5 megabytes. This was achieved by implementing a doubly-indirect block in each inode structure, significantly expanding the file system's capacity.

## Project Overview

### Modifications Made

1. **File System Initialization:**
   - Updated `Makefile`: Set `CPUS` to 1 for optimization.
   - Added `QEMUEXTRA = -snapshot` to the Makefile for faster emulation.
   - Modified `param.h` to increase `FSSIZE` to 20,000 blocks.

2. **Understanding and Testing:**
   - Analyzed `large.c` for its operation in creating the largest possible file in the original XV6.
   - Conducted tests with the 'large' program to verify the original file size limit of 140 blocks.

### Core Changes

1. **File System Structure:**
   - Modified the inode structure (`struct dinode` in `fs.h`), reducing direct blocks to 11 and adding a doubly-indirect block.
   - Adapted `struct inode` in `file.h` to mirror changes in `struct dinode`.

2. **Block Mapping:**
   - Reworked `bmap()` in `fs.c` to handle doubly-indirect blocks.
   - Implemented logic for mapping logical block numbers to disk block numbers with the new structure.

### Testing and Validation

- Ran `large` program on the modified XV6. Confirmed the creation of files up to 16523 blocks (~8.5 MB).
- Ensured stability and integrity of the file system during extensive read/write operations.

## Hints and Tips

- Understanding `bmap()` is crucial for grasping the mapping between different types of blocks.
- Deletion of files with doubly-indirect blocks does not require modifications.
- Recreate `fs.img` if there are changes to `NDIRECT` or after file system crashes.
- Remember to release blocks (`brelse()`) after usage to avoid memory leaks.

## Conclusion

This project successfully extends the XV6 file system's capabilities, allowing for larger file sizes and demonstrating advanced file system concepts.

