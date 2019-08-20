# PSR-1 Basic Coding Standard

[Tài liệu tham khảo](http://www.php-fig.org/psr/psr-1/)

Tài liệu này trình bày những quy ước cơ bản để đảm bảo tính thống nhất giữa các file code PHP.

## 1. Khái quát chung

- Files PHẢI sử dụng thẻ `<?php` hoặc `<?=` 

- Files PHẢI sử dụng encode: UTF-8 không có BOM (byte-order mark)

- Trong một file có thể định nghĩa symbols (classes, functions, constants, etc.), hoặc gây ra side-effects (e.g. tạo ra output, thay đổi .ini settings, etc.), nhưng KHÔNG NÊN làm cả hai.

- Namespaces và tên classes PHẢI tuân theo quy chuẩn "autoloading" của PSR: [PSR-0](http://www.php-fig.org/psr/psr-0/), [PSR-4](http://www.php-fig.org/psr/psr-4/).

- Tên class PHẢI được viết dưới dạng `StudlyCaps`.

- Tên constants của class PHẢI được viết dưới dạng `ALL_UPPER_CASE_WITH_UNDERSCORE`.

- Tên method PHẢI được viết dưới dạng `camelCase`.


## 2. Files


### 2.1. PHP Tags

Trong các file có chứa code PHP, đoạn code PHP PHẢI sử dụng tag đầy đủ `<?php ?>` hoặc short-echo tag `<?= ?>` .
Ngoài ra không được sử dụng những tag khác. (Ví dụ không dùng tag `<? ?>`)

### 2.2. Character Encoding

PHP code phải được encode bằng UTF-8 không có BOM.

### 2.3. Side Effects

Trong một file có thể định nghĩa symbols (classes, functions, constants, etc.), hoặc gây ra side-effects (e.g. tạo ra output, thay đổi .ini settings, etc.), nhưng KHÔNG NÊN làm cả hai.

Cụm từ "side effects" mang ý nghĩa là thực hiện những logic mà không liên quan trực tiếp đến việc định nghĩa classes, functions, constants ... *thường là từ việc including file*

"Side effects" bao gồm những việc sau (không phải là tất cả): tạo output, sử dụng `require`  `include`, hoặc kết nối đến external services, thay đổi file ini setting, emit errors hay exceptions, chỉnh sửa biến global hay static, đọc và viết file ...

Dưới đây là một ví dụ về việc một file chứa cả declarations (định nghĩa) và side effects (KHÔNG NÊN):

```php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
```

Dưới đây là ví dụ về một file chỉ bao gồm declarations mà không có side effects (NÊN):

```php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```


## 3. Namespace và tên Class

Namespaces và tên classes PHẢI tuân theo quy chuẩn "autoloading" của PSR: [PSR-0](http://www.php-fig.org/psr/psr-0/), [PSR-4](http://www.php-fig.org/psr/psr-4/).

Điều này có nghĩa là mỗi class PHẢI được viết vào một file, và phải có ý nhất 1 level trong namespace.

Tên class PHẢI được viết dưới dạng `StudlyCaps`.

Code với phiên bản PHP 5.3 trở lên PHẢI dùng đúng namespaces.

Chẳng hạn:

```php
<?php
// PHP 5.3 and later:
namespace Vendor\Model;

class Foo
{
}
```

Code với phiên bản 5.2.x trở xuống NÊN dùng pseudo-namespace với `Vendor_` là prefix.

```php
<?php
// PHP 5.2.x and earlier:
class Vendor_Model_Foo
{
}
```

## 4. Class Constants, Properties, và Methods

Từ class dưới đây được hiểu là cả những class bình thường, hay cả interfaces và traits.

### 4.1. Constants

Constants của class PHẢI được viết hoa toàn bộ và sử dụng gạch dưới ngăn cách giữa các từ. Ví dụ:

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '3.4';
    const DATE_APPROVED = '2014-03-04';
}
```

### 4.2. Properties

Bộ quy tắc này không đưa ra quy định hay gợi ý về việc nên viết properties như thế nào, có thể TÙY CHỌN một trong các dạng sau:

- `$StudlyCaps` ví dụ `$USER_PROFILE`
- `$camelCase` ví dụ `$userProfile`
- `$under_score` ví dụ `$user_profile`

Dù sử dụng quy tắc đặt tên nào đi chăng nữa thì nó cần phải được thực hiện thống nhất trong
một vendor, package, class, method ...

### 4.3. Methods

Tên Method PHẢI được viết dưới dạng `camelCase`. Ví dụ:

```php
<?php
public function getUserProfile() {
    // method body
}
```