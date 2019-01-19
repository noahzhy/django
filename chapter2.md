# 创建项目
```shell
django-admin startproject mysite
```
**`mysite`**是你的项目名。

## 项目结构
```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

这些目录和文件的用处是： 

* 最外层的 **`mysite/ `** 根目录只是你项目的容器，你可以将它重命名为任何你喜欢的名字。
* **`manage.py`**: 一个让你用各种方式管理 Django 项目的命令行工具。
* 里面一层的 **`mysite/`** 目录包含你的项目，它是一个纯 Python 包。它的名字就是当你引用它内部任何东西时需要用到的 Python 包名。 (比如 mysite.urls).
* **`mysite/__init__.py`**：一个空文件，告诉 Python 这个目录应该被认为是一个 Python 包。
* **`mysite/settings.py`**：Django 项目的配置文件。
* **`mysite/urls.py`**：Django 项目的 **URL** 声明，就像你网站的“目录”。
* **`mysite/wsgi.py`**：作为你的项目的运行在 WSGI 兼容的Web服务器上的入口。

## 简易服务器
```shell
python manage.py runserver
```

你应该会看到如下输出：

```
Performing system checks...

System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.

一月 11, 2019 - 15:50:53
Django version 2.1, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

刚刚启动的是 Django 自带的用于开发的简易服务器，它是一个用纯 Python 写的轻量级的 Web 服务器。**千万不要**将这个服务器用于和生产环境相关的任何地方。这个服务器只是为了开发而设计的。

浏览器访问 ``https://127.0.0.1:8000/``你将会看到一个“祝贺”页面，服务器已经运行了。