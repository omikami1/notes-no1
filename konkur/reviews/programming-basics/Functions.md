عالی! یه جمع‌بندی کامل و تستی از توابع مهم C در قالب جدول می‌سازم. چون تعداد توابع زیاده، به بخش‌های منطقی تقسیم می‌کنم تا قابل ذخیره و مرور باشه.

---

# ۱) توابع `<string.h>` — کار با رشته

| تابع | کار | ورودی | خروجی | مثال |
|------|------|--------|--------|-------|
| `strlen(s)` | طول رشته | رشته | تعداد کاراکتر (بدون `\0`) | `strlen("hello")` → `5` |
| `strcpy(d, s)` | کپی رشته | دو رشته | pointer به d | `strcpy(d,"hi")` → `d="hi"` |
| `strncpy(d, s, n)` | کپی n کاراکتر | دو رشته + عدد | pointer به d | `strncpy(d,"hello",3)` → `"hel"` |
| `strcat(d, s)` | الحاق | دو رشته | pointer به d | `strcat("hi ","there")` → `"hi there"` |
| `strncat(d, s, n)` | الحاق n کاراکتر | دو رشته + عدد | pointer به d | `strncat("hi ","there",3)` → `"hi the"` |
| `strcmp(a, b)` | مقایسه | دو رشته | 0=برابر، <0، >0 | `strcmp("a","b")` → `<0` |
| `strncmp(a, b, n)` | مقایسه n کاراکتر | دو رشته + عدد | مثل strcmp | `strncmp("abc","abd",2)` → `0` |
| `strchr(s, c)` | اولین c | رشته + کاراکتر | pointer یا NULL | `strchr("hello",'l')` → `"llo"` |
| `strrchr(s, c)` | آخرین c | رشته + کاراکتر | pointer یا NULL | `strrchr("hello",'l')` → `"lo"` |
| `strstr(s, sub)` | زیررشته | دو رشته | pointer یا NULL | `strstr("hello","ll")` → `"llo"` |
| `strtok(s, delim)` | تقسیم رشته | رشته + جداکننده | token بعدی یا NULL | `strtok("a,b,c",",")` → `"a"` |
| `strspn(s, accept)` | طول prefix مجاز | دو رشته | عدد | `strspn("abc123","abc")` → `3` |
| `strcspn(s, reject)` | طول تا اولین غیرمجاز | دو رشته | عدد | `strcspn("abc\n","\n")` → `3` |
| `strpbrk(s, accept)` | اولین کاراکتر از مجموعه | دو رشته | pointer یا NULL | `strpbrk("abc","cb")` → `"bc"` |
| `memcpy(d, s, n)` | کپی حافظه | دو pointer + عدد | pointer به d | کپی هر نوع داده |
| `memmove(d, s, n)` | کپی با overlap | دو pointer + عدد | pointer به d | امن برای همپوشانی |
| `memset(d, c, n)` | پر کردن | pointer + کاراکتر + عدد | pointer به d | `memset(a,0,10)` → صفر کردن |
| `memcmp(a, b, n)` | مقایسه حافظه | دو pointer + عدد | مثل strcmp | مقایسه بایت‌به‌بایت |

---

# ۲) توابع `<ctype.h>` — کار با کاراکترها

| تابع | کار | ورودی | خروجی | مثال |
|------|------|--------|--------|-------|
| `isalpha(c)` | حرف الفبا؟ | کاراکتر | غیرصفر یا 0 | `isalpha('a')` → `true` |
| `isdigit(c)` | رقم؟ | کاراکتر | غیرصفر یا 0 | `isdigit('5')` → `true` |
| `isalnum(c)` | حرف یا رقم؟ | کاراکتر | غیرصفر یا 0 | `isalnum('a')` → `true` |
| `isspace(c)` | فاصله/تب/نیو لاین؟ | کاراکتر | غیرصفر یا 0 | `isspace('\n')` → `true` |
| `isupper(c)` | حرف بزرگ؟ | کاراکتر | غیرصفر یا 0 | `isupper('A')` → `true` |
| `islower(c)` | حرف کوچک؟ | کاراکتر | غیرصفر یا 0 | `islower('a')` → `true` |
| `ispunct(c)` | علامت نگارشی؟ | کاراکتر | غیرصفر یا 0 | `ispunct('!')` → `true` |
| `isxdigit(c)` | رقم هگز؟ | کاراکتر | غیرصفر یا 0 | `isxdigit('F')` → `true` |
| `isprint(c)` | قابل چاپ؟ | کاراکتر | غیرصفر یا 0 | `isprint(' ')` → `true` |
| `iscntrl(c)` | کنترلی؟ | کاراکتر | غیرصفر یا 0 | `iscntrl('\n')` → `true` |
| `toupper(c)` | به بزرگ | کاراکتر | کاراکتر | `toupper('a')` → `'A'` |
| `tolower(c)` | به کوچک | کاراکتر | کاراکتر | `tolower('A')` → `'a'` |

