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

## 动态文件设置
**`MEDIA_ROOT`** 和 **`MEDIA_URL`** 代表的是用户上传后的文件保存的地方。可以理解为存放可变文件的文件夹。

在 Django 的 **FileField** 和 **ImageField** 这样的 Model 类中，有 **`upload_to`** 参数可选。当 **`upload_to`** 设置相关的地址后，例如：

```py
models.ImageField(upload_to = 'test_pictures') 
```

文件上传后将自动保存到： **`os.path.join(MEDIA_ROOT, upload_to)`**，在本例中就是：**`/uploads/test_pictures`**
而 **`MEDIA_URL`**，则代表用户可以通过怎样的 URL 来访问这些上传后的文件资源。

在本例子中，本机地址是：**`http://127.0.0.1/`**，**`MEDIA_URL`** 设置为 **`/uploads/`**
那么通过：**`http://127.0.0.1/uploads/文件名`** 就可以访问相关的上传图片或者其他文件。

