<div dir="rtl" style="font-family: 'Vazir', sans-serif; line-height: 1.8;">

---
در فصل دوازدهم، به مبحث کار با API‌ها (رابط‌های برنامه‌نویسی کاربردی) در PHP خواهیم پرداخت. API‌ها به شما امکان می‌دهند که برنامه‌های وب خود را به سرویس‌های دیگر متصل کنید، داده‌ها را به اشتراک بگذارید و قابلیت‌های جدیدی به برنامه‌های خود اضافه کنید. در این فصل، به بررسی نحوه استفاده از API‌های RESTful، ارسال درخواست‌های HTTP، دریافت و پردازش پاسخ‌ها، و پیاده‌سازی API‌های ساده در PHP خواهیم پرداخت.

### **فصل دوازدهم: کار با API‌ها در PHP**

---

### **12.1 مقدمه‌ای بر API‌ها**

API مخفف "Application Programming Interface" به معنای رابط برنامه‌نویسی کاربردی است. APIها به برنامه‌های مختلف اجازه می‌دهند که با یکدیگر ارتباط برقرار کنند و داده‌ها و خدمات خود را به اشتراک بگذارند. یکی از رایج‌ترین انواع APIها، **RESTful API** است که از پروتکل HTTP برای ارسال و دریافت داده‌ها استفاده می‌کند.

### **12.2 RESTful API چیست؟**

REST (Representational State Transfer) یک سبک معماری برای طراحی APIهای وب است که از پروتکل HTTP برای عملیات CRUD (Create, Read, Update, Delete) استفاده می‌کند. RESTful APIها به شما این امکان را می‌دهند که از طریق URLها به منابع مختلف دسترسی پیدا کرده و عملیات‌های مختلفی بر روی آن‌ها انجام دهید.

#### **12.2.1 عملیات HTTP رایج در RESTful API**

- **GET:** برای دریافت داده‌ها از سرور (خواندن).
- **POST:** برای ارسال داده‌های جدید به سرور (ایجاد).
- **PUT:** برای به‌روزرسانی داده‌های موجود در سرور (به‌روزرسانی).
- **DELETE:** برای حذف داده‌های موجود در سرور (حذف).

### **12.3 ارسال درخواست‌های HTTP در PHP**

برای ارسال درخواست‌های HTTP به یک API خارجی، می‌توان از توابع داخلی PHP مانند `file_get_contents()` و `cURL` استفاده کرد. `cURL` یک کتابخانه قدرتمند برای ارسال درخواست‌های HTTP در PHP است که انعطاف‌پذیری بالایی را برای کار با APIها فراهم می‌کند.

#### **12.3.1 استفاده از `file_get_contents()` برای ارسال درخواست‌های GET**

**مثال: ارسال درخواست GET به یک API:**

```php
<?php
$url = "https://jsonplaceholder.typicode.com/posts/1";
$response = file_get_contents($url); // ارسال درخواست GET به API
$data = json_decode($response, true); // تبدیل پاسخ JSON به آرایه PHP

echo "Title: " . $data['title'] . "<br>";
echo "Body: " . $data['body'];
?>
```

در این مثال، یک درخواست GET به یک API نمونه ارسال شده و پاسخ JSON دریافت شده و به آرایه PHP تبدیل شده است.

#### **12.3.2 استفاده از cURL برای ارسال درخواست‌های GET و POST**

**مثال: ارسال درخواست GET با cURL:**

```php
<?php
$ch = curl_init(); // شروع یک جلسه cURL
curl_setopt($ch, CURLOPT_URL, "https://jsonplaceholder.typicode.com/posts/1"); // تنظیم URL
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true); // بازگرداندن پاسخ به جای نمایش مستقیم
$response = curl_exec($ch); // اجرای درخواست GET
curl_close($ch); // بستن جلسه cURL

$data = json_decode($response, true);
echo "Title: " . $data['title'] . "<br>";
echo "Body: " . $data['body'];
?>
```

