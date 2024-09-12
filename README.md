# Parsing-PE-Headers

## Explanations of PE File Format

PE stand for Portable Executables is a File format for executables used by windows OS. Executables can be exe, dll, srv and many more. 
*************************




### Dos Header
DOS Header is a 64-byte long structure. Below is the structure of DOS Header.
To access the DOS header in a Portable Executable (PE) file, we can cast the starting address of the file to a PIMAGE_DOS_HEADER pointer. Since the DOS header is the first structure in the PE file, we can directly assign the starting address of the file to a dosHeader pointer.

PIMAGE_DOS_HEADER dosHeader = {};<br />
dosHeader = (PIMAGE_DOS_HEADER)fileData; 

**fileData** is the starting address of the file, obtained after loading the file into memory.
**dosHeader** is a pointer to the DOS header structure, which we create by casting fileData to the PIMAGE_DOS_HEADER type. This allows us to work with the DOS header easily.

*********************
This structure is important to PE Header but only few member of it are important.
* e_magic: This is first member of the DOS header, occupying 2 bytes (WORD). It's also known as the Magic Number, with a fixed value of 0x5A4D (or "MZ" in ASCII). This value, represented in little-endian order, acts as a signature, identifying the file as an MS-DOS executable. To get the PE header offset, use dosHeader->e_lfanew
* e_lfanew: This is the last member of DOS header, occupying 4 bytes(LONG). It holds the an offset to the start of the NT headers. It is essential for the Windows PE loader to locate the NT headers, which contain crucial information about the executable file's format and structure. To get the PE header offset, use - dosHeader->e_lfanew

### DOS Stub
The DOS stub embedded within PE file, which is part of the MS-DOS. When a PE file (like a Windows executable) is run on a DOS system, it displays a simple message like **This program cannot be run in DOS mode**, letting the user know that the file requires a Windows environment to run. DOS stub is located immediately after the DOS header and before the NT headers.

### Image NT Headers
The NT Headers in a PE (Portable Executable) file are crucial because they contain the File Header, the Optional Header (which is very important), and the Data Directories. 
To locate and access the IMAGE NT HEADER there is formula mentioned below:

PIMAGE_NT_HEADERS imageNTHeaders = {};<br />
imageNTHeaders = (PIMAGE_NT_HEADERS)((DWORD)fileData + dosHeader->e_lfanew);

**Practical Calculation of lcoating the IMAGE NT HEADERS**




## Explanation of Code

PIMAGE_DOS_HEADER dosheader //PIMAGE_DOS_HEADER is a structure defined in windows API that represents the DOS Header of PE file. dosHeader is a variable of type PIMAGE_DOS_Header, means it will point to DOS header of PE file in memory
