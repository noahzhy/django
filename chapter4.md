# 编写视图
开始编写第一个视图吧。打开 **`myapp/views.py`**，把下面这些 Python 代码输入进去：
```py
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the myapp index.")
```
如果想看见效果，我们需要将一个 URL 映射到它——这就是我们需要 URLconf 的原因了。

为了创建 URLconf，请在 **`myapp`** 目录里新建一个 **`urls.py`** 文件。

在 **`myapp/urls.py`** 中，输入如下代码：

```py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```
下一步是要在根 **URLconf** 文件中指定我们创建的 **`myapp.urls`** 模块。在 **`mysite/urls.py`** 文件的 **urlpatterns** 列表里插入一个 **include()**， 如下：

```py
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('myapp/', include('myapp.urls')),
    path('admin/', admin.site.urls),
]
```

你现在把 **index** 视图添加进了 **URLconf**。可以验证是否正常工作，运行下面的命令:

```shell
python manage.py runserver
```

用浏览器访问 **`http://localhost:8000/myapp/`**，你应该能够看见 **Hello, world. You're at the myapp index.** ，这是你在 **index** 视图中定义的。

## 首页

通过上面的例子，我们不难发现 **`urlpatterns`** 负责将 URL 映射到我们需要的位置。

我们继续新建一个名为 index 的应用，方便我们管理 index 页。

```shell
python manage.py startapp index
```

同上面的步骤，我们给这个 index 编写视图，并且将 URL 映射到 index 上。

打开 **`index/views.py`**，把下面这些 Python 代码输入进去：
```py
from django.http import HttpResponse

def index(request):
    html = '''<html><body><img style="width:256px;" src="https://lision.me/ios_native_js/html5.png"  alt="ex" /><text>Hello World!</text></body></html>'''
    return HttpResponse(html)
```


