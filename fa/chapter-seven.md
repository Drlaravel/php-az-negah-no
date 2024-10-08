



<div dir="rtl" style="font-family: 'Vazir', sans-serif; line-height: 1.8;">

### **فصل هفتم: مدیریت خطاها و استثناها در PHP**

---

### **7.1 مقدمه‌ای بر مدیریت خطاها و استثناها**

مدیریت خطاها یکی از بخش‌های حیاتی برنامه‌نویسی است که کمک می‌کند تا برنامه‌ها به صورت پایدارتر و قابل اعتمادتر عمل کنند. در زبان PHP، روش‌های متعددی برای مدیریت و کنترل خطاها وجود دارد. این روش‌ها شامل استفاده از توابع داخلی مدیریت خطا، استفاده از بلوک‌های `try...catch` برای مدیریت استثناها، تعریف خطاهای سفارشی و استفاده از کتابخانه‌های موجود می‌شود.

خطاها می‌توانند به دلایل مختلفی رخ دهند؛ از جمله خطاهای برنامه‌نویسی (مانند خطاهای سینتکسی)، خطاهای اجرایی (مانند تقسیم بر صفر)، و خطاهای محیطی (مانند مشکلات اتصال به پایگاه داده یا عدم دسترسی به فایل‌ها).

### **7.2 انواع خطاها در PHP**

در PHP، خطاها به چندین دسته تقسیم می‌شوند که هر کدام نوع خاصی از مشکل را نشان می‌دهند:

1. **خطاهای تجزیه (Parse Errors):** این نوع خطاها زمانی رخ می‌دهند که PHP قادر به تجزیه کد شما نباشد. این نوع خطاها معمولاً به دلیل اشتباهات سینتکسی مانند فراموش کردن یک نقطه‌ویرگول (`;`) در پایان یک دستور ایجاد می‌شوند.
   
   **مثال:**

   ```php
   <?php
   echo "Hello, World!" // نقطه‌ویرگول در پایان فراموش شده است
   ?>
   ```

2. **خطاهای کشنده (Fatal Errors):** این خطاها زمانی رخ می‌دهند که PHP قادر به انجام یک عملیات خاص نباشد. این می‌تواند به دلیل فراخوانی یک تابع یا کلاس ناشناخته، و یا دسترسی به یک شیء نادرست باشد.

   **مثال:**

   ```php
   <?php
   nonExistentFunction(); // فراخوانی یک تابع تعریف‌نشده
   ?>
   ```

3. **خطاهای هشدار (Warnings):** این خطاها زمانی رخ می‌دهند که مشکلی در اجرای کد وجود دارد، اما PHP همچنان به اجرای برنامه ادامه می‌دهد. به عنوان مثال، تلاش برای درج یک فایل که وجود ندارد.

   **مثال:**

   ```php
   <?php
   include("nonexistentfile.php"); // تلاش برای درج یک فایل که وجود ندارد
   ?>
   ```

4. **خطاهای اخطار (Notices):** این نوع خطاها زمانی رخ می‌دهند که PHP به مشکلی جزئی برخورد کند، اما اجرای کد همچنان ادامه می‌یابد. این خطاها معمولاً زمانی رخ می‌دهند که به یک متغیر تعریف‌نشده دسترسی پیدا کنید.

   **مثال:**

   ```php
   <?php
   echo $undefinedVariable; // استفاده از متغیر تعریف‌نشده
   ?>
   ```

### **7.3 مدیریت خطاهای استاندارد در PHP**

PHP به طور پیش‌فرض دارای سیستم مدیریت خطای داخلی است که رفتار پیش‌فرض آن می‌تواند توسط برنامه‌نویس تغییر کند. تنظیم سطح گزارش‌دهی خطاها، نمایش یا عدم نمایش خطاها و تغییر نحوه مدیریت خطاها از جمله اقداماتی است که می‌توان انجام داد.

#### **7.3.1 استفاده از `error_reporting()`**

این تابع به شما اجازه می‌دهد که نوع خطاهایی که می‌خواهید PHP گزارش دهد را مشخص کنید. این تابع می‌تواند برای فعال یا غیرفعال کردن انواع مختلفی از خطاها استفاده شود.

```php
<?php
// تنظیم سطح گزارش‌دهی خطاها
error_reporting(E_ALL); // گزارش تمام خطاها
ini_set('display_errors', 1); // نمایش خطاها در مرورگر
?>
```

در این مثال، تمام خطاها، هشدارها و اخطارها گزارش داده می‌شوند و در مرورگر نمایش داده می‌شوند. این نوع تنظیمات معمولاً در محیط توسعه استفاده می‌شود و در محیط تولید معمولاً خطاها به لاگ‌ها نوشته می‌شوند.

#### **7.3.2 توابع کنترل خطا**

علاوه بر `error_reporting()`، PHP توابع دیگری نیز برای کنترل و مدیریت خطاها دارد:

- **`ini_set()`**: این تابع به شما امکان می‌دهد تا تنظیمات مختلفی را به طور موقت تغییر دهید. برای مثال:

  ```php
  ini_set('log_errors', 1); // فعال کردن گزارش خطاها در فایل لاگ
  ini_set('error_log', 'errors.log'); // تنظیم مسیر فایل لاگ خطا
  ```

