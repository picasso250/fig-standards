基本编码规范
=====================

当进行多人协作时，代码规范的要点列如下：

The key words "MUST"（必、务必）, "MUST NOT"（切勿）, "REQUIRED"（需要）, "SHALL"（将）, "SHALL NOT"（不要）, "SHOULD"（应该）,
"SHOULD NOT"（不应该）, "RECOMMENDED"（建议）, "MAY"（可以）, and "OPTIONAL"（可选） in this document are to be
interpreted as described in [RFC 2119][].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md


1. 总览
-----------

- 只使用 `<?php` 和 `<?=` 标签。

- PHP 代码文件要采用不带 BOM 头的 UTF-8 格式。

- 一个代码文件**要么**声明一些符号（类、函数、常量等），**要么**产生副作用（如输出，改变 .ini 设置等），二者择其一，不可俱全。

- 命名空间和类的规范务必遵循 [PSR-0][]。

- 类名是双峰驼式 `StudlyCaps`。

- 类常量必是全大写，以下划线分隔。

- 方法名是单峰驼式 `camelCase`。


2. 文件
--------

### 2.1. PHP 标签

PHP 代码必须使用长标签： `<?php ?>` 或者短的输出标签： `<?= ?>` ；其他标签皆禁止。

### 2.2. 字符编码

PHP 代码必须使用无 BOM 头的 UTF-8 格式。

### 2.3. 副作用

一个代码文件**要么**声明一些符号（类、函数、常量等），**要么**执行逻辑、产生副作用（如输出，改变 .ini 设置等），二者择其一，不可俱全。

**副作用**
The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

**副作用**包括但不限于：输出、显式使用 `require` 或 `include` 、调用外部服务、修改 ini 文件、引起错误或者例外、修改全局变量、读取或者写入文件，等等。

以下是一个既包括声明又包括副作用的文件；请尽力避免：

```php
<?php
// 副作用：改变 ini 设置
ini_set('error_reporting', E_ALL);

// 副作用：加载文件
include "file.php";

// 副作用：输出
echo "<html>\n";

// 声明
function foo()
{
    // function body
}
```

以下是一个只包含声明，不包含副作用的文件；请学习：

```php
<?php
// 声明
function foo()
{
    // function body
}

// 条件声明**不**属于副作用
if (! function_exists('bar')) {
    function bar()
    {
        // function body
    }
}
```


3. 命名空间和类名
----------------------------

命名空间和类名必须遵循 [PSR-0][].

这意味着每个类独立成文，且包含在一个顶层的 vendor 里。

类名是双峰驼式 `StudlyCaps`。

5.3 之后的代码必须使用正式的命名空间。

如：

```php
<?php
// PHP 5.3 and later:
namespace Vendor\Model;

class Foo
{
}
```

4. 类的常量、属性和方法
-------------------------------------------

今所提到的**类**意指所有的类、接口和特质。

### 4.1. 常量

类常量名必是全大写，以下划线分隔。

如：

```php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
```

### 4.2. 属性

本册无意评价下述三种写法的优劣。

- `$StudlyCaps`
- `$camelCase`
- `$under_score` 

无论何种命名习惯，都应在自己的变量作用域中保持一致。所谓变量作用域可能是 vendor-level, package-level, class-level, 也可能是 method-level.

### 4.3. 方法

方法名是单峰驼式 `camelCase`。
