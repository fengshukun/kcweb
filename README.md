#  框架简要说明

<div style="border-box;border-left:7px solid #5BC0DE;background:#F4F8FA;padding-left:10px;color:#5bc0de;">
	<ul><h2>一个集成web应用的开发框架</h2>kcw 快速创建cli和web框架
	

</div>
<div style="border-box;border-left:7px solid #5BC0DE;background:#F4F8FA;padding-left:10px;color:#5bc0de;">
	<ul><h2>主要特性</h2><li style="color:#000">mysql对象化</li><li style="color:#000">mongodb对象化</li><li style="color:#000">助手函数</li><li style="color:#000">配置支持</li><li style="color:#000">独立路由配置 (默认 按文件名/方法名)</li><li style="color:#000">数据库助手</li><li style="color:#000">配置优先级</li><li style="color:#000">命令行快速创建web应用</li><li style="color:#000">命令行创建cli应用</li><li style="color:#000">分布式数据库支持</li><li style="color:#000">mysql事务支持</li><li style="color:#000">链试操作</li><li style="color:#000">lock锁</li><li style="color:#000">web应用修改时时同步</li><li style="color:#000">kcw命令行</li>
	</ul>
</div>


#### kcw的环境要求如下：

<div style="border-box;border-left:7px solid #5BC0DE;background:#F4F8FA;padding-left:10px;color:#5bc0de;font-size:16px">
	python3或更高
	<div style="height:2px;"></div>
</div>

#### 安装
<div style="border-box;border-left:7px solid #5BC0DE;background:#F4F8FA;padding-left:10px;color:#5bc0de;font-size:16px">
	pip install kcweb -i http://mirrors.aliyun.com/pypi/simple/
	<div style="height:2px;"></div>
</div>

### 创建应用
create.py 文件说明
<div style="border-box;border-left:7px solid #5BC0DE;background:#F4F8FA;padding-left:10px;color:#5bc0de;">
	新建一个app.py文件,内容如下，执行python3 app.py创建应用
	如下面的代码创建了一个app应用，同时在app应用下创建了一个api模块
	<div style="height:2px;"></div>
</div>

```app.py
from kcweb.create import create
create("app","api")  # 创建项目
```

<h3>执行完上述文件后，您的目录结构应该是这样，如下：</h3>

```
├─./                               框架目录
├─app                              公共方法目录
│  ├─common                        公共函数目录
│  │  ├─__init__.py                函数文件
│  ├─config                        配置目录
│  │  ├─__init__.py                配置文件
│  ├─api                           模块目录
│  │  ├─common                     该模块的公共函数目录
│  │  │  ├─__init__.py             函数文件
│  │  ├─controller                 控制器目录
│  │  │  ├─__init__.py             版本初始化文件
│  │  │  ├─v1
│  │  │  │  ├─__init__.py          函数初始化文件
│  │  │  │  ├─index.py             控制器文件
│  │  │  ├─v2
│  │  │  │  ├─__init__.py          函数初始化文件
│  │  │  │  ├─index.py             控制器文件
│  │  ├─tpl                        模板文件目录
│  │  │  ├─v1
│  │  │  │  ├─index
│  │  │  │  │  ├─index.html        模块文件
│  │  │  ├─v1
│  │  │  │  ├─index
│  │  │  │  │  ├─index.html        模块文件
│  │  ├─__init__.py                控制器初始化文件
│  ├─script                        命令行脚本
│  │  ├─common                     该模块的公共函数目录
│  │  │  ├─__init__.py             函数文件
│  │  │  ├─win.py                  类文件
│  │  ├─test.py                    脚本文件
│  ├─static                        静态资源目录
│  ├─runtime                       缓存目录
│  ├─__init__.py                   自动导入模块文件
├─create.py                
├─app.py            应用创建后生成的运行文件（应用创建时自动创建）
```

<p>执行完上述文件在当前目录下执行python3 app.py。 通过访问127.0.0.1:39001</p>


<div style="border-box;border-left:7px solid #5BC0DE;background:#F4F8FA;padding-left:10px;color:#5bc0de;">
	<ul>
	<h2>
	配置
	</h2>
	配置以变量定义、字典赋值，所有的配置变量都是一个字典
	
	<li style="color:#000">核心配置：核心框架内置的配置文件，无需更改</li><li style="color:#000">公共配置：每个应用的全局配置文件</li><li style="color:#000">动态配置：主要是在视图中进行（动态）更改配置，该配置方式只在当前模块和当次请求有效，因为不会保存到配置文件中</li><li style="color:#000">方法配置：主要是通过特定的方法传入配置信息</li>
	</ul>
</div>
<div>
<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;">注意：redis连接池链接模式下不支持动态配置，动态配置不生效，如果您的项目需要redis动态配置，那么您需要在模块配置中设置redis连接方式为False。如：redis['pattern']=False</div>
</div>
<div>
<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;"><h3>配置优先级：</h3></div><div style="padding-left:20px">核心配置 < 公共配置 < 动态配置 < 方法配置</div>
</div>


<div>
<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;"><h3>自定义配置：</h3></div><div style="padding-left:20px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;自定义配置就是需要在应用下使用自己的配置，如：调用某平台的接口需要使用的appid和appkey需要单独配置时所使用的配置</div>
</div>
<div>

<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;"><h3>配置文件：</h3>完整配置如下：</div>

```
# 应用配置
app['app_debug']=True  #是否开启调试模式
app['tpl_folder']='./tpl'  #设置模板文件目录名 注意：不能配置目录路径
app['before_request']='before_request'  #设置请求前执行的函数
app['after_request']='after_request'    #设置请求后执行的函数  
app['staticpath']='app/static'
# redis配置
redis['host']='127.0.0.1' #服务器地址
redis['port']=6379 #端口
redis['password']=''  #密码
redis['db']=0 #Redis数据库    注：Redis用0或1或2等表示
redis['pattern']=True # True连接池链接 False非连接池链接
redis['ex']=0  #过期时间 （秒）

#缓存配置
cache['type']='File' #驱动方式 支持 File Redis
cache['path']='runtime/cachepath' #缓存保存目录 
cache['expire']=120 #缓存有效期 0表示永久缓存
cache['host']=redis['host'] #Redis服务器地址
cache['port']=redis['port'] #Redis 端口
cache['password']=redis['password'] #Redis登录密码
cache['db']=1 #Redis数据库    注：Redis用1或2或3等表示

# session配置
session['type']='File' #session 存储类型  支持 file、Redis
session['path']='runtime/session' #session缓存目录
session['expire']=86400 #session默认有效期 该时间是指session在服务的保留时间，通常情况下浏览器上会保留该值的10倍
session['prefix']="KCW" # SESSION 前缀
session['host']=redis['host'] #Redis服务器地址
session['port']=redis['port'] #Redis 端口
session['password']=redis['password'] #Redis登录密码
session['db']=2 #Redis数据库    注：Redis用1或2或3等表示


# 默认数据库配置
database['type']='mysql' # 数据库类型  目前支持mysql和sqlite
database['host']=['127.0.0.1']#服务器地址 [地址1,地址2,地址3...] 多个地址分布式(主从服务器)下有效
database['port']=[3306] #端口 [端口1,端口2,端口3...]
database['user']=['root']  #用户名 [用户名1,用户名2,用户名3...]
database['password']=['root']  #密码 [密码1,密码2,密码3...]
database['db']=['test']  #数据库名 [数据库名1,数据库名2,数据库名3...]
database['charset']='utf8'   #数据库编码默认采用utf8
database['pattern']=False # True数据库长连接模式 False数据库短连接模式  注：建议web应用使用短连接，cli应用使用长连接
database['cli']=False # 是否以cli方式运行
database['dbObjcount']=1 # 连接池数量（单个数据库地址链接数量），数据库链接实例数量 mysql长链接模式下有效
database['deploy']=0 # 数据库部署方式:0 集中式(单一服务器),1 分布式(主从服务器)  mysql数据库有效
database['master_num']=1 #主服务器数量 不能超过host服务器数量  （等于服务器数量表示读写不分离：主主复制。  小于服务器表示读写分离：主从复制。） mysql数据库有效
database['master_dql']=False #主服务器是否可以执行dql语句 是否可以执行select语句  主服务器数量大于等于host服务器数量时必须设置True
database['break']=0 #断线重连次数，0表示不重连。 注：cli模式下 10秒进行一次重连并且连接次数是当前配置的300倍

#sqlite配置
sqlite['db']='kcwdb'  # 数据库文件存放地址

#mongodb配置
mongo['host']='127.0.0.1'
mongo['port']='27017'
mongo['user']=''
mongo['password']=''
mongo['db']='test'



#路由配置 
route['default']=True #是否开启默认路由  默认路由开启后面不影响以下配置的路由，模块名/版本名/控制器文件名/方法名 作为路由地址   如：http://www.kcw.com/api/v1/index/index/
route['modular']=[{"www":"api"},{"127":"api"},{"192":"api"}] #配置域名模块 配置后地址为：http://www.kcw.com/v1/index/index/  注意:如果使用的是代理服务器需要把代理名称设置为当前配置的域名，否则不生效
route['edition']='' #默认路由版本，配置后地址为 http://www.kcw.com/index/index/
route['files']='index' #默认路由文件 
route['funct']='index'  #默认路由函数
route['methods']=['POST','GET'] #默认请求方式
#email配置
email['sender']='' #发件人邮箱账号
email['pwd']='' #发件人邮箱密码(如申请的smtp给的口令)
email['sendNick']='' #发件人昵称
email['sendNick']='' #发件人昵称
email['theme']='' #默认主题
email['recNick']='' #默认收件人昵称
#其他配置 如：
other['aliyun']['AccessKey_ID']=''  #配置阿里云账户id
other['aliyun']['AccessKey_Key']='' #配置阿里云账户key
```

<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;"><h3>方法配置：</h3>下面是使用mysql的方法配置数据库信息</div>

```
mysql('test').connect({"host":"127.0.0.1"}).find()
```

<div>
<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;"><h3>动态配置：</h3></div><div style="padding-left:20px">动态修改配置信息，如动态修改数据库链接ip、端口和重连次数
</div>
</div>
<div>

```
config.database['host']=['127.0.0.1'] #服务器地址
config.database['port']=[3306] #端口
config.database['break']=1 #断线重连次数
```

动态配置不建议在web应用中使用，因为他是全局的，通常情况下，如果您的web应用需要部分接口需要修改配置信息应该使用方法配置，cli脚本可以使用动态配置




<div>
<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;"><h3>使用配置：</h3></div><div style="padding-left:20px">获取配置信息
</div>
</div>
<div>

```
print(config.app)  #获取app配置信息
print(config.database['host'])  #获取数据库配置信息
print(config.other['aliyun'])  #获取aliyun配置信息
...
```

## 运行文件
<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;color:#d9534f;">app.py是web应用的运行文件，你您只需要用python执行app.py即可运行web应用,app.py文件是您创建应用时生成的<div style="height:2px"></div></div>

app.py内容如下：

```
# #gunicorn -b 0.0.0.0:39010 app:app
from kcweb import web
import app as application
app=web(__name__,application)
if __name__ == "__main__":
    #app 是当前文件名  host监听ip port端口
    app.run("app",host="0.0.0.0",port="39001")
```

您可以根据上面的备注修改相关的信息

## URL设计
<div style="border-box;border-left:7px solid #5BC0DE;padding-left:10px;color:#5bc0de;">
kcweb在没有定义路由的情况下典型的URL访问规则是：</div>

```
http://serverName/模块/版本/控制器/函数/[参数名/参数值...]
```

<div style="border-box;border-left:7px solid #5BC0DE;padding-left:10px;color:#5bc0de;">
kcweb在创建应用时默认配置了基本路由</div>

```
route['default']=True #是否开启默认路由  默认路由开启后面不影响以下配置的路由，模块名/版本名/控制器文件名/方法名 作为路由地址   如：http://www.kcw.com/api/v1/index/index/
route['modular']=[{"www":"api"},{"127":"api"},{"192":"api"}] #配置域名模块 配置后地址为：http://www.kcw.com/v1/index/index/  注意:如果使用的是代理服务器需要把代理名称设置为当前配置的域名，否则不生效
route['edition']='v1' #默认路由版本，配置后地址为 http://www.kcw.com/index/index/
route['files']='index' #默认路由文件 
route['funct']='index'  #默认路由函数
route['methods']=['POST','GET'] #默认请求方式
```

<p style="border-box;border-left:7px solid #5BC0DE;padding-left:10px;color:#5bc0de;">
所以您的URL访问规则是：</p>

```
http://serverName/控制器/函数/[参数名/参数值...]
```

## 方法



<div>
<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;"><h3>公共方法：</h3></div><div style="padding-left:20px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果您定义的方法需要被当前应用的所有模块模块使用，那么你应该把您的的方法定义在公共方法文件中，所有方法名应该以下划线方式命名，并且不能出现框架提供的方法名，下面定义的方法可以在其他模块下使用</div>
</div>
<div>

```
├─./					
├─app				应用目录
│  ├─common		公共方法目录
│  │  ├─__init__.py		公共方法文件
from kcweb.common import *
from app import config
def returnjson(data=[],code=0,msg="成功",status='200 ok'):
    """在浏览器输出包装过的json

        参数 data 结果 默认[]

        参数 code body状态码 默认0

        参数 msg body状态描述 默认 成功

        参数 status http状态码 默认 200

        返回 json字符串结果集 
        """
    res={
        "code":code,
        "msg":msg,
        "time":times(),
        "data":data
    }
    return json_encode(res),status,{"Content-Type":"application/json; charset=utf-8"}
```

<div>
<div style="border-box;border-left:7px solid #D9534F;padding-left:10px;"><h3>模块方法：</h3></div><div style="padding-left:20px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;如果您定义的方法只是为某个模块使用，那么你应该把您的的方法定义在模块方法文件中，所有方法名应该以下划线方式命名，并且不能出现框架提供的方法名和公共方法里定义的方法名，下面定义的方法可以在当前模块下使用</div>
</div>
<div>

```
├─./							
├─app					   应用目录
│  ├─api						模块目录(简称模块)
│  │  ├─common				  当前模块方法目录
│  │  │  ├─__init__.py		  当前模块方法文件

from app1.common import *
#下面的方法在当前模块中有效
G=globals.G
#下面的方法在当前模块中有效
def before_request():
    G.userinfo=get_session("userinfo")
    print('api模块在请求前执行，我是要在配置文件配置后才能生效哦！',G.userinfo)
def after_request():
    print('api模块在请求后执行，我是要在配置文件配置后才能生效哦！')
def set_session(name,value,expire=None):
    "设置session"
    return session.set("app1api"+str(name),value,expire)
def get_session(name):
    "获取session"
    return session.get("app1api"+str(name))
def del_session(name):
    "删除session"
    return session.rm("app1api"+str(name))
def tpl(path,**context):
    return Template("/api/tpl"+str(path),**context)

```





## 控制器定义
控制器文件通常放在[应用]/[模块]/controller/[版本]目录下面，文件名统一保持小写。一个视图文件格式应该是如下：returnjson方法的作用是在浏览器输出包装过的json，当然你也可以修改该方法的值

```index.py
from [应用].[模块].common import *
def index1():
    return returnjson("index")
def index2():
    return returnjson("index")
...
```

访问的url是（在没有定义路由的情况下）
<div style="border-box;border-left:7px solid #CCC;padding-left:10px;;">http://server/[模块]/[版本]index/index1
http://server/[模块]/[版本]index/index2<div style="height:2px"></div></div>
##视图初始文件
______init__.py

```index.py
from . import index
# def error(err,data):
#     "该函数在当前目录下无法匹配时被调用"
#     return data,"200",{"Content-Type":"text/json; charset=utf-8"}
```

创建控制器文件后，您需要在当前版本目录下的______init__.py文件中导入控制器文件，______init__.py文件也可以定义函数，但他不能调用common下的方法

更多文档参考 ：http://212.129.149.238:9501/index/index/doc/docde/1
