# 学习笔记

##### 远程连接数据库--1130

​	首先把localhost更改为%

![插入图片](https://raw.githubusercontent.com/sjwyqr/Learning-Laravel/master/imges/%E6%9B%B4%E6%94%B9%E7%94%A8%E6%88%B7.png)

​	然后刷新权限

```mysql
flush privileges; 
```

##### 配置文件

![插入图片](https://raw.githubusercontent.com/sjwyqr/Learning-Laravel/master/imges/%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6.png)

##### laravel框架更改配置

```php
1、时区#'timezone' => 'UTC',#Asia/Shanghai   'timezone' => 'Asia/Shanghai',
2、语言#'locale' => 'en',	'locale' => 'zh-CN',
```

##### 创建自己的辅助函数

我们把所有的『自定义辅助函数』存放于 `bootstrap/helpers.php` 文件中，这里需要新建一个空文件：

```php
touch bootstrap/helpers.php
#Linux 的 touch touch命令有两个功能：一是用于把已存在文件的时间标签更新为系统当前的时间（默认方式），它们的数据将原封不动地保留下来；二是用来创建新的空文件。
```

**辅助函数需要在 `bootstrap/app.php` 文件的最顶部进行加载：**

```php
#bootstrap/app.php
require_once __DIR__ . '/helpers.php';
```

##### 视图文件知识

![视图文件知识-1](https://raw.githubusercontent.com/sjwyqr/Learning-Laravel/master/imges/%E8%A7%86%E5%9B%BE%E6%96%87%E4%BB%B6%E7%9F%A5%E8%AF%86-1.png)

##### 加载模版

![加载模版](https://raw.githubusercontent.com/sjwyqr/Learning-Laravel/master/imges/%E5%8A%A0%E8%BD%BD%E6%A8%A1%E7%89%88.png)

## 页面展示全过程

​	1、创建控制器

```php
php artisan make:controller PagesController
--------------------------------------------------------------
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;

class PagesController extends Controller
{
    public function root()
    {
        return view('pages.root');
    }
}
```

​	2、视图

```php
创建视图	resources/views/pages/root.blade.php
----------------------------------
@extends('layouts.app')
@section('title', '首页')

@section('content')
  <h1>这里是首页</h1>
@stop
```

​	3、绑定路由

```php
routes/web.php
  ----------------------------------
Route::get('/', 'PagesController@root')->name('root');
```

##### 注册与登录

###### 用户认证脚手架

```php
#Laravel 自带了用户认证功能
php artisan make:auth
#命令 make:auth 会询问我们是否要覆盖 app.blade.php，因为我们在前面章节中已经自定义了『主要布局文件』—— app.blade.php，所以此处输入 no
```

###### Blade 模板引擎???

###### `POST` 类型表单时注意事项

```php
#当用户点击『退出登录』按钮时，触发 JS 提交『退出登录表单』—— logout-form 。注意提交 POST 类型表单时需要一并提交 CSRF 令牌。
<form id="logout-form" action="{{ route('logout') }}" method="POST" style="display: none;">
    {{ csrf_field() }}
</form>
```

##### 执行数据库迁移时报错，提示表已经存在

在 AppServiceProvider.php, boot方法中, 调用 Schema::defaultStringLength 方法

```php
use Illuminate\Support\Facades\Schema;

/**
 * Bootstrap any application services.
 *
 * @return void
 */
public function boot()
{
    Schema::defaultStringLength(191);
```

----------------------------------------------

​																				2018年3月28日

------------------------------------------

