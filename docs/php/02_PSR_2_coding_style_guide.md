# PSR-2 Coding Style Guide

[Tài liệu gốc](http://www.php-fig.org/psr/psr-2/)

Tài liệu này mở rộng từ tài liệu [PSR-1](01_PSR_1_basic_coding_standard.md) (basic coding standard).

Mục đích của tài liệu này là nhằm giảm bớt những khó khăn trong việc đọc code của người khác bằng cách đặt ra những quy định hay gợi
ý về việc format PHP code.

## 1. Khái quát chung

- Code PHẢI tuân thủ "basic coding standard" [PSR-1](01_PSR_1_basic_coding_standard.md).

- Code PHẢI dùng 4 spaces (soft-tab) để indent, KHÔNG ĐƯỢC dùng tab (hard-tab).

- KHÔNG ĐƯỢC áp dụng giới hạn cứng (hard-limit) về độ dài của một dòng; giới hạn mềm (soft-limit) PHẢI là 120 kí tự. Một dòng NÊN có tối đa 80 kí tự.

- Sau phần khai báo `namespace` PHẢI có một dòng trống (blank line). Sau phần khai báo `use` cũng PHẢI có một dòng trống.

- Khi khai báo class, dấu mở ngoặc nhọn sau tên class PHẢI được viết ở dòng mới (new line). Dấu đóng ngoặc nhọn cũng PHẢI viết ở dòng mới sau khi kết thúc class.

- Khi khai báo method, dấu mở ngoặc nhọn sau tên method PHẢI được viết ở dòng mới. Dấu đóng ngoặc nhọn cũng PHẢI viết ở dòng mới sau khi kết thúc method.

- Khi khai báo properties và methods, PHẢI khai báo từ khóa phạm vi (visibility) như `public`, `protected` hoặc `private`. Từ khóa `abstract` và `final` PHẢI được khai báo trước từ khóa phạm vi. Từ khóa `static` PHẢI khai báo sau từ khóa phạm vi.

- Khi dùng các cấu trúc điều khiển (control structures), sau từ khóa (ví dụ như `if`, `else`, `for` ...) PHẢI có một dấu cách. Ngược lại, KHÔNG ĐƯỢC có dấu cách sau tên method khi gọi.

- Khi dùng các cấu trúc điều khiển, dấu mở ngoặc nhọn PHẢI được viết cùng dòng với từ khóa. Ngược lại dấu đóng ngoặc nhọn PHẢI viết ở dòng mới.

- Khi dùng các cấu trúc điều khiển, dấu mở ngoặc đơn sau từ khóa KHÔNG ĐƯỢC có dấu cách theo sau. Dấu đóng ngoặc đơn KHÔNG ĐƯỢC có dấu cách ở trước.

### 1.1. Ví dụ

Đoạn code ví dụ dưới đây đã bao gồm các quy tắc được đề cập ở phần trên:

```php
<?php
namespace Vendor\Package;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    public function sampleFunction($a, $b = null)
    {
        if ($a === $b) {
            bar();
        } elseif ($a > $b) {
            $foo->bar($arg1);
        } else {
            BazClass::bar($arg2, $arg3);
        }
    }

    final public static function bar()
    {
        // method body
    }
}
```

## 2. Tổng thể


### 2.1 Basic Coding Standard

Code PHẢI tuân thủ [PSR-1](01_PSR_1_basic_coding_standard.md).

### 2.2 Files

Mọi PHP files PHẢI dùng Unix LF (linefeed) line ending.

Mọi PHP files PHẢI kết thúc bằng một dòng trống.

Trong một file chỉ bao gồm code PHP thì KHÔNG ĐƯỢC viết tag đóng `?>`.

### 2.3. Lines

KHÔNG ĐƯỢC áp dụng hard limit về độ dài của một dòng. Chương trình check style tự động KHÔNG ĐƯỢC báo error về độ dài dòng.

Soft limit về độ dài của một dòng PHẢI là 120 kí tự. Chương trình check style tự động PHẢI báo warning nhưng KHÔNG ĐƯỢC báo
error khi vượt quá soft limit.

Một dòng KHÔNG NÊN có quá 80 kí tự. Dòng mà dài quá 80 kí tự thì NÊN chia nhỏ ra thành nhiều dòng với độ dài mỗi dòng
không quá 80 kí tự.

Một dòng không trống KHÔNG ĐƯỢC có trailing whitespace (dấu cách ở cuối dòng).

Dòng trống CÓ THỂ được thêm vào code để dễ đọc hơn và để phân cách những đoạn code.

KHÔNG ĐƯỢC có quá một statement trên một dòng.

Ví dụ:

```php
if ($a == $b) { if ($a == $c) { // Hai "if" ở cùng một dòng
// ...
}}
```

### 2.4. Canh lề - Indenting

Code KHÔNG ĐƯỢC dùng tab, mà PHẢI sử dụng 4 dấu cách làm indent.

### 2.5. Keywords và True/False/Null

Những [keywords](http://php.net/manual/en/reserved.keywords.php) của PHP PHẢI được viết thường. (không viết hoa)

Ví dụ: 

```php
IF ($a == $b) { từ khóa "IF" không được viết hoa
// ...
}
```

Những constants của PHP là `true`, `false`, và `null` cũng PHẢI viết thường.

## 3. Khai báo Namespace và Use

Cần PHẢI có một dòng trắng phía sau khai báo `namespace`.

Những phần khai báo `use` PHẢI được đặt phía sau phần khai báo `namespace`.

PHẢI dùng một từ `use` cho mỗi khai báo.

PHẢI có một dòng trắng phía sau đoạn code `use`.

Ví dụ sau đây đã tuân theo những quy ước trên:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

// ... additional PHP code ...
```


Ví dụ sau đây không tuân theo những quy ước trên (ví dụ sai):

```php
<?php
namespace Vendor\Package; // Sau khai báo namespace không có một dòng trống
use FooClass; use BarClass as Bar; // Sử dụng 2 khai báo use ở cùng một dòng
use OtherVendor\OtherPackage\BazClass; // Sau khai báo use không có một dòng trống
// ... additional PHP code ...
```

## 4. Classes, Properties, và Methods

Từ `class` dưới đây được hiểu là cả những `class` bình thường, `interfaces` và `traits`.

### 4.1. Extends và Implements

Từ khoá `extends` và `implements` PHẢI được viết cùng dòng với tên class.

Dấu mở ngoặc nhọn của class PHẢI đứng trên một dòng riêng. Dấu đóng ngoặc phải được viết ở dòng sau của phần body. Ví dụ:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements \ArrayAccess, \Countable
{
    // constants, properties, methods
}
```

Danh sách những interface được `implements` CÓ THỂ được viết trên nhiều dòng, trong đó mỗi dòng theo sau được indent 1 lần. Khi thực hiện việc đó thì tên interface đầu tiên PHẢI được đặt trên 1 dòng mới, và mỗi dòng KHÔNG ĐƯỢC có quá 1 interface. 

Ví dụ:

```php
<?php
namespace Vendor\Package;

use FooClass;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class ClassName extends ParentClass implements
    \ArrayAccess,
    \Countable,
    \Serializable
{
    // constants, properties, methods
}
```

### 4.2. Properties

Từ khóa phạm vi (visibility) PHẢI được khai báo ở mọi property.

KHÔNG ĐƯỢC dùng từ khoá `var` để khai báo một property.

Trong một dòng thì KHÔNG ĐƯỢC khai báo quá một property.

Tên property KHÔNG NÊN có prefix là dấu gạch dưới `_` để biểu thị tính protected hay private.

Ví dụ:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public $foo = null;
}
```

### 4.3. Methods

Từ khóa phạm vi (visibility) PHẢI được khai báo ở mọi properties method.

Tên method KHÔNG NÊN có prefix là dấu gạch dưới `_` để biểu thị tính protected hay private.

Khi khai báo tên method thì KHÔNG ĐƯỢC để một khoảng trắng ở phía sau tên method. Dấu mở ngoặc nhọn PHẢI nằm trên một dòng riêng, và dấu đóng ngoặc cũng PHẢI nằm ở dòng riêng ngay sau khi kết thúc method.

KHÔNG ĐƯỢC có khoảng trắng sau dấu mở ngoặc tròn và dấu đóng ngoặc tròn (khi khai báo tham số của method).

Ví dụ (chú ý đến vị trí của dấu ngặc đơn, dấu phẩy, khoảng trắng và dấu ngoặc nhọn):

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function fooBarBaz($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }

    public function fooNoParam()
    {
        // method body
    }
}
```

### 4.4. Method Arguments

Trong danh sách tham số của method thì KHÔNG ĐƯỢC có khoảng trắng trước mỗi dấu phẩy, và phải có một khoảng trắng sau mỗi dấu phẩy.

Những tham số mà có giá trị mặc định PHẢI được đặt ở cuối danh sách.

Ví dụ:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function foo($arg1, &$arg2, $arg3 = [])
    {
        // method body
    }
}
```

Danh sách tham số CÓ THỂ được tách thành nhiều dòng, trong đó mỗi dòng theo sau được indent một lần. Khi làm vậy thì tham số đầu tiên trong danh sách PHẢI được đặt ở trên một dòng mới, và mỗi dòng KHÔNG ĐƯỢC có quá một tham số.

Khi mà danh sách tham số được chia làm nhiều dòng, thì dấu đóng ngoặc tròn và dấu mở ngoặc nhọn PHẢI được đặt cùng nhau trên một dòng, với một khoảng trắng ở giữa.

Ví dụ:

```php
<?php
namespace Vendor\Package;

