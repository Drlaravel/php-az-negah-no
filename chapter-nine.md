<div dir="rtl" style="font-family: 'Vazir', sans-serif; line-height: 1.8;">
---
در فصل نهم، به مبحث کار با پایگاه داده‌ها در PHP پرداخته خواهد شد. پایگاه داده‌ها یکی از اساسی‌ترین بخش‌های برنامه‌نویسی وب هستند و PHP به‌خوبی از انواع پایگاه داده‌ها پشتیبانی می‌کند. در این فصل، به بررسی نحوه اتصال به پایگاه داده، اجرای دستورات SQL، جلوگیری از حملات SQL Injection و تکنیک‌های بهینه‌سازی در کار با پایگاه داده خواهیم پرداخت.

### **فصل نهم: کار با پایگاه داده‌ها در PHP**

---

### **9.1 مقدمه‌ای بر کار با پایگاه داده‌ها**

پایگاه داده‌ها ابزاری برای ذخیره و مدیریت داده‌ها به صورت سازمان‌یافته هستند. در برنامه‌نویسی وب، پایگاه داده‌ها به برنامه‌ها این امکان را می‌دهند که اطلاعاتی مانند داده‌های کاربر، تنظیمات برنامه، تاریخچه تراکنش‌ها و سایر اطلاعات را ذخیره، بازیابی و مدیریت کنند. PHP به‌طور پیش‌فرض از چندین نوع پایگاه داده پشتیبانی می‌کند، از جمله MySQL، PostgreSQL، SQLite و SQL Server.

برای کار با پایگاه داده‌ها در PHP، معمولاً از سه روش اصلی استفاده می‌شود:

1. **استفاده از کتابخانه MySQLi** (به معنی MySQL Improved): برای کار با پایگاه داده MySQL به صورت بهینه و امن.
2. **استفاده از PDO (PHP Data Objects):** یک رابط جهانی برای کار با انواع مختلف پایگاه داده که به صورت شیءگرا عمل می‌کند.
3. **استفاده از SQLite:** برای برنامه‌های کوچک‌تر یا کاربردهایی که نیاز به یک پایگاه داده داخلی سبک دارند.

### **9.2 کار با MySQLi**

کتابخانه MySQLi یکی از محبوب‌ترین روش‌ها برای اتصال به پایگاه داده MySQL و اجرای دستورات SQL است. MySQLi هم به صورت رویه‌ای (procedural) و هم به صورت شیءگرا (OOP) قابل استفاده است. در اینجا هر دو روش مورد بررسی قرار می‌گیرند.

#### **9.2.1 اتصال به پایگاه داده با MySQLi (روش شیءگرا)**

برای اتصال به یک پایگاه داده MySQL، باید از کلاس `mysqli` استفاده کرد. این کلاس برای مدیریت اتصال به پایگاه داده و اجرای دستورات SQL استفاده می‌شود.

**مثال: اتصال به پایگاه داده MySQL:**

```php
<?php
$servername = "localhost"; // نام سرور
$username = "root"; // نام کاربری پایگاه داده
$password = ""; // رمز عبور پایگاه داده
$dbname = "testdb"; // نام پایگاه داده

// ایجاد اتصال
$conn = new mysqli($servername, $username, $password, $dbname);

// بررسی اتصال
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error); // نمایش پیام خطا در صورت عدم اتصال
} else {
    echo "Connected successfully";
}
?>
```

در این مثال، اتصال به پایگاه داده `testdb` در سرور محلی ایجاد شده است. در صورت عدم موفقیت در اتصال، پیامی نمایش داده می‌شود.

#### **9.2.2 اجرای دستورات SQL با MySQLi**

پس از اتصال موفق به پایگاه داده، می‌توان دستورات SQL را برای ایجاد، خواندن، به‌روزرسانی و حذف داده‌ها (CRUD) اجرا کرد.

**مثال: اجرای یک دستور SQL برای ایجاد جدول:**

