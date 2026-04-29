# List of Banned Functions & Safe String Alternatives

The following list of functions in the table includes the recommended replacement from the Safe Strings library, or for cases where an alternate library function is not available/appropriate, directions for using a function from the standard C library is provided.
The table includes the SDL Banned functions, and adds additional functions common in the Linux environment that, although not on the banned list, operate in a similar way to the banned functions and are therefore similarly susceptible to buffer overflow vulnerabilities. Additionally, some functions, though not banned (e.g. memset()), have a recommended replacement that safely validates parameters.

| Banned Function | Replacement Function |
|----------------|----------------------|
| `alloca()`<br>`_alloca()` | use `malloc()` or `new()` which create memory on the heap, instead of the alloc functions which allocate memory on the stack, as alloc can allow damage to stack frames |
| `scanf()`<br>`wscanf()`<br>`sscanf()`<br>`swscanf()`<br>`vscanf()`<br>`vsscanf()` | use `fgets()` instead of scanf() functions |
| `strlen()`<br>`wcslen()` | `strnlen_s()`<br>`wcsnlen_s()` |
| `strtok()`<br>`strtok_r()`<br>`wcstok()` | `strtok_s()` |
| `strcat()`<br>`strncat()`<br>`wcscat()`<br>`wcsncat()` | `strcat_s()`, `strncat_s()`, `strlcat()`*<br>`wcscat_s()`, `wcsncat_s()` |
| `strcpy()`<br>`strncpy()`<br>`wcscpy()`<br>`wcsncpy()` | `strcpy_s()`, `strncpy_s()`, `strlcpy()`*<br>`wcscpy_s()`, `wcsncpy_s()` |
| `memcpy()`<br>`wmemcpy()` | `memcpy_s()`<br>`wmemcpy_s()` |
| `stpcpy()`<br>`stpncpy()`<br>`wcpcpy()`<br>`wcpncpy()` | `stpcpy_s()`, `stpncpy_s()`<br>`wcpcpy_s()`, `wcpncpy_s()` |
| `memmove()`<br>`wmemmove()` | `memmove_s()`<br>`wmemmove_s()` |
| `memcmp()`<br>`wmemcmp()` | `memcmp_s()`<br>`wmemcmp_s()` |
| `memset()`<br>`wmemset()` | `memset_s()`<br>`wmemset_s()` |
| `gets()` | use `fgets()` instead |
| `sprintf()`<br>`vsprintf()`<br>`swprintf()`<br>`vswprintf()` | use `snprintf()` or one of the specialized (non-varg) versions in the safe string library |
| `snprintf()`<br>`vsnprintf()` | Consider using a wrapper function that avoids the vargs construct and uses compile-time checks on the parameters passed into `snprintf()`. See example functions in the Safe String library. |
| `realpath()` | continue to use `realpath()` but use NULL for the second parameter to force allocation of an appropriate sized buffer on the heap. |
| `getwd()` | use `getcwd()` instead because it checks the buffer size |
| `wctomb()`<br>`wcrtomb()`<br>`wcstombs()`<br>`wcsrtombs()`<br>`wcsnrtombs()` | The wide-character to multi-byte string conversion routines can create buffer overflows, but currently no alternatives are provided. If enough requests are made that indicate these functions are in wide use and safer alternatives are needed, these functions may be added to the library extensions. |

*Note *:** `strlcpy()` and `strlcat()` are not provided in the Safe String Library, but are functions often found in the kernel library, and provide safe string operation, meaning that they do not overrun the buffer size, and they always NULL terminate the result, and the length of the composed string is also returned. These functions are normally considered safer replacements for `strcpy()` and `strcat()`. Again, `strlcpy()` and `strlcat()` are NOT included in the Safe String Library, but may be found in your version of Linux standard libraries.


## نسخه فارسی (Persian Version)

# فهرست توابع ممنوعه و جایگزین‌های امن

جدول زیر شامل توابع ممنوعه و جایگزین‌های پیشنهادی از کتابخانه Safe Strings است. در مواردی که جایگزین مستقیمی وجود ندارد، راهنمای استفاده از توابع استاندارد C ارائه شده است. این فهرست شامل توابع ممنوعه SDL و توابع رایج در محیط لینوکس است که مشابه آن‌ها عمل کرده و آسیب‌پذیر هستند.

| تابع ممنوعه | تابع جایگزین |
|-------------|---------------|
| `alloca()`<br>`_alloca()` | از `malloc()` یا `new()` در هپ (heap) استفاده کنید، نه تخصیص روی پشته (stack) چون ممکن است به قاب‌های پشته آسیب برساند. |
| `scanf()`<br>`wscanf()`<br>`sscanf()`<br>`swscanf()`<br>`vscanf()`<br>`vsscanf()` | به جای توابع scanf از `fgets()` استفاده کنید. |
| `strlen()`<br>`wcslen()` | `strnlen_s()`<br>`wcsnlen_s()` |
| `strtok()`<br>`strtok_r()`<br>`wcstok()` | `strtok_s()` |
| `strcat()`<br>`strncat()`<br>`wcscat()`<br>`wcsncat()` | `strcat_s()`، `strncat_s()`، `strlcat()`*<br>`wcscat_s()`، `wcsncat_s()` |
| `strcpy()`<br>`strncpy()`<br>`wcscpy()`<br>`wcsncpy()` | `strcpy_s()`، `strncpy_s()`، `strlcpy()`*<br>`wcscpy_s()`، `wcsncpy_s()` |
| `memcpy()`<br>`wmemcpy()` | `memcpy_s()`<br>`wmemcpy_s()` |
| `stpcpy()`<br>`stpncpy()`<br>`wcpcpy()`<br>`wcpncpy()` | `stpcpy_s()`، `stpncpy_s()`<br>`wcpcpy_s()`، `wcpncpy_s()` |
| `memmove()`<br>`wmemmove()` | `memmove_s()`<br>`wmemmove_s()` |
| `memcmp()`<br>`wmemcmp()` | `memcmp_s()`<br>`wmemcmp_s()` |
| `memset()`<br>`wmemset()` | `memset_s()`<br>`wmemset_s()` |
| `gets()` | از `fgets()` استفاده کنید. |
| `sprintf()`<br>`vsprintf()`<br>`swprintf()`<br>`vswprintf()` | از `snprintf()` یا نسخه‌های غیر varg کتابخانه Safe Strings استفاده کنید. |
| `snprintf()`<br>`vsnprintf()` | توصیه می‌شود از یک تابع wrapper استفاده کنید که از سازنده varg اجتناب کرده و بررسی‌های زمان کامپایل را انجام دهد. نمونه در کتابخانه Safe Strings موجود است. |
| `realpath()` | همچنان از `realpath()` استفاده کنید ولی پارامتر دوم را `NULL` قرار دهید تا بافر مناسب روی هپ تخصیص یابد. |
| `getwd()` | به جای آن از `getcwd()` استفاده کنید چون اندازه بافر را بررسی می‌کند. |
| `wctomb()`<br>`wcrtomb()`<br>`wcstombs()`<br>`wcsrtombs()`<br>`wcsnrtombs()` | روال‌های تبدیل رشته پهن‌کاراکتر به مولتی‌بایت می‌توانند باعث سرریز بافر شوند، اما در حال حاضر جایگزینی ارائه نشده است. در صورت درخواست زیاد ممکن است به کتابخانه اضافه شوند. |

*یادداشت:* توابع `strlcpy()` و `strlcat()` در کتابخانه Safe Strings وجود ندارند، اما معمولاً در کتابخانه کرنل لینوکس یافت می‌شوند و کارکرد امنی دارند (همیشه نتیجه را NULL-terminated کرده و طول را برمی‌گردانند). این توابع جایگزین‌های امنی برای `strcpy()` و `strcat()` در نظر گرفته می‌شوند.