class ClassName
{
    public function aVeryLongMethodName(
        ClassTypeHint $arg1,
        &$arg2,
        array $arg3 = []
    ) {
        // method body
    }
}
```

### 4.5. `abstract`, `final`, và `static`

Khi được sử dụng, từ khóa `abstract` và `final` PHẢI được đặt trước từ khóa phạm vi (visibility).

Khi được sử dụng, từ khóa `static` PHẢI được đặt sau từ khóa phạm vi (visibility).

Ví dụ:

```php
<?php
namespace Vendor\Package;

abstract class ClassName
{
    protected static $foo;

    abstract protected function zim();

    final public static function bar()
    {
        // method body
    }
}
```

### 4.6. Gọi Method và Function

Khi gọi một method hay một function, KHÔNG ĐƯỢC có khoảng trắng giữa tên của method hay function và dấu mở ngoặc tròn.

KHÔNG ĐƯỢC có khoảng trắng sau dấu mở ngoặc tròn và trước dấu đóng ngoặc tròn.

Trong danh sách tham số, KHÔNG ĐƯỢC có khoảng trắng trước mỗi dấu phẩy, và PHẢI có một khoảng trắng sau mỗi dấu phẩy.

Ví dụ:

```php
<?php
bar();
$foo->bar($arg1);
Foo::bar($arg2, $arg3);
```

Danh sách tham số CÓ THỂ được tách ra thành nhiều dòng, trong đó mỗi dòng theo sau được indent một lần. Khi làm như vậy thì tham số đầu tiên PHẢI được đặt trên một dòng mới, và mỗi dòng KHÔNG ĐƯỢC có quá một tham số.

Ví dụ:

```php
<?php
$foo->bar(
    $longArgument,
    $longerArgument,
    $muchLongerArgument
);
```

## 5. Control Structures

Những quy tắc chung khi viết các cấu trúc điều khiển control structure (ví dụ `if`, `else`, `for`, ...) bao gồm:

- PHẢI có một khoảng trắng sau từ khóa.
- KHÔNG ĐƯỢC có khoảng trắng sau dấu mở ngoặc tròn.
- KHÔNG ĐƯỢC có khoảng trắng trước dấu đóng ngoặc tròn.
- PHẢI có một khoảng trắng sau đấu đóng ngoặc tròn và trước dấu mở ngoặc nhọn.
- Phần thân của structure PHẢI được indent một lần.
- Dấu đóng ngoặc nhọn PHẢI được đặt trên một dòng mới sau phần thân.

Phần thân của mỗi structure PHẢI được đặt trong dấu đóng mở ngoặc kép. Điều này sẽ làm tiêu chuẩn hoá cách viết structures và làm giảm thiểu việc phát sinh ra lỗi khi mà có những dòng mới được thêm vào phần thân.

Ví dụ điều này là sai mặc dù không sai về mặt ngôn ngữ:

```php
<?php
if ($a == $b) doSomething();
```

PHẢI đặt phần thân cấu trúc trong dấu đóng mở ngoặc kép:

```php
<?php
if ($a == $b) {
    doSomething();
}
```

### 5.1. `if`, `elseif`, `else`

Một cấu trúc `if` được viết như sau (hãy chú ý đến vị trí của dấu ngoặc tròn, khoảng trắng, dấu ngoặc nhọn. `else` và `elseif` được đặt trên cùng một dòng với dấu đóng ngoặc nhọn của phần body phía trước):

```php
<?php
if ($expr1) {
    // if body
} elseif ($expr2) {
    // elseif body
} else {
    // else body;
}
```

Từ khoá `elseif` NÊN được dùng thay cho `else if`, để mọi từ khóa chỉ là một từ đơn.

### 5.2. `switch`, `case`

Một cấu trúc `switch` được viết như sau (hãy chú ý đến vị trí của dấu ngoặc tròn, khoảng trắng và dấu ngoặc nhọn):

```php
<?php
switch ($expr) {
    case 0:
        echo 'First case, with a break';
        break;
    case 1:
        echo 'Second case, which falls through';
        // no break
    case 2:
    case 3:
    case 4:
        echo 'Third case, return instead of break';
        return;
    default:
        echo 'Default case';
        break;
}
```

Phần `case` PHẢI được indent một lần so với `switch`, và `break` keyword (hay các keyword ngắt khác) PHẢI được indent giống
với phần thân của `case`.

PHẢI có một comment ví dụ như `// no break` nếu phần thân của `case` không trống, và được cố tình cho qua (không có break).