**مثال: ارسال درخواست POST با cURL:**

```php
<?php
$ch = curl_init("https://jsonplaceholder.typicode.com/posts"); // تنظیم URL
$data = array(
    'title' => 'Sample Title',
    'body' => 'This is a sample post.',
    'userId' => 1
);

curl_setopt($ch, CURLOPT_POST, true); // تنظیم درخواست به POST
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data)); // ارسال داده‌ها به صورت JSON
curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: application/json')); // تنظیم نوع محتوا به JSON
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true); // بازگرداندن پاسخ

$response = curl_exec($ch); // اجرای درخواست POST
curl_close($ch); // بستن جلسه cURL

echo "Response: " . $response;
?>
```

### **12.4 پیاده‌سازی یک API ساده در PHP**

در PHP، می‌توان به راحتی یک API ساده ایجاد کرد که درخواست‌های HTTP را پردازش کرده و پاسخ‌های مناسب ارسال کند. برای این کار، می‌توان از ساختار فایل PHP معمولی استفاده کرد.

#### **12.4.1 پیاده‌سازی یک API ساده برای مدیریت کاربران**

در این مثال، یک API ساده برای مدیریت کاربران ایجاد می‌شود که امکان عملیات‌های CRUD را فراهم می‌کند.

**ساختار فایل:**
- `api.php`

**کد نمونه:**

```php
<?php
header("Content-Type: application/json"); // تنظیم نوع محتوا به JSON
$request_method = $_SERVER["REQUEST_METHOD"]; // دریافت متد درخواست

switch ($request_method) {
    case 'GET':
        getUsers();
        break;
    case 'POST':
        addUser();
        break;
    case 'PUT':
        updateUser();
        break;
    case 'DELETE':
        deleteUser();
        break;
    default:
        echo json_encode(["message" => "Invalid request method"]);
        break;
}

// توابع مدیریت کاربران
function getUsers() {
    // دریافت کاربران از پایگاه داده (نمونه)
    $users = [
        ["id" => 1, "name" => "John Doe", "email" => "john@example.com"],
        ["id" => 2, "name" => "Jane Doe", "email" => "jane@example.com"]
    ];
    echo json_encode($users);
}

function addUser() {
    // دریافت داده‌های کاربر از درخواست POST
    $data = json_decode(file_get_contents("php://input"), true);
    if (!empty($data["name"]) && !empty($data["email"])) {
        // اضافه کردن کاربر به پایگاه داده (نمونه)
        echo json_encode(["message" => "User added successfully"]);
    } else {
        echo json_encode(["message" => "Invalid user data"]);
    }
}

function updateUser() {
    // دریافت داده‌های کاربر از درخواست PUT
    $data = json_decode(file_get_contents("php://input"), true);
    if (!empty($data["id"]) && (!empty($data["name"]) || !empty($data["email"]))) {
        // به‌روزرسانی کاربر در پایگاه داده (نمونه)
        echo json_encode(["message" => "User updated successfully"]);
    } else {
        echo json_encode(["message" => "Invalid user data"]);
    }
}

function deleteUser() {
    // دریافت ID کاربر از درخواست DELETE
    $data = json_decode(file_get_contents("php://input"), true);
    if (!empty($data["id"])) {
        // حذف کاربر از پایگاه داده (نمونه)
        echo json_encode(["message" => "User deleted successfully"]);
    } else {
        echo json_encode(["message" => "Invalid user ID"]);
    }
}
?>
```

### **12.5 ارسال و دریافت داده‌ها با فرمت JSON**

JSON (JavaScript Object Notation) یک فرمت متداول برای تبادل داده‌ها بین کلاینت و سرور است. در PHP، می‌توان از توابع `json_encode()` و `json_decode()` برای کار با داده‌های JSON استفاده کرد.

**مثال: تبدیل آرایه PHP به JSON:**

```php
<?php
$user = ["id" => 1, "name" => "John Doe", "email" => "john@example.com"];
$json = json_encode($user); // تبدیل آرایه به JSON
echo $json; // نمایش JSON
?>
```

