سؤال خوبی پرسیدی. اول جواب مستقیم، بعد لیست کامل preprocessor directiveها.

---

# جواب مستقیم سؤال 🎯

دستوری که باعث می‌شه:

- توکن‌های داخلش به‌عنوان **پیام خطا** نمایش داده بشن
- **preprocessing متوقف** بشه
- برنامه **کامپایل نشه**

اینه:

```c
#error پیام خطا
```

## مثال:

```c
#ifndef __STDC__
#error This compiler is not standard C
#endif
```

اگه `__STDC__` تعریف نشده باشه، کامپایلر پیام `This compiler is not standard C` رو چاپ می‌کنه و **preprocessing رو متوقف می‌کنه** و برنامه کامپایل نمی‌شه.

## تفاوت `#error` و `#warning`:

| دستور | پیام | توقف پردازش | کامپایل |
|--------|------|---------------|----------|
| `#error` | خطا | ✅ بله | ❌ نمی‌شه |
| `#warning` | هشدار | ❌ نه | ✅ می‌شه |

---

# لیست کامل Preprocessor Directives در C

## ۱) دستورات شرطی (Conditional Compilation)

| دستور | کار |
|--------|------|
| `#if expr` | اگه expr درست باشه، بلاک پردازش می‌شه |
| `#ifdef NAME` | اگه NAME تعریف شده باشه |
| `#ifndef NAME` | اگه NAME تعریف نشده باشه |
| `#elif expr` | else-if برای `#if` |
| `#else` | بلاک جایگزین |
| `#endif` | پایان بلاک شرطی |

### مثال:
```c
#ifdef DEBUG
    printf("debug mode\n");
#elif defined(VERBOSE)
    printf("verbose\n");
#else
    printf("normal\n");
#endif
```

---

## ۲) تعریف و حذف ماکرو

| دستور | کار |
|--------|------|
| `#define NAME value` | تعریف ماکرو |
| `#define NAME(params) body` | ماکرو تابعی |
| `#undef NAME` | حذف تعریف ماکرو |

### مثال:
```c
#define PI 3.14159
#define MAX(a,b) ((a) > (b) ? (a) : (b))
#undef PI
```

---

## ۳) شامل کردن فایل

| دستور | کار |
|--------|------|
| `#include <file>` | شامل فایل سیستمی |
| `#include "file"` | شامل فایل محلی |

### تفاوت:
- `< >` → جستجو در مسیرهای استاندارد کامپایلر
- `" "` → اول مسیر محلی، بعد مسیرهای استاندارد

---

## ۴) کنترل خطا و دیباگ

| دستور | کار | توقف؟ |
|--------|------|--------|
| `#error message` | چاپ پیام خطا و توقف پردازش | ✅ بله |
| `#warning message` | چاپ هشدار (ادامه می‌ده) | ❌ نه |
| `#line number "file"` | تغییر شماره خط و نام فایل | — |
| `#pragma ...` | دستور مخصوص کامپایلر | — |

### مثال `#error`:
```c
#if __STDC_VERSION__ < 199901L
#error C99 or later required
#endif
```

### مثال `#warning`:
```c
#warning This code is deprecated
```

### مثال `#line`:
```c
#line 100 "myfile.c"
// خط بعدی به‌عنوان خط 100 فایل myfile.c حساب می‌شه
```

### مثال `#pragma`:
```c
#pragma once            // جلوگیری از include چندباره
#pragma pack(1)         // غیرفعال کردن padding
#pragma GCC optimize("O2")
```

---

## ۵) دستورات ماکروی استاندارد (Predefined Macros)

این‌ها **دستور** نیستن، ولی ماکروهای از پیش تعریف‌شده هستن:

| ماکرو | معنی |
|--------|-------|
| `__FILE__` | نام فایل فعلی |
| `__LINE__` | شماره خط فعلی |
| `__DATE__` | تاریخ کامپایل |
| `__TIME__` | زمان کامپایل |
| `__func__` | نام تابع فعلی (C99) |
| `__STDC__` | اگه استاندارد C باشه، 1 |
| `__STDC_VERSION__` | نسخه استاندارد (مثل 199901L) |
| `__cplusplus` | در C++ تعریف شده |

### مثال:
```c
printf("File: %s, Line: %d\n", __FILE__, __LINE__);
```

---

## ۶) اپراتورهای preprocessor

| اپراتور | کار |
|----------|------|
| `#` | تبدیل آرگومان به رشته (stringize) |
| `##` | الحاق توکن‌ها (token paste) |
| `defined(NAME)` | چک تعریف شدن (فقط در `#if`) |

### مثال `#`:
```c
#define STR(x) #x
STR(hello)   // → "hello"
```

### مثال `##`:
```c
#define CONCAT(a,b) a##b
CONCAT(var, 1)   // → var1
```

### مثال `defined`:
```c
#if defined(DEBUG) && !defined(NDEBUG)
    ...
#endif
```

---

# جدول جمع‌بندی همه دستورات

| دسته | دستورات |
|-------|----------|
| **شرطی** | `#if`, `#ifdef`, `#ifndef`, `#elif`, `#else`, `#endif` |
| **ماکرو** | `#define`, `#undef` |
| **شامل** | `#include` |
| **خطا/دیباگ** | `#error`, `#warning`, `#line`, `#pragma` |
| **ماکروهای آماده** | `__FILE__`, `__LINE__`, `__DATE__`, `__TIME__`, `__func__`, `__STDC__` |
| **اپراتورها** | `#`, `##`, `defined` |

---

# کاربردهای واقعی `#error`

### ۱) چک نسخه استاندارد:
```c
#if __STDC_VERSION__ < 199901L
#error C99 or later required
#endif
```

### ۲) چک معماری:
```c
#if !defined(__x86_64__) && !defined(__i386__)
#error This code only works on x86
#endif
```

### ۳) چک سیستم‌عامل:
```c
#if !defined(_WIN32) && !defined(__linux__)
#error Unsupported OS
#endif
```

### ۴) چک هدر ضروری:
```c
#ifndef CONFIG_H
#error config.h must be included first
#endif
```

---

# نکات تستی طلایی ⚡

1. `#error` → **توقف preprocessing** + پیام خطا → کامپایل نمی‌شه
2. `#warning` → فقط **هشدار** → کامپایل ادامه پیدا می‌کنه
3. `#error` و `#warning` در **C23** استاندارد شدن (قبلاً extension بودن)
4. `#error` فقط توکن‌های خط رو چاپ می‌کنه، نه چیز دیگه
5. `#pragma` → رفتارش **مخصوص کامپایلر**ه (portable نیست)
6. `#line` → برای ابزارهایی مثل **lex/yacc** مفیده
7. `#include` → فقط **یک بار** per translation unit پردازش می‌شه، مگر با `#pragma once` یا include guard
8. `#define` → بدون `;` نوشته می‌شه (اگه `;` بذاری، جزو بدنه ماکرو می‌شه)

---

# مثال نهایی: include guard

```c
#ifndef MYHEADER_H
#define MYHEADER_H

// محتوای هدر

#endif
```

یا با pragma:
```c
#pragma once
// محتوای هدر
```

---

**خلاصه یک‌خطی:**  
> دستوری که توکن‌هاش به‌عنوان پیام خطا چاپ می‌شن، preprocessing رو متوقف می‌کنه و کامپایل نمی‌شه → **`#error`**

اگه خواستی، می‌تونم یه مثال عملی از `#if` + `#error` + `#pragma` با کامپایل واقعی برات بنویسم که ببینی چطور کار می‌کنه.