---

# ۳) توابع ورودی/خروجی `<stdio.h>`

## ۳-۱) کاراکتری

| تابع | کار | ورودی | خروجی | مثال |
|------|------|--------|--------|-------|
| `getchar()` | یک کاراکتر از stdin | — | int (کاراکتر یا EOF) | `c=getchar()` |
| `putchar(c)` | چاپ کاراکتر | کاراکتر | int | `putchar('A')` |
| `getc(f)` | کاراکتر از فایل | FILE* | int | `getc(fp)` |
| `putc(c, f)` | کاراکتر در فایل | کاراکتر + FILE* | int | `putc('A',fp)` |
| `fgetc(f)` | مثل getc | FILE* | int | `fgetc(fp)` |
| `fputc(c, f)` | مثل putc | کاراکتر + FILE* | int | `fputc('A',fp)` |

## ۳-۲) رشته‌ای

| تابع | کار | ورودی | خروجی | مثال |
|------|------|--------|--------|-------|
| `gets(s)` | خواندن خط (حذف شده) | بافر | pointer یا NULL | ❌ استفاده نکن |
| `fgets(s, n, f)` | خواندن خط امن | بافر + عدد + FILE* | pointer یا NULL | `fgets(b,100,stdin)` |
| `puts(s)` | چاپ + `\n` | رشته | int | `puts("hi")` → `hi\n` |
| `fputs(s, f)` | چاپ بدون `\n` | رشته + FILE* | int | `fputs("hi",stdout)` |

## ۳-۳) قالبی (Formatted)

| تابع | کار | ورودی | خروجی | مثال |
|------|------|--------|--------|-------|
| `printf(fmt, ...)` | چاپ قالب‌دار | قالب + مقادیر | int | `printf("%d",5)` |
| `scanf(fmt, ...)` | خواندن قالب‌دار | قالب + آدرس‌ها | int | `scanf("%d",&n)` |
| `sprintf(b, fmt, ...)` | چاپ در رشته | بافر + قالب | int | `sprintf(b,"%d",5)` |
| `snprintf(b, n, fmt, ...)` | نسخه امن | بافر + عدد + قالب | int | `snprintf(b,10,"%d",5)` |
| `sscanf(s, fmt, ...)` | خواندن از رشته | رشته + قالب | int | `sscanf("5","%d",&n)` |
| `fprintf(f, fmt, ...)` | چاپ در فایل | FILE* + قالب | int | `fprintf(fp,"%d",5)` |
| `fscanf(f, fmt, ...)` | خواندن از فایل | FILE* + قالب | int | `fscanf(fp,"%d",&n)` |

## ۳-۴) فایل

| تابع                    | کار            | ورودی                         | خروجی         | مثال                   |
| ----------------------- | -------------- | ----------------------------- | ------------- | ---------------------- |
| `fopen(name, mode)`     | باز کردن فایل  | نام + حالت                    | FILE* یا NULL | `fopen("a.txt","r")`   |
| `fclose(f)`             | بستن           | FILE*                         | 0 یا EOF      | `fclose(fp)`           |
| `fread(buf, sz, n, f)`  | خواندن بلوکی   | بافر + اندازه + تعداد + FILE* | تعداد آیتم    | خواندن باینری          |
| `fwrite(buf, sz, n, f)` | نوشتن بلوکی    | بافر + اندازه + تعداد + FILE* | تعداد آیتم    | نوشتن باینری           |
| `fseek(f, off, whence)` | جابه‌جایی      | FILE* + offset + مبدأ         | 0 یا -1       | `fseek(fp,0,SEEK_SET)` |
| `ftell(f)`              | موقعیت فعلی    | FILE*                         | long          | `ftell(fp)`            |
| `rewind(f)`             | برگشت به ابتدا | FILE*                         | void          | `rewind(fp)`           |
| `feof(f)`               | پایان فایل؟    | FILE*                         | غیرصفر یا 0   | `while(!feof(fp))`     |
| `ferror(f)`             | خطا؟           | FILE*                         | غیرصفر یا 0   | `if(ferror(fp))`       |
| `perror(s)`             | چاپ خطا        | رشته                          | void          | `perror("open")`       |
| `remove(name)`          | حذف فایل       | نام                           | 0 یا -1       | `remove("a.txt")`      |
| `rename(o, n)`          | تغییر نام      | دو نام                        | 0 یا -1       | `rename("a","b")`      |
| `fflush(f)`             | تخلیه بافر     | FILE*                         | 0 یا EOF      | `fflush(stdout)`       |