**مثال: تبدیل JSON به آرایه PHP:**

```php
<?php
$json = '{"id":1,"name":"John Doe","email":"john@example.com"}';
$user = json_decode($json, true); // تبدیل JSON به آرایه
print_r($user); // نمایش آرایه
?>
```

### **12.6 مدیریت احراز هویت و مجوزها در API‌ها**

احراز هویت و مجوزها بخش‌های مهمی از طراحی یک API امن هستند. برای محافظت از APIها، معمولاً از تکنیک‌هایی مانند استفاده از توکن‌های API، JWT (JSON Web Tokens)، و OAuth استفاده می‌شود.

#### **12.6.1 استفاده از توکن‌های API**

توکن‌های API یک روش ساده برای احراز هویت کاربران و محدود کردن دسترسی به APIها هستند. این توکن‌ها می‌توانند به صورت دستی ایجاد شده و به کاربران اختصاص داده شوند.

**مثال: بررسی توکن API در یک API ساده:**

```php
<?php
$valid_token = "YOUR_SECURE_TOKEN";

if ($_SERVER['HTTP_AUTHORIZATION'] !== $valid_token) {
    http_response_code(401); // کد پاسخ 401 (Unauthorized)
    echo json_encode(["message" => "Unauthorized"]);
    exit();
}
?>
```

### **12.7 بهترین شیوه‌ها برای طراحی و پیاده‌سازی APIها**

1. **استفاده از HTTP Status Codes مناسب:** همیشه از کدهای وضعیت HTTP مناسب برای نشان دادن نتیجه درخواست‌ها استفاده کنید (مانند

 200 برای موفقیت، 404 برای پیدا نشدن، 500 برای خطاهای سرور).
   
2. **استفاده از ورژن‌بندی API:** ورژن‌بندی API به شما این امکان را می‌دهد که تغییرات آینده را بدون اختلال در نسخه‌های فعلی مدیریت کنید (مثلاً `/api/v1/users`).

3. **مستندسازی APIها:** همیشه مستندات کامل و به‌روز برای APIهای خود ارائه دهید تا توسعه‌دهندگان دیگر به راحتی از آن‌ها استفاده کنند.

4. **استفاده از SSL/TLS برای امنیت:** برای محافظت از داده‌های ارسال‌شده بین کلاینت و سرور، همیشه از HTTPS استفاده کنید.

### **12.8 تمرین‌های فصل دوازدهم**

1. **ارسال درخواست‌های GET و POST:** برنامه‌ای بنویسید که از cURL برای ارسال درخواست‌های GET و POST به یک API خارجی استفاده کند.
   
2. **پیاده‌سازی API ساده:** یک API ساده برای مدیریت کتاب‌ها بنویسید که عملیات‌های CRUD را پشتیبانی کند.
   
3. **کار با JSON در PHP:** برنامه‌ای بنویسید که داده‌های فرم را به JSON تبدیل کرده و آن‌ها را به یک API ارسال کند.
   
4. **مدیریت احراز هویت با توکن API:** برنامه‌ای ایجاد کنید که از توکن‌های API برای احراز هویت و دسترسی به منابع محافظت‌شده استفاده کند.
   
5. **مستندسازی API:** API خود را با استفاده از ابزارهایی مانند Swagger مستند کنید.

### **خلاصه فصل دوازدهم**

در این فصل، با نحوه کار با APIها در PHP آشنا شدید. یاد گرفتید که چگونه درخواست‌های HTTP را با استفاده از `file_get_contents()` و `cURL` ارسال کنید، APIهای ساده را پیاده‌سازی کنید، داده‌ها را با فرمت JSON مدیریت کنید و از توکن‌های API برای احراز هویت استفاده کنید. پیروی از بهترین شیوه‌ها می‌تواند به شما کمک کند تا APIهای امن، قابل استفاده مجدد و کارآمدتری طراحی کنید.

---
</div>