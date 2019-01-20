# 静态与动态文件
通常我们需要提供用户在线上传和下载的功能，并且我们在开发网页时，不可避免的要用到js，css这类的文件，所以没我们需要设置静态文件路径。

## 设置静态文件与动态文件路径
编辑 **`mysite`** 文件夹里的 **`settings.py`**
```py
# 静态文件的路径
STATIC_URL = '/static/'
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'), # app共有的静态文件，比如：jqurey.js
    '', # 其他静态文件的路径
)

# 动态文件的路径
MEDIA_URL = '/uploads/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'uploads')
```

## 配置路由
**`urls.py`** 中配置路由
```py
from django.contrib import admin
from django.urls import include, path
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
	path('', include('index.urls')),
    path('admin/', admin.site.urls),

] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)


```

## 动态文件设置
**`MEDIA_ROOT`** 和 **`MEDIA_URL`** 代表的是用户上传后的文件保存的地方。可以理解为存放可变文件的文件夹。

在 Django 的 **FileField** 和 **ImageField** 这样的 Model 类中，有 **`upload_to`** 参数可选。当 **`upload_to`** 设置相关的地址后，例如：

```py
models.ImageField(upload_to = 'test_pictures') 
```

文件上传后将自动保存到： **`os.path.join(MEDIA_ROOT, upload_to)`**，在本例中就是：**`/uploads/test_pictures`**
而 **`MEDIA_URL`**，则代表用户可以通过怎样的 URL 来访问这些上传后的文件资源。

在本例子中，本机地址是：**`http://127.0.0.1/`**，**`MEDIA_URL`** 设置为 **`/uploads/`**
那么通过：**`http://127.0.0.1:8000/uploads/文件名`** 就可以访问相关的上传图片或者其他文件。

## 静态文件设置
**`STATIC_ROOT`** 和 **`STATIC_URL`** 用于网站放置的**静态图片、CSS、JS** 等文件的地址。

**`STATIC_URL`**，同 **`MEDIA_URL`** 类似；设置 **`STATIC_URL`** 为 **`/static/`** 后，通过：**`http://127.0.0.1:8000/static/文件名`** 就可以访问相应的静态文件了。

>**`STATIC_ROOT`** 是一个比较特殊的文件夹。
>这是 Django 的开发模式和部署模式区别最大的地方。

通常我们在开发模式下，可以在我们所在的 **project** 下建立相应的 app， 然后每个 app 下都建立相应的 static 文件夹。

在开发模式下（**`Debug=True`**），Django 将为我们自动查找这些静态文件（每个app）并在网页上显示出来。然而，在部署模式下，Django 认为这些工作交由 web 服务器来运行会更有效率。

因此，在部署时，我们需要运行 ：
```shell
python manage.py collectstatic
```
这个命令将会把每个 app 里的 **`static`** 目录下的文件复制到 **`STATIC_ROOT`** 这个文件夹下。

如果在部署模式下（**`Debug=False`**） 访问相关网页，如：**`http://127.0.0.1:8000/static/文件名`**，将不会访问 Django下各个 App 中的 **static** 文件夹，而是 **`STATIC_ROOT`** 中所指定的文件夹。

为了在部署模式下正确使用，我们还需要在 **`urls.py`** 中添加以下：

```py
from django.contrib import admin
from django.urls import include, path
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('', include('index.urls')),
    path('admin/', admin.site.urls),

] + static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```