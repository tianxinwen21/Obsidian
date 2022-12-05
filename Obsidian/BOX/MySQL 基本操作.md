#input
# MySQL 基本操作

* 数据库的基本操作：创建数据库、删除数据库
* 常用数据类型
* 表的操作：创建表、删除表



## 1. 数据库的操作

*所有的命令大小写都可*

### 1.1 显示当前的数据库

```c
show databases;
```

### 1.2 创建数据库

语法：

```mysql
create database [if not exists] java106
[create_specification [, create_specification] ...]

create_specification:
 [default] character set charset_name
 [defualt] collate collation_name
```

说明：

* []是可选项
* character set :指定数据库采用的字符集
* collate：指定数据库字符集的校验规则

示例：

> 当我们创建数据库没有指定字符集和校验规则时，系统使用默认字符集：utf8，校验规则 是：utf8_ general_ ci

* 创建一名叫`java106_0`的数据库:

```c
create database java106_0;
```

* 如果系统没有`java106_1`的数据库，则创建一个名叫`java106_1`的数据库，如果有则不创建:

```c
create database if not exist java106_1;
```

* 如果系统没有`java106_2`的数据库，则创建一个使用utf8mb4字符集的`java106_2`数据库，如果有则 不创建:

```c
creat database if not exists java106_2 character set utf8mb4;
```

**[注意]**

MySQL的`utf8`编码不是真正的`utf8`，没有包含某些复杂的中文字符。MySQL真正的`utf8`是 使用`utf8mb4`，建议大家都使用`utf8mb4`。

### 1.3 使用数据库

```
use 数据库名；
```

### 1.4 删除数据库

```
drop database [if exists] java106;
```

数据库删除以后，内部看不见对应的数据库，里边的表和数据全部被删除。



## 2. 常用数据类型