### 5.3. `while`, `do while`

Một cấu trúc `while` được viết như sau (hãy chú ý vào vị trí của dấu ngoặc tròn, khoảng trắng và dấu ngoặc nhọn):

```php
<?php
while ($expr) {
    // structure body
}
```

Tương tự như vậy, một cấu trúc `do while` được viết như sau (hãy chú ý vào vị trí của dấu ngoặc tròn, khoảng trắng và dấu ngoặc nhọn):

```php
<?php
do {
    // structure body;
} while ($expr);
```

### 5.4. `for`

Một cấu trúc `for` được viết như sau (hãy chú ý vào vị trí của dấu chấm phẩy, dấu ngoặc tròn, khoảng trắng và dấu ngoặc nhọn):

```php
<?php
for ($i = 0; $i < 10; $i++) {
    // for body
}
```

### 5.5. `foreach`

Một cấu trúc `foreach` được viết như sau (hãy chú ý vào vị trí của `=>`, dấu ngoặc tròn, khoảng trắng và dấu ngoặc nhọn):

```php
<?php
foreach ($iterable as $key => $value) {
    // foreach body
}
```

## 5.6. `try`, `catch`

Một block `try catch` được viết như sau (hãy chú ý vào vị trí của dấu ngoặc tròn, khoảng trắng và dấu ngoặc nhọn):

```php
<?php
try {
    // try body
} catch (FirstExceptionType $e) {
    // catch body
} catch (OtherExceptionType $e) {
    // catch body
}
```

# 6. Closures

Closures PHẢI được định nghĩa với một khoảng trắng phía sau keywork `function`, và một khoảng trắng ở phía trước cũng
như phía sau của keyword `use`.

Dấu mở ngoặc ngọn PHẢI được đặt ở cùng dòng, và dấu đóng ngoặc nhọn PHẢI được đặt ở một dòng mới phía sau phần thân.

KHÔNG ĐƯỢC có một khoảng trắng ở phía sau dấu mở ngoặc tròn của phần khai báo danh sách argument hay variable,
và KHÔNG ĐƯỢC có một khoảng trắng ở phía trước dấu đóng ngoặc tròn của phần khai báo danh sách argument hay variable.

Trong danh sách arugment hay variable, KHÔNG ĐƯỢC có khoảng trắng trước mỗi dấu phẩy, và PHẢI có một khoảng trắng
phía sau mỗi dấu phẩy.

Arguments của Closure mà có giá trị mặc định thì PHẢI được đặt ở cuối của danh sách argument.

Cách định nghĩa một closure trông như sau (hãy chú ý vào vị trí của dấu ngoặc tròn, dấu phẩy, khoảng trắng và dấu ngoặc nhọn):

```php
<?php
$closureWithArgs = function ($arg1, $arg2) {
    // body
};

$closureWithArgsAndVars = function ($arg1, $arg2) use ($var1, $var2) {
    // body
};
```

Danh sách argument và danh sách variable có thể được tách ra làm nhiều dòng, trong đó mỗi dòng theo sau được indent một lần. Khi làm như vậy thì argument hay variable đầu tiên PHẢI được đặt ở trên một dòng mới, và mỗi dòng KHÔNG ĐƯỢC có quá một argument hay một variable.

Khi mà kết thúc của danh sách (kể cả arguments hay variables) được chia thành nhiều dòng, thì dấu đóng ngoặc tròn và dấu mở ngoặc nhọn PHẢI được đặt cùng nhau trên một dòng, với một khoảng trắng ở giữa.

Dưới đây là những ví dụ về các closures có và không có danh sách argument hay variable được chia thành nhiều dòng:

```php
<?php
$longArgs_noVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) {
   // body
};

$noArgs_longVars = function () use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_longVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};

$longArgs_shortVars = function (
    $longArgument,
    $longerArgument,
    $muchLongerArgument
) use ($var1) {
   // body
};

$shortArgs_longVars = function ($arg) use (
    $longVar1,
    $longerVar2,
    $muchLongerVar3
) {
   // body
};
```

Chú ý rằng những quy tắc trên còn được áp dụng khi một closure được sử dụng trục tiếp như một argument trong một lời gọi
hàm hay method.

```php
<?php
$foo->bar(
    $arg1,
    function ($arg2) use ($var1) {
        // body
    },
    $arg3
);
```


## 7. Kết luận

Có nhiều yếu tố về style hay practice khác được cố tình bỏ qua hoặc không đề cập toàn bộ trong tài liệu này. Ví dụ như:

- Khai báo biến toàn cục (global variables) hay hằng số global (global constants)
- Khai báo hàm (functions)
- Toán tử và phép gán
- Liên kết dòng (inter-line alignment)
- Khối comment và docBlock
- Tiền tố và hậu tố trong cách đặt tên
- Best practices

Ngoài ra, những quy ước kể trên CÓ THỂ được xem xét lại và mở rộng hoặc thay đổi trong các tài liệu khác.