- **`restore_error_handler()`**: برای بازگرداندن کنترل خطا به حالت پیش‌فرض PHP استفاده می‌شود.

### **7.4 استفاده از بلوک‌های `try...catch` برای مدیریت استثناها**

PHP از نسخه 5 به بعد از مدیریت استثناها با استفاده از بلوک‌های `try...catch` پشتیبانی می‌کند. این بلوک‌ها به شما اجازه می‌دهند که بخش‌هایی از کد را که ممکن است خطا ایجاد کنند، شناسایی کرده و به شکل مناسب مدیریت کنید.

#### **7.4.1 ساختار بلوک‌های `try...catch`**

بلوک `try` شامل کدی است که ممکن است خطا ایجاد کند، و بلوک `catch` کدی است که خطا را مدیریت می‌کند.

```php
<?php
try {
    // کدی که ممکن است استثنا پرتاب کند
    $result = 10 / 0; // تقسیم بر صفر که خطا ایجاد می‌کند
} catch (Exception $e) {
    // مدیریت استثنا
    echo "Caught Exception: " . $e->getMessage();
} finally {
    echo "This block always executes."; // بلوک اختیاری finally که همیشه اجرا می‌شود
}
?>
```

در این مثال، بلوک `try` شامل کدی است که ممکن است خطا ایجاد کند. اگر خطا رخ دهد، به بلوک `catch` منتقل می‌شود، و در نهایت بلوک `finally` که همیشه اجرا می‌شود، حتی اگر خطایی رخ ندهد.

### **7.5 تعریف و مدیریت خطاهای سفارشی**

PHP به شما اجازه می‌دهد که خطاهای سفارشی خود را تعریف کنید. برای این کار، باید یک تابع خطای سفارشی ایجاد کرده و از تابع `set_error_handler()` برای تنظیم آن استفاده کنید.

#### **7.5.1 تعریف یک تابع خطای سفارشی**

در این مثال، یک تابع خطای سفارشی تعریف می‌شود که یک پیام خاص برای خطاهای مختلف نمایش می‌دهد.

```php
<?php
function customError($errno, $errstr) {
    echo "Error: [$errno] $errstr<br>";
    error_log("Error: [$errno] $errstr", 3, "errors.log"); // ذخیره خطا در فایل لاگ
}

// تنظیم تابع خطای سفارشی
set_error_handler("customError");

// تولید یک خطا
echo 10 / 0; // این خطا را ایجاد می‌کند و به تابع customError می‌رود
?>
```

در اینجا، وقتی که خطا رخ می‌دهد، تابع `customError()` اجرا می‌شود و پیام خطای سفارشی نمایش داده می‌شود و همچنین در فایل `errors.log` ذخیره می‌شود.

### **7.6 مدیریت خطاهای پایگاه داده**

در هنگام کار با پایگاه داده‌ها، خطاها می‌توانند ناشی از مشکلات اتصال به سرور، خطاهای دستوری SQL، یا دسترسی نادرست به داده‌ها باشند. برای مدیریت این نوع خطاها، می‌توان از بلوک‌های `try...catch` استفاده کرد.

```php
<?php
try {
    // اتصال به پایگاه داده
    $conn = new PDO("mysql:host=localhost;dbname=testdb", "root", "");
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    
    // اجرای یک دستور SQL
    $conn->exec("INVALID SQL"); // این خطا ایجاد می‌کند
} catch (PDOException $e) {
    echo "Database error: " . $e->getMessage();
} finally {
    $conn = null; // بستن اتصال
}
?>
```

### **7.7 مدیریت خطاهای API و وب‌سرویس‌ها**

هنگام کار با API‌ها و وب‌سرویس‌ها، خطاها می‌توانند ناشی از مشکلات شبکه، درخواست‌های نادرست، یا پاسخ‌های غیرمنتظره باشند. مدیریت خطاهای API باید به گونه‌ای باشد که بتواند تمام این شرایط را پوشش دهد.

### **تمرین‌های فصل هفتم**

1. **تنظیم سطح گزارش‌دهی خطاها:** تنظیم کنید که فقط خطاهای کشنده نمایش داده شوند.
2. **استفاده از `try...catch`:** یک برنامه ساده بنویسید که یک عدد را

 بر صفر تقسیم کند و خطای مربوطه را با استفاده از `try...catch` مدیریت کند.
3. **تعریف خطای سفارشی:** تابع خطای سفارشی خود را برای مدیریت خطاهای نوع خاصی بنویسید.
4. **مدیریت خطاهای پایگاه داده:** برنامه‌ای بنویسید که به پایگاه داده متصل شود و خطاهای مربوط به عملیات‌های SQL را مدیریت کند.
5. **مدیریت خطاهای API:** برنامه‌ای بنویسید که به یک API متصل شود و خطاهای مربوط به درخواست‌های ناموفق را مدیریت کند.

### **خلاصه فصل هفتم**

در این فصل، با انواع مختلف خطاها در PHP آشنا شدید و یاد گرفتید چگونه آن‌ها را مدیریت و گزارش کنید. همچنین با بلوک‌های `try...catch` برای مدیریت استثناها و نحوه تعریف خطاهای سفارشی آشنا شدید. این مهارت‌ها به شما کمک می‌کنند تا برنامه‌های PHP قابل اطمینان‌تری بنویسید و خطاها را به صورت بهینه مدیریت کنید.

---

</div>