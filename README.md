# Parsing-PE-Headers

## Explanations of PE File Format

PE stand for Portable Executables is a File format for executables used by windows OS. Executables can be exe, dll, srv and many more. 
*************************




### Dos Header
DOS Header is a 64-byte long structure. Below is the structure of DOS Header.
*********************
This structure is important to PE Header but only few member of it are important.
* e_magic: This is first member of the DOS header, occupying 2 bytes (WORD). It's also known as the Magic Number, with a fixed value of 0x5A4D (or "MZ" in ASCII). This value, represented in little-endian order, acts as a signature, identifying the file as an MS-DOS executable.
* e_lfanew: This is the last member of DOS header, occupying 4 bytes(LONG). It holds the an offset to the start of the NT headers. It is essential for the Windows PE loader to locate the NT headers, which contain crucial information about the executable file's format and structure.

### DOS Stub
The DOS stub embedded within PE file, which is part of the MS-DOS. When a PE file (like a Windows executable) is run on a DOS system, it displays a simple message like **This program cannot be run in DOS mode**, letting the user know that the file requires a Windows environment to run. DOS stub is located immediately after the DOS header and before the NT headers.




## Explanation of Code

PIMAGE_DOS_HEADER dosheader //PIMAGE_DOS_HEADER is a structure defined in windows API that represents the DOS Header of PE file. dosHeader is a variable of type PIMAGE_DOS_Header, means it will point to DOS header of PE file in memory
