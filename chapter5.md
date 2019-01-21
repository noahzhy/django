# 创建模型
>在 Django 中，我们用模型来称呼数据库，模型是你的数据唯一而且准确的信息来源。一般来说，每一个模型都映射一个数据库表。

## 快速上手
```py
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
```
上面的 Person 模型会创建一个如下的数据库表：

```sql
CREATE TABLE myapp_person (
    "id" serial NOT NULL PRIMARY KEY,
    "first_name" varchar(30) NOT NULL,
    "last_name" varchar(30) NOT NULL
);
```

需要注意的是：一个 id 字段会被自动添加，但是这种行为可以被改写。

## 使用模型
一旦你定义了你的模型，你需要告诉 Django 你准备使用这些模型。你需要修改 **`settings.py`** 文件中的 **`INSTALLED_APPS`** ，在这个设置中添加包含你 **`models.py`** 文件的模块的名字。
```py
INSTALLED_APPS = [
    #...
    'myapp',
    #...
]

```