---

# ۴) توابع `<stdlib.h>` — عمومی

| تابع | کار | ورودی | خروجی | مثال |
|------|------|--------|--------|-------|
| `malloc(n)` | تخصیص حافظه | عدد | pointer یا NULL | `malloc(10*sizeof(int))` |
| `calloc(n, sz)` | تخصیص + صفر | تعداد + اندازه | pointer یا NULL | `calloc(10,sizeof(int))` |
| `realloc(p, n)` | تغییر اندازه | pointer + عدد | pointer یا NULL | `realloc(p,20)` |
| `free(p)` | آزادسازی | pointer | void | `free(p)` |
| `atoi(s)` | رشته به int | رشته | int | `atoi("42")` → `42` |
| `atof(s)` | رشته به double | رشته | double | `atof("3.14")` → `3.14` |
| `atol(s)` | رشته به long | رشته | long | `atol("100")` |
| `strtol(s, &e, b)` | رشته به long با مبنا | رشته + pointer + مبنا | long | `strtol("FF",NULL,16)` → `255` |
| `strtod(s, &e)` | رشته به double | رشته + pointer | double | `strtod("3.14",NULL)` |
| `abs(n)` | قدر مطلق int | int | int | `abs(-5)` → `5` |
| `labs(n)` | قدر مطلق long | long | long | `labs(-5L)` |
| `rand()` | عدد تصادفی | — | int (0..RAND_MAX) | `rand()%100` |
| `srand(seed)` | مقدار اولیه تصادفی | عدد | void | `srand(time(NULL))` |
| `qsort(a,n,sz,cmp)` | مرتب‌سازی | آرایه + تعداد + اندازه + تابع مقایسه | void | `qsort(a,10,sizeof(int),cmp)` |
| `bsearch(k,a,n,sz,cmp)` | جستجوی دودویی | کلید + آرایه + ... | pointer یا NULL | `bsearch(&k,a,10,sizeof(int),cmp)` |
| `exit(n)` | خروج برنامه | کد | void | `exit(0)` |
| `abort()` | خروج فوری | — | void | `abort()` |
| `system(s)` | اجرای دستور | رشته | int | `system("ls")` |
| `getenv(s)` | خواندن متغیر محیطی | رشته | رشته یا NULL | `getenv("PATH")` |

---

# ۵) `<math.h>` — ریاضی

| تابع | کار | ورودی | خروجی | مثال |
|------|------|--------|--------|-------|
| `sqrt(x)` | جذر | double | double | `sqrt(16)` → `4` |
| `pow(x, y)` | توان | دو double | double | `pow(2,3)` → `8` |
| `fabs(x)` | قدر مطلق | double | double | `fabs(-3.5)` → `3.5` |
| `floor(x)` | گرد به پایین | double | double | `floor(3.7)` → `3` |
| `ceil(x)` | گرد به بالا | double | double | `ceil(3.2)` → `4` |
| `round(x)` | گرد به نزدیک | double | double | `round(3.5)` → `4` |
| `fmod(x, y)` | باقیمانده اعشاری | دو double | double | `fmod(5.5,2)` → `1.5` |
| `sin(x)`, `cos(x)`, `tan(x)` | مثلثاتی | double (رادیان) | double | `sin(0)` → `0` |
| `log(x)`, `log10(x)` | لگاریتم | double | double | `log(1)` → `0` |
| `exp(x)` | e^x | double | double | `exp(0)` → `1` |

---

# ۶) `<time.h>` — زمان

| تابع/نوع | کار | ورودی | خروجی | مثال |
|-----------|------|--------|--------|-------|
| `time(&t)` | زمان فعلی | pointer | time_t | `time(NULL)` |
| `clock()` | زمان CPU | — | clock_t | `clock()` |
| `difftime(a, b)` | اختلاف زمان | دو time_t | double | `difftime(t2,t1)` |
| `localtime(&t)` | تبدیل به محلی | pointer | struct tm* | `localtime(&t)` |
| `gmtime(&t)` | تبدیل به UTC | pointer | struct tm* | `gmtime(&t)` |
| `strftime(b,n,f,tm)` | قالب‌بندی زمان | بافر + ... | size_t | `strftime(b,100,"%Y",&tm)` |
| `struct tm` | ساختار زمان | — | — | `tm.tm_year`, `tm.tm_mon` |

---

# ۷) `<stdbool.h>` — بولی

| ماکرو | مقدار |
|--------|--------|
| `bool` | `_Bool` |
| `true` | `1` |
| `false` | `0` |

---

# ۸) `<stdint.h>` — انواع با اندازه دقیق

| نوع | اندازه |
|------|---------|
| `int8_t`, `uint8_t` | 8 بیت |
| `int16_t`, `uint16_t` | 16 بیت |
| `int32_t`, `uint32_t` | 32 بیت |
| `int64_t`, `uint64_t` | 64 بیت |
| `size_t` | بدون علامت برای اندازه |
| `ptrdiff_t` | اختلاف pointer |
| `NULL` | `((void*)0)` |

---

# ۹) ساختارهای مهم (`struct`)

| ساختار | هدر | فیلدهای مهم |
|---------|------|--------------|
| `FILE` | stdio.h | opaque — فقط با pointer کار کن |
| `struct tm` | time.h | `tm_sec`, `tm_min`, `tm_hour`, `tm_mday`, `tm_mon`, `tm_year`, `tm_wday`, `tm_yday`, `tm_isdst` |
| `struct div_t` | stdlib.h | `quot`, `rem` |
| `struct ldiv_t` | stdlib.h | `quot`, `rem` (long) |
| `struct timespec` | time.h | `tv_sec`, `tv_nsec` |

### مثال `struct tm`:
```c
time_t t = time(NULL);
struct tm *lt = localtime(&t);
printf("%d/%d/%d\n", lt->tm_year+1900, lt->tm_mon+1, lt->tm_mday);
```

---

# ۱۰) جدول جمع‌بندی هدرها

| هدر | توابع کلیدی |
|------|---------------|
| `<stdio.h>` | printf, scanf, fopen, fgets, fclose |
| `<string.h>` | strlen, strcpy, strcmp, strtok, memcpy |
| `<ctype.h>` | isalpha, isdigit, toupper, tolower |
| `<stdlib.h>` | malloc, free, atoi, qsort, rand, exit |
| `<math.h>` | sqrt, pow, sin, floor, fabs |
| `<time.h>` | time, clock, localtime, strftime |
| `<stdbool.h>` | bool, true, false |
| `<stdint.h>` | int32_t, uint64_t, size_t |
| `<stdarg.h>` | va_start, va_arg, va_end |
| `<assert.h>` | assert |
| `<errno.h>` | errno, perror |
| `<signal.h>` | signal, raise |
| `<setjmp.h>` | setjmp, longjmp |
| `<locale.h>` | setlocale, localeconv |
| `<limits.h>` | INT_MAX, CHAR_MIN, ... |
| `<float.h>` | FLT_MAX, DBL_MIN, ... |

---

# ۱۱) نکات تستی طلایی ⚡

1. **`scanf` و `\n`** → `\n` در بافر می‌مونه، با `getchar` پاکش کن
2. **`fgets`** → `\n` رو ذخیره می‌کنه، با `strcspn` حذفش کن
3. **`puts`** → خودش `\n` می‌ذاره، `fputs` نمی‌ذاره
4. **`strcmp`** → هرگز با `==` مقایسه نکن
5. **`strncpy`** → ممکنه `\0` نذارهUntitled
6. **`malloc`** → همیشه چک کن `NULL` نباشه
7. **`free`** → فقط روی حافظه malloc شده، دوبار free نکن
8. **`strtok`** → رشته اصلی رو خراب می‌کنه
9. **`atoi`** → خطا رو تشخیص نمی‌ده، از `strtol` استفاده کن
10. **`qsort`** → تابع مقایسه باید `int cmp(const void*, const void*)` باشه

---

اگه خواستی، می‌تونم این جدول‌ها رو **در قالب یه فایل Markdown یا PDF تک‌صفحه‌ای** برات جمع کنم که راحت پرینت بگیری و مرور کنی. بگو کدوم فرمت رو می‌خوای.