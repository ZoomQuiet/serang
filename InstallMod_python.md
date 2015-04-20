ModPython

## install mod\_python ##
```
checking for Py_NewInterpreter in -lpython2.5... no
configure: error: Can not link to python
```
由于我的python是从deb安装的，缺少src
安装python-dev后，解决

## 运行 ##

```
一个处理器就是初始处理某个阶段的函数。同一个阶段可以有多于一个处理器进行处理，被叫做apache序列。
对应每个阶段有个缺省的apache处理器(大多数只做缺省动作或者什么都不作)。然后由其他的apache模块提供处理器，比如mod_python。

mod_python提供了apache每一个重要的处理器。mod_python处理器缺省时不会做任何事情，除非用特定的配置文件标志。
这些标志以"Python"开始并以"Handler"结尾(如：PythonAuthenHandler)，指定Python函数来处理指定的阶段。
所以mod_python的主函数只是作为发报机的角色连接apache处理器和Python函数。

最常用的处理器是PythonHandler。它处理含有上下文的请求。因为它没有名字，所以有时也成为通用处理器。
这个处理器的apache缺省行为是读取文件并发送到客户端。大多数应用应该重写这个处理器。
参考自官方文档的翻译:http://www.upsdn.net/html/2006-08/693.html
看来需要找/写一个handler
```

**vhost配置**
```
<VirtualHost *:80>
    PythonPath "['/home/serang/apps'] + sys.path"
    AddHandler mod_python .py
    PythonHandler test
    PythonDebug On
</VirtualHost>
```

**增加对django的支持**
参考：

http://www.cnblogs.com/zhengyun_ustc/archive/2006/11/20/django_apache_win32.html

http://hideto.javaeye.com/blog/42538
```
<VirtualHost *:80>

    <Location "/">
        SetHandler python-program
        PythonPath "['/home/zhaofw/workspace/serang']+ sys.path"
        PythonHandler django.core.handlers.modpython
        SetEnv DJANGO_SETTINGS_MODULE apps.settings_apache
        PythonAutoReload On
        PythonDebug On
    </Location>
    Alias /site_media /home/zhaofw/workspace/serang/apps/media
    Alias /media /usr/lib/python2.5/site-packages/django/contrib/admin/media
    <Location "/site_media">
        SetHandler None
    </Location>
    <Location "/media">
        SetHandler None
    </Location>

    #PythonPath "['/home/zhaofw/workspace/serang/apps'] + sys.path"
    #AddHandler mod_python .py
    #PythonHandler mptest
    #PythonDebug On
</VirtualHost>
参考 ： http://www.woodpecker.org.cn/obp/django/django-stepbystep/newtest/doc/tut12.html#id15
```
但这种方式，未必适合这里的需求，先配来看看。

出现了这个错误：
ImproperlyConfigured: Error importing middleware django.contrib.sessions.middleware: "No module named wiki"

错误原因找到了，和上面的配置没关系。
我希望在apps下放所有的应用，这些应用共享settings的配置，对于AE来说，这是正常的，不需要应用去配置数据库，模板应该在应用内部，可能在某个地方写错了，再找找。