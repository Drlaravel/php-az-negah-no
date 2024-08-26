<div dir="rtl" style="font-family: 'Vazir', sans-serif; line-height: 1.8;">
---

### فصل دوازدهم: کار با API‌ها

---

## 12.1 معرفی API‌ها

API (Application Programming Interface) یک واسط است که به برنامه‌ها اجازه می‌دهد با یکدیگر ارتباط برقرار کنند. API‌ها معمولاً برای تبادل داده‌ها بین برنامه‌های مختلف استفاده می‌شوند.

## 12.2 معرفی RESTful API

REST (Representational State Transfer) یک سبک معماری است که برای ساخت API‌ها استفاده می‌شود. RESTful API‌ها از پروتکل HTTP برای ارتباطات استفاده می‌کنند و معمولاً از فرمت JSON برای تبادل داده‌ها بهره می‌برند.

### 12.2.1 متدهای HTTP

RESTful API‌ها از متدهای HTTP مختلفی برای انجام عملیات مختلف استفاده می‌کنند:

- **GET**: برای دریافت داده‌ها.
- **POST**: برای ایجاد داده‌های جدید.
- **PUT**: برای به‌روزرسانی داده‌ها.
- **DELETE**: برای حذف داده‌ها.

## 12.3 ایجاد یک API ساده با PHP

### 12.3.1 ایجاد یک API برای مدیریت کاربران

در اینجا یک API ساده برای مدیریت کاربران ایجاد می‌کنیم که شامل عملیات CRUD است.

#### 12.3.1.1 دریافت لیست کاربران

```php
<?php
header("Content-Type: application/json");

$users = [
    ["id" => 1, "name" => "Ali", "email" => "ali@example.com"],
    ["id" => 2, "name" => "Mina", "email" => "mina@example.com"]
];

echo json_encode($users);
?>
```

#### 12.3.1.2 دریافت یک کاربر با ID

```php
<?php
header("Content-Type: application/json");

$users = [
    1 => ["name" => "Ali", "email" => "ali@example.com"],
    2 => ["name" => "Mina", "email" => "mina@example.com"]
];

$id = $_GET['id'];
if (isset($users[$id])) {
    echo json_encode($users[$id]);
} else {
    http_response_code(404);
    echo json_encode(["message" => "User not found"]);
}
?>
```

#### 12.3.1.3 ایجاد کاربر جدید

```php
<?php
header("Content-Type: application/json");

$data = json_decode(file_get_contents("php://input"), true);
$newUser = [
    "id" => rand(1, 100),
    "name" => $data['name'],
    "email" => $data['email']
];

// اینجا می‌توانید کاربر جدید را به پایگاه داده اضافه کنید

echo json_encode($newUser);
?>
```

#### 12.3.1.4 به‌روزرسانی کاربر

```php
<?php
header("Content-Type: application/json");

$data = json_decode(file_get_contents("php://input"), true);
$id = $_GET['id'];

// اینجا می‌توانید کاربر را در پایگاه داده به‌روزرسانی کنید

echo json_encode(["message" => "User updated", "id" => $id]);
?>
```

#### 12.3.1.5 حذف کاربر

```php
<?php
header("Content-Type: application/json");

$id = $_GET['id'];

// اینجا می‌توانید کاربر را از پایگاه داده حذف کنید

echo json_encode(["message" => "User deleted", "id" => $id]);
?>
```

## 12.4 کار با cURL برای درخواست HTTP

cURL یک ابزار خط فرمان و کتابخانه است که به شما اجازه می‌دهد درخواست‌های HTTP را ارسال کنید و پاسخ‌ها را دریافت کنید.

### 12.4.1 ارسال درخواست GET

```php
<?php
$ch = curl_init();

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/users");
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);

$response = curl_exec($ch);
curl_close($ch);

echo $response;
?>
```

### 12.4.2 ارسال درخواست POST

```php
<?php
$ch = curl_init();

$data = json_encode(["name" => "Ali", "email" => "ali@example.com"]);

curl_setopt($ch, CURLOPT_URL, "https://api.example.com/users");
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1);
curl_setopt($ch, CURLOPT_HTTPHEADER, ["Content-Type: application/json"]);

$response = curl_exec($ch);
curl_close($ch);

echo $response;
?>
```

## 12.5 استفاده از JSON Web Tokens (JWT) برای احراز هویت

JWT (JSON Web Token) یک استاندارد باز است که برای انتقال اطلاعات به صورت امن بین دو طرف استفاده می‌شود. JWT‌ها معمولاً برای احراز هویت در API‌ها استفاده می‌شوند.

### 12.5.1 ایجاد و ارسال JWT

```php
<?php
$header = json_encode(["alg" => "HS256", "typ" => "JWT"]);
$payload = json_encode(["user_id" => 1, "name" => "Ali"]);
$base64UrlHeader = str_replace(['+', '/', '='], ['-', '_', ''], base64_encode($header));
$base64UrlPayload = str_replace(['+', '/', '='], ['-', '_', ''], base64_encode($payload));
$secret = "your-256-bit-secret";
$signature = hash_hmac('sha256', $base64UrlHeader . "." . $base64UrlPayload, $secret, true);
$base64UrlSignature = str_replace(['+', '/', '='], ['-', '_', ''], base64_encode($signature));
$jwt = $base64UrlHeader . "." . $base64UrlPayload . "." . $base64UrlSignature;

echo $jwt;
?>
```

### 12.5.2 اعتبارسنجی JWT

```php
<?php
$jwt = "your.jwt.token.here";
$parts = explode(".", $jwt);
$header = base64_decode($parts[0]);
$payload = base64_decode($parts[1]);
$signatureProvided = $parts[2];

$secret = "your-256-bit-secret";
$signature = hash_hmac('sha256', $parts[0] . "." . $parts[1], $secret, true);
$base64UrlSignature = str_replace(['+', '/', '='], ['-', '_', ''], base64_encode($signature));

if ($base64UrlSignature === $signatureProvided) {
    echo "JWT is valid";
} else {
    echo "JWT is invalid";
}
?>
```

---

## تمرین‌های فصل دوازدهم

1. **ایجاد یک API ساده**: یک API ساده با PHP ایجاد کنید که عملیات CRUD برای کاربران را پیاده‌سازی کند.

2. **ارسال درخواست GET با cURL**: یک درخواست GET با استفاده از cURL به یک API ارسال کنید و نتیجه را در مرورگر نمایش دهید.

3. **ارسال درخواست POST با cURL**: یک درخواست POST با استفاده از cURL به یک API ارسال کنید و داده‌ها را به سرور ارسال کنید.

4. **ایجاد و استفاده از JWT**: یک JWT ایجاد کنید و سپس آن را اعتبارسنجی کنید تا مطمئن شوید که JWT صحیح است.

---

## خلاصه فصل دوازدهم

در این فصل، با API‌ها و نحوه ایجاد و استفاده از آن‌ها در PHP آشنا شدید. شما یاد گرفتید که چگونه یک RESTful API ایجاد کنید و از متدهای HTTP برای انجام عملیات مختلف استفاده کنید. همچنین با ابزار cURL برای ارسال درخواست‌های HTTP و استفاده از JSON Web Tokens (JWT) برای احراز هویت آشنا شدید. API‌ها یکی از اجزای حیاتی برنامه‌های مدرن هستند و در این فصل، مهارت‌های لازم برای کار با API‌ها در PHP را به دست آوردید.

---
</div>