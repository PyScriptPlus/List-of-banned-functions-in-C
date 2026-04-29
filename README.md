# List of Banned Functions & Safe String Alternatives

The following list of functions in the table includes the recommended replacement from the Safe Strings library, or for cases where an alternate library function is not available/appropriate, directions for using a function from the standard C library is provided.
The table includes the SDL Banned functions, and adds additional functions common in the Linux environment that, although not on the banned list, operate in a similar way to the banned functions and are therefore similarly susceptible to buffer overflow vulnerabilities. Additionally, some functions, though not banned (e.g. memset()), have a recommended replacement that safely validates parameters.

| Banned Function | Replacement Function |
|----------------|----------------------|
| `alloca()`<br>`_alloca()` | use `malloc()` or `new()` which create memory on the heap, instead of the alloc functions which allocate memory on the stack, as alloc can allow damage to stack frames |
| `scanf()`<br>`wscanf()`<br>`sscanf()`<br>`swscanf()`<br>`vscanf()`<br>`vsscanf()` | use `fgets()` instead of `scanf()` functions |
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

<div dir="rtl" align="right">

## نسخه فارسی (Persian Version)

# فهرست توابع ممنوعه و جایگزین‌های امن

جدول زیر شامل توابع ممنوعه و جایگزین‌های پیشنهادی از کتابخانه Safe Strings است. در مواردی که جایگزین مستقیمی وجود ندارد، راهنمای استفاده از توابع استاندارد C ارائه شده است. این فهرست شامل توابع ممنوعه SDL و توابع رایج در محیط لینوکس است که مشابه آن‌ها عمل کرده و آسیب‌پذیر هستند.

<table dir="rtl" style="text-align: right;">
  <thead>
    <tr><th style="text-align: right;">تابع ممنوعه</th><th style="text-align: right;">تابع جایگزین</th></tr>
  </thead>
  <tbody>
    <tr><td style="text-align: right;"><span dir="ltr"><code>alloca()</code><br><code>_alloca()</code></span></td><td style="text-align: right;">از <span dir="ltr"><code>malloc()</code></span> یا <span dir="ltr"><code>new()</code></span> در هپ (heap) استفاده کنید، نه تخصیص روی پشته (stack) چون ممکن است به قاب‌های پشته آسیب برساند.</td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>scanf()</code><br><code>wscanf()</code><br><code>sscanf()</code><br><code>swscanf()</code><br><code>vscanf()</code><br><code>vsscanf()</code></span></td><td style="text-align: right;">به جای توابع scanf() از <span dir="ltr"><code>fgets()</code></span> استفاده کنید.</td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>strlen()</code><br><code>wcslen()</code></span></td><td style="text-align: right;"><span dir="ltr"><code>strnlen_s()</code><br><code>wcsnlen_s()</code></span></td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>strtok()</code><br><code>strtok_r()</code><br><code>wcstok()</code></span></td><td style="text-align: right;"><span dir="ltr"><code>strtok_s()</code></span></td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>strcat()</code><br><code>strncat()</code><br><code>wcscat()</code><br><code>wcsncat()</code></span></td><td style="text-align: right;"><span dir="ltr"><code>strcat_s()</code></span>، <span dir="ltr"><code>strncat_s()</code></span>، <span dir="ltr"><code>strlcat()</code></span>*<br><span dir="ltr"><code>wcscat_s()</code></span>، <span dir="ltr"><code>wcsncat_s()</code></span></td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>strcpy()</code><br><code>strncpy()</code><br><code>wcscpy()</code><br><code>wcsncpy()</code></span></td><td style="text-align: right;"><span dir="ltr"><code>strcpy_s()</code></span>، <span dir="ltr"><code>strncpy_s()</code></span>، <span dir="ltr"><code>strlcpy()</code></span>*<br><span dir="ltr"><code>wcscpy_s()</code></span>، <span dir="ltr"><code>wcsncpy_s()</code></span></td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>memcpy()</code><br><code>wmemcpy()</code></span></td><td style="text-align: right;"><span dir="ltr"><code>memcpy_s()</code></span><br><span dir="ltr"><code>wmemcpy_s()</code></span></td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>stpcpy()</code><br><code>stpncpy()</code><br><code>wcpcpy()</code><br><code>wcpncpy()</code></span></td><td style="text-align: right;"><span dir="ltr"><code>stpcpy_s()</code></span>، <span dir="ltr"><code>stpncpy_s()</code></span><br><span dir="ltr"><code>wcpcpy_s()</code></span>، <span dir="ltr"><code>wcpncpy_s()</code></span></td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>memmove()</code><br><code>wmemmove()</code></span></td><td style="text-align: right;"><span dir="ltr"><code>memmove_s()</code></span><br><span dir="ltr"><code>wmemmove_s()</code></span></td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>memcmp()</code><br><code>wmemcmp()</code></span></td><td style="text-align: right;"><span dir="ltr"><code>memcmp_s()</code></span><br><span dir="ltr"><code>wmemcmp_s()</code></span></td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>memset()</code><br><code>wmemset()</code></span></td><td style="text-align: right;"><span dir="ltr"><code>memset_s()</code></span><br><span dir="ltr"><code>wmemset_s()</code></span></td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>gets()</code></span></td><td style="text-align: right;">از <span dir="ltr"><code>fgets()</code></span> استفاده کنید.</td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>sprintf()</code><br><code>vsprintf()</code><br><code>swprintf()</code><br><code>vswprintf()</code></span></td><td style="text-align: right;">از <span dir="ltr"><code>snprintf()</code></span> یا نسخه‌های غیر varg کتابخانه Safe Strings استفاده کنید.</td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>snprintf()</code><br><code>vsnprintf()</code></span></td><td style="text-align: right;">توصیه می‌شود از یک تابع wrapper استفاده کنید که از سازنده varg اجتناب کرده و بررسی‌های زمان کامپایل را انجام دهد. نمونه در کتابخانه Safe Strings موجود است.</td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>realpath()</code></span></td><td style="text-align: right;">همچنان از <span dir="ltr"><code>realpath()</code></span> استفاده کنید ولی پارامتر دوم را <span dir="ltr"><code>NULL</code></span> قرار دهید تا بافر مناسب روی هپ تخصیص یابد.</td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>getwd()</code></span></td><td style="text-align: right;">به جای آن از <span dir="ltr"><code>getcwd()</code></span> استفاده کنید چون اندازه بافر را بررسی می‌کند.</td></tr>
    <tr><td style="text-align: right;"><span dir="ltr"><code>wctomb()</code><br><code>wcrtomb()</code><br><code>wcstombs()</code><br><code>wcsrtombs()</code><br><code>wcsnrtombs()</code></span></td><td style="text-align: right;">روال‌های تبدیل رشته پهن‌کاراکتر به مولتی‌بایت می‌توانند باعث سرریز بافر شوند، اما در حال حاضر جایگزینی ارائه نشده است. در صورت درخواست زیاد ممکن است به کتابخانه اضافه شوند.</td></tr>
  </tbody>
</table>

> **یادداشت:** توابع <span dir="ltr"><code>strlcpy()</code></span> و <span dir="ltr"><code>strlcat()</code></span> در کتابخانه Safe Strings وجود ندارند، اما معمولاً در کتابخانه کرنل لینوکس یافت می‌شوند و کارکرد امنی دارند (همیشه نتیجه را NULL-terminated کرده و طول را برمی‌گردانند). این توابع جایگزین‌های امنی برای <span dir="ltr"><code>strcpy()</code></span> و <span dir="ltr"><code>strcat()</code></span> در نظر گرفته می‌شوند.

</div>
