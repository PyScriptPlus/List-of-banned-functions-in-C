# List-of-banned-functions-in-C

```
List of Banned Functions & Safe String Alternatives
The following list of functions in the table includes the recommended replacement from the Safe Strings library, or for cases where an alternate library function is not available/appropriate, directions for using a function from the standard C library is provided.
The table includes the SDL Banned functions, and adds additional functions common in the Linux environment that, although not on the banned list, operate in a similar way to the banned functions and are therefore similarly susceptible to buffer overflow vulnerabilities. Additionally, some functions, though not banned (e.g. memset()), have a recommended replacement that safely validates parameters.
The Safe String Library functions provides links to the API Reference page [This is still a work in progress, and not all functions are documented].

​Banned Function	Replacement Function​ ​ ​ ​ ​ 
​alloca()
_alloca()	​use malloc() or new() which create memory on the heap, instead of the alloc functions which allocate memory on the stack, as alloc can allow damage to stack frames
​scanf()
wscanf()
sscanf()
swscanf()
vscanf()
vsscanf()	​use fgets() instead of scanf() functions
strlen()
wcslen()	​strnlen_s()
wcsnlen_s()
strtok()
strtok_r()
wcstok()	​strtok_s()
​strcat()
strncat()
wcscat()
wcsncat()	strcat_s(), ​strncat_s(), strlcat()*
wcscat_s(), wcsncat_s()
​strcpy()
strncpy()
wcscpy()
wcsncpy()	​strcpy_s() strncpy_s(), strlcpy()*
wc​scpy_s(), wcsncpy_s()
​​memcpy()
wmemcpy()	​memcpy_s() wmemcpy_s()
​​stpcpy()
stpncpy()
wcpcpy()
wcpncpy()	stpcpy_s(), stpncpy_s()
wcpcpy_s(), wcpncpy_s()
memmove()
wmemmove()	​memmove_s() wmemmove_s()
memcmp()
wmemcmp()	​memcmp_s() wmemcmp_s()
me​mset()
wmemset()	​memset_s() wmemset_s()
gets()	​use fgets() instead
sprintf​()
vsprintf()
swprintf()
vswprintf()	​use snprintf() or one of the specialized (non-varg) versions in the safe string library
snprintf()
vsnprintf()	​Consider using a wrapper function that avoids the vargs construct and uses compile-time checks on the parameters passed into snprintf(). See example functions in the Safe String library.  
​realpath()	​continue to use realpath() but use NULL for the second parameter to force allocation of an appropriate sized buffer on the heap.
getwd()
​use getcwd() instead because it checks the buffer size
wctomb()
wcrtomb()
wcstombs()
wcsrtombs()
wcsnrtombs()
​The wide-character to multi-byte string conversion routines can create buffer overflows, but currently no alternatives are provided. If enough requests are made that indicate these functions are in wide use and safer alternatives are needed, these functions may be added to the library extensions.

Note *: strlcpy() and strlcat() are not provided in the Safe String Library, but are functions often found in the kernel library, and provide safe string operation, meaning that they do not overrun the buffer size, and they always NULL terminate the result, and the length of the composed string is also returned. These functions are normally considered safer replacements for strcpy() and strcat(). Again, strlcpy() and strlcat() are NOT included in the Safe String Library, but may be found in your version of Linux standard libraries.






```