```php
<?php
$sql = "CREATE TABLE users (
    id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(30) NOT NULL,
    email VARCHAR(50),
    reg_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
)";

// اجرای دستور SQL
if ($conn->query($sql) === TRUE) {
    echo "Table 'users' created successfully";
} else {
    echo "Error creating table: " . $conn->error;
}
?>
```

#### **9.2.3 خواندن داده‌ها از پایگاه داده**

برای خواندن داده‌ها از یک جدول، از دستور `SELECT` استفاده می‌شود. نتایج به‌دست‌آمده را می‌توان به شکل‌های مختلفی پردازش کرد.

**مثال: خواندن تمام رکوردها از جدول `users`:**

```php
<?php
$sql = "SELECT id, username, email FROM users";
$result = $conn->query($sql);

if ($result->num_rows > 0) {
    // خروجی هر ردیف
    while ($row = $result->fetch_assoc()) {
        echo "ID: " . $row["id"] . " - Username: " . $row["username"] . " - Email: " . $row["email"] . "<br>";
    }
} else {
    echo "0 results";
}
?>
```

#### **9.2.4 استفاده از دستورات آماده (Prepared Statements) برای امنیت بیشتر**

برای جلوگیری از حملات SQL Injection، باید از دستورات آماده استفاده کرد. این دستورات به شما اجازه می‌دهند تا مقادیر ورودی کاربران را به صورت امن به دستورات SQL اضافه کنید.

**مثال: استفاده از دستورات آماده برای جلوگیری از SQL Injection:**

```php
<?php
$stmt = $conn->prepare("INSERT INTO users (username, email) VALUES (?, ?)");
$stmt->bind_param("ss", $username, $email); // "ss" به معنای دو رشته (string)

$username = "JohnDoe";
$email = "johndoe@example.com";
$stmt->execute(); // اجرای دستور آماده

echo "New record created successfully";

$stmt->close(); // بستن دستور آماده
?>
```

### **9.3 کار با PDO (PHP Data Objects)**

PDO یک روش پیشرفته‌تر و انعطاف‌پذیرتر برای کار با پایگاه داده‌ها در PHP است که از چندین نوع پایگاه داده پشتیبانی می‌کند. PDO به‌صورت شیءگرا عمل می‌کند و از دستورات آماده (Prepared Statements) به خوبی پشتیبانی می‌کند.

#### **9.3.1 اتصال به پایگاه داده با استفاده از PDO**

**مثال: اتصال به پایگاه داده MySQL با PDO:**

```php
<?php
$dsn = "mysql:host=localhost;dbname=testdb"; // Data Source Name
$username = "root"; // نام کاربری پایگاه داده
$password = ""; // رمز عبور پایگاه داده

try {
    $conn = new PDO($dsn, $username, $password);
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connected successfully";
} catch (PDOException $e) {
    echo "Connection failed: " . $e->getMessage();
}
?>
```

#### **9.3.2 اجرای دستورات SQL با PDO**

**مثال: ایجاد یک جدول با استفاده از PDO:**

```php
<?php
$sql = "CREATE TABLE users (
    id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(30) NOT NULL,
    email VARCHAR(50),
    reg_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
)";

try {
    $conn->exec($sql);
    echo "Table 'users' created successfully";
} catch (PDOException $e) {
    echo "Error creating table: " . $e->getMessage();
}
?>
```

#### **9.3.3 استفاده از دستورات آماده در PDO**

**مثال: استفاده از دستورات آماده برای وارد کردن داده‌ها:**

```php
<?php
$sql = "INSERT INTO users (username, email) VALUES (:username, :email)";
$stmt = $conn->prepare($sql);

$stmt->bindParam(':username', $username);
$stmt->bindParam(':email', $email);

$username = "JaneDoe";
$email = "janedoe@example.com";
$stmt->execute();

echo "New record created successfully";
?>
```

### **9.4 بهینه‌سازی و نکات امنیتی در کار با پایگاه داده‌ها**

#### **9.4.1 استفاده از دستورات آماده (Prepared Statements)**

استفاده از دستورات آماده به شدت توصیه می‌شود تا از حملات SQL Injection جلوگیری شود. این دستورات به صورت پویا با داده‌های ورودی کار می‌کنند و داده‌های کاربر را به صورت امن به دستورات SQL اضافه می‌کنند.

#### **9.4.2 محدود کردن دسترسی به پایگاه داده**

همیشه از حداقل دسترسی‌های ممکن برای کاربران پایگاه داده استفاده کنید. برای مثال، یک کاربر که فقط نیاز به خواندن داده‌ها دارد، نباید دسترسی نوشتن داشته باشد.

#### **9.4.3 استفاده از تراکنش‌ها (Transactions)**

تراکنش‌ها برای اطمینان از اینکه چندین عملیات پایگاه داده به صورت اتمیک انجام می‌شوند (همه با هم یا هیچ‌کدام)، استفاده می‌شوند.

**مثال: استفاده از تراکنش‌ها در PDO:**

```php
<?php
try {
    $conn->beginTransaction(); // شروع تراکنش
    $conn->exec("INSERT INTO users (username, email) VALUES ('Alice', 'alice@example.com')");
    $conn->exec("INSERT INTO users (username, email) VALUES ('Bob', 'bob@example.com')");
    $conn->commit(); // تایید تراکنش
    echo "New records created successfully";
} catch (PDOException $e) {
    $conn->rollBack(); // لغو تراکنش در صورت خطا
    echo "Error: " . $e->getMessage();
}
?>
```

### **9.5 استفاده از SQLite در PHP**



SQLite یک پایگاه داده کوچک و سبک است که نیاز به نصب سرور ندارد و به‌صورت داخلی با PHP کار می‌کند. این پایگاه داده برای برنامه‌های کوچک و زمانی که به یک پایگاه داده ساده نیاز دارید، مناسب است.

**مثال: اتصال به پایگاه داده SQLite و ایجاد یک جدول:**

```php
<?php
try {
    $conn = new PDO("sqlite:mydatabase.db");
    $conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
    echo "Connected to SQLite database successfully.";

    $sql = "CREATE TABLE users (
        id INTEGER PRIMARY KEY,
        username TEXT NOT NULL,
        email TEXT NOT NULL
    )";
    $conn->exec($sql);
    echo "Table 'users' created successfully.";
} catch (PDOException $e) {
    echo "Error: " . $e->getMessage();
}
?>
```

### **9.6 تمرین‌های فصل نهم**

1. **اتصال به پایگاه داده MySQL:** برنامه‌ای بنویسید که به یک پایگاه داده MySQL متصل شود و یک جدول ایجاد کند.
2. **استفاده از دستورات آماده در MySQLi:** برنامه‌ای بنویسید که داده‌های کاربران را به صورت امن وارد یک جدول کند.
3. **استفاده از PDO برای خواندن داده‌ها:** برنامه‌ای بنویسید که از PDO برای خواندن داده‌ها از یک جدول استفاده کند.
4. **مدیریت خطاها و تراکنش‌ها در پایگاه داده:** برنامه‌ای بنویسید که چندین دستور SQL را به صورت تراکنش اجرا کند و در صورت بروز خطا، تراکنش را لغو کند.
5. **کار با SQLite:** برنامه‌ای بنویسید که با استفاده از SQLite یک پایگاه داده ایجاد کرده و داده‌ها را مدیریت کند.

### **خلاصه فصل نهم**

در این فصل، با نحوه کار با پایگاه داده‌ها در PHP آشنا شدید. روش‌های مختلفی برای اتصال به پایگاه داده‌ها و اجرای دستورات SQL بررسی شد. همچنین، نکات امنیتی و بهینه‌سازی برای کار با پایگاه داده‌ها توضیح داده شدند. استفاده از MySQLi و PDO، دو روش رایج برای ارتباط با پایگاه داده‌ها هستند که هر دو امکاناتی برای مدیریت ایمن و کارآمد داده‌ها فراهم می‌کنند. در نهایت، به SQLite به عنوان یک گزینه سبک و داخلی برای ذخیره داده‌ها پرداخته شد.

---


</div>