# PSR-4 Autoloader

[Tài liệu tham khảo](https://www.php-fig.org/psr/psr-4/)

## 0. Autoloading

[Tài liệu tham khảo](https://www.php.net/autoload).

Kĩ thuật nạp tự động (autoloading) cho phép các classes hoặc interfaces khác được nạp một cách tự động nếu nó chưa được định nghĩa.

Ví dụ, đoạn mã sau sẽ báo lỗi vì class `Bar` không được nạp/load:

```php
<?php
Bar::example();
```

Theo cách làm cũ, ta cần load class `Bar` như sau:

```php
<?php
include 'foo/bar.php';

Bar::example();
```

Autoloading sẽ tránh được việc khai báo `include` quá nhiều ở mỗi file code. Bằng việc sử dụng autoloading, PHP sẽ tìm cách thử load class hoặc interface lần cuối, trước khi tung error. 

Ví dụ:

```php
<?php
use Foo\Bar;

Bar::example();

// hoặc
\Foo\Bar::example();
```

`Autoloader` hay `autoloading classes` là những class được dùng để thực hiện kĩ thuật autoloading.

## 1. Khái quát chung

Tài liệu này mô tả kĩ thuật nạp tự động (autoload). Ngoài ra, tài liệu này cũng mô tả vị trí đặt của những file sẽ được autoload.

## 2. Đặc tả kĩ thuật

**1. Khái niệm `class` ở đây ám chỉ các khái niệm `class`, `interface`, `trait` và những cấu trúc tương tự.**

**2. Tên đầy đủ của một class (fully qualified classname) sẽ có dạng như sau**

```
\<NamespaceName>(\<SubNamespaceNames>)*\<ClassName>
```

  1. Tên đầy đủ của class PHẢI có một top-level namespace hay còn gọi là `vendor namespace` (thường được biết đến là tên package).
  2. Tên đầy đủ của class CÓ THỂ có một hoặc nhiều tên `sub-namespace`.
  3. Tên đầy đủ của class PHẢI có một tên đại diện hay còn gọi là `short name` hoặc `base name`.
  4. Dấu gạch dưới (underscores `_`) không có ý nghĩa đặc biệt ở bất cứ vị trí nào của tên đầy đủ.
  5. Các kí tự chữ (Alphabetic characters) trong tên đầy đủ CÓ THỂ kết hợp tùy ý chữ hoa và chữ thường.
  6. Tất cả tên ở các cấp PHẢI phân biệt về chữ hoa chữ thường (nghĩa là tên \foo\bar và \Foo\Bar là hai tên khác nhau).

**3. Sự tương ứng giữa một tên đầy đủ và đường dẫn (khi load một file)**

  1. Một chuỗi liên tiếp (hay còn gọi là `namespace prefix`), bao gồm tên top-level namsepace, một hoặc nhiều tên sub-namespace, từ tên đầy đủ của class sẽ tương ứng với một thư mục gốc hay `base directory`. Trong thực tế, việc này sẽ được đăng ký từ trước. Ví dụ:

``` json
# composer.json

"psr-4" {
    "App\\": "app/"
}
```

  2. Các tên sub-namespace liên tiếp sau tên `namespace prefix` sẽ tương ứng với các thư mục con trong thư mục gốc. Trong đó việc phân chia các sub-namespace cũng tương ứng với việc phân chia thư mục con. Tên của các thư mục con PHẢI khớp (cả về chữ hoa chữ thường) với tên của sub-namespace.
  3. Tên đại diện (hay `basename`) tương ứng với một file với đuôi `.php`. Tên của file PHẢI khớp (cả về chữ hoa chữ thường) với basename của class.

**4. Hoạt động của Autoloader KHÔNG ĐƯỢC trả về ngoại lệ, KHÔNG ĐƯỢC xuất hiện lỗi ở bất cứ cấp độ nào, và KHÔNG NÊN trả về giá trị**

## 3. Ví dụ

Bảng dưới đây thể hiện sự tương ứng giữa đường dẫn của file source code và tên đầy đủ của class, giữa `namespace prefix` và `base directory`

| FULLY QUALIFIED CLASS NAME | NAMESPACE PREFIX | BASE DIRECTORY | RESULTING FILE PATH |
| ----------- | ----------- | ----------- | ----------- |
| \Acme\Log\Writer\File_Writer | Acme\Log\Writer | ./acme-log-writer/lib/ | ./acme-log-writer/lib/File_Writer.php |
| \Aura\Web\Response\Status | Aura\Web | /path/to/aura-web/src/ | /path/to/aura-web/src/Response/Status.php |
| \Symfony\Core\Request | Symfony\Core | ./vendor/Symfony/Core/ | ./vendor/Symfony/Core/Request.php |
| \Zend\Acl | Zend | /usr/includes/Zend/ | /usr/includes/Zend/Acl.php |
