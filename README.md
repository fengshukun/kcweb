完整文档请参考：http://intapp.kwebapp.cn/index/index/doc/docde/1
#### 创建应用
- 新建一个server.py文件,内容如下，执行python3 server.py创建应用
- 如下面的代码创建了一个app应用，同时在app应用下创建了一个api模块
```server.py
from kcweb.create import create
create("app","api")  # 创建项目
```

- 您的目录结构应该是这样，如下：
```
├─./							   框架目录
├─app							  公共方法目录
│  ├─common						公共函数目录
│  │  ├─__init__.py				函数文件
│  ├─config						配置目录
│  │  ├─__init__.py				配置文件
│  ├─api   						模块目录
│  │  ├─common					 该模块的公共函数目录
│  │  │  ├─__init__.py			 函数文件
│  │  ├─controller				 控制器目录
│  │  │  ├─__init__.py			 版本初始化文件
│  │  │  ├─v1
│  │  │  │  ├─__init__.py		  函数初始化文件
│  │  │  │  ├─index.py		 	控制器文件
│  │  │  ├─v2
│  │  │  │  ├─__init__.py		  函数初始化文件
│  │  │  │  ├─index.py		 	控制器文件
│  │  ├─tpl						模板文件目录
│  │  │  ├─v1
│  │  │  │  ├─index
│  │  │  │  │  ├─index.html		模块文件
│  │  │  ├─v1
│  │  │  │  ├─index
│  │  │  │  │  ├─index.html		模块文件
│  │  ├─__init__.py   			 控制器初始化文件
│  ├─script						命令行脚本
│  │  ├─common					 该模块的公共函数目录
│  │  │  ├─__init__.py			 函数文件
│  │  │  ├─win.py				  类文件
│  │  ├─test.py   				 脚本文件
│  ├─static						静态资源目录
│  ├─runtime   					缓存目录
│  ├─__init__.py   				自动导入模块文件
├─server.py			应用创建后生成的运行文件（应用创建时自动创建）
```
- 其中server.py文件内容将被修改如下
```
# #gunicorn -b 0.0.0.0:39001 server:app
from kcweb import web
import app as application
app=web(__name__,application)
if __name__ == "__main__":
    #app 是当前文件名  host监听ip port端口 name python解释器名字 (windows一般是python  linux一般是python3)
    app.run("server",host="0.0.0.0",port="39001",name="python")
```
- 如果您当前系统的python解释器名字是python3，你应该是在当前目录下执行python3 server.py。 然后访问127.0.0.1:39001


- 如果您当前系统的python解释器名字是python，您应该修改server.py代码如下
```
# #gunicorn -b 0.0.0.0:39001 server:app
from kcweb import web
import app as application
app=web(__name__,application)
if __name__ == "__main__":
    #app 是当前文件名  host监听ip port端口
    app.run("server",host="0.0.0.0",port="39001",name="python")
```
然后访问127.0.0.1:39001

