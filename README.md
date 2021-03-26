# 创建项目包
```
1. django-admin startproject project
```
```
Django_course
    └── project 
           │── manage.py	
           └── project
                  │——settings.py
                  │——urls.py
                  │——wsgi.py
                  └──__init__.py

```
* manage.py 一个命令行工具，可以使你用多种方式对Django项目进行交互
* project/settings.py 配置文件
* project/urls.py 项目url声明
* project/wsgi.py WSGI兼容的Web服务器入口
# 创建激活应用
```
2. cd project && python manage.py startapp MyApp

3. 编辑project/setting.py,将MyApp应用加入到INSTALLED_APPS中
```
在Django_course/project下生成MyApp应用文件夹  
**project为一个项目，该项目的应用模板均在此文件夹下**
# 配置数据库
在project/__init__.py添加
```
import pymysql
pymysql.install_as_MySQLdb()
```
Django默认使用SQLite数据库，project/setting.py中通过DATABASES配置其他类型数据库(Mysql)
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '数据库名',
        'USER': '用户名',
        'PASSWORD': '密码',
        'HOST': '数据库服务器ip,本机127.0.0.1',
        'POST': '端口',
    }
}
```
# [定义模型(数据表)](materials/模型.html)
在MyApp/models.py中定义模型类，一个模型类在数据库中对应一张数据表  
模型类继承models.Model类  
不需要定义主键，主键会自动添加，值为自动增长
```
4. python manage.py makemigrations

在MyApp/migrations生成一个迁移文件

5. python manage.py migrate

生成数据库中的表
```
# [定义视图](materials/视图.html)
在django中，视图对WEB请求进行回应  
视图接收request对象作为第一个参数，包含请求的信息  
视图就是一个Python函数，定义在MyApp/views.py
修改project/urls.py
```python
from django.contrib import admin
from django.conf.urls import url,include

urlpatterns = [
    url('admin/', admin.site.urls),
    url(r'^',include('MyApp.urls')),
]
```
**在MyApp中创建新的urls.py文件,在此文件中添加视图函数与模板的连接**
# [定义模板](materials/模板.html)
模板是html页面，可以通过传递参数与视图函数进行交互  
创建templates文件夹用来存放项目的模板文件  
在project/setting.py文件中设置TEMPLATES的路径  
**通过MyApp中新的urls.py文件,连接模板与视图**
# 启动服务器
```
6. python manage.py runserver 
```
# 站点管理
```
7. python manage.py creatersuperuser
```
按提示数据用户名、邮箱、密码  
通过URL<127.0.0.1:8000/admin/>登陆  
如下设置project/setting.py字段，修改中文及时间
```python
# LANGUAGE_CODE = 'en-us'
LANGUAGE_CODE = 'zh-Hans'

# TIME_ZONE = 'UTC'
TIME_ZONE = 'Asia/Shanghai'
```
# [Django扩展](material/Django高级扩展.html)