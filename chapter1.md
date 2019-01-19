# 安装 Django
首先你需要安装 Python，推荐 Python3，具体方法自行 Google。
第二步，安装 pip3 以及 Django。
```shell
sudo apt-get install python3-pip
sudo pip3 install django
```


### 验证
```py
import django
print(django.get_version())
2.1.5
```