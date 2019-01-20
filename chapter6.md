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

