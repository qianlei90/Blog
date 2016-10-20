Title: 《Flask Web开发》笔记
Date: 2016-05-06 15:50:20
Category: 技术
Tags: 笔记, Python
Slug: Flask_Web开发-基于Python的Web应用开发实战
Author: Lemon Tree

### 第一章 安装

虚拟坏境与pip安装，源码setup安装我是一次都没用过...

```shell
pyenv virtualenv 2.7 YourVirtualEnvName
pip install flask
```

### 第二章 程序的基本结构

先看最简单的代码:

```python
from flask inport Flask, render_template
# Flask对象实例化，每个实例都是一个独自的web server，如果是单个app一般使用__name__作为标识
# Flask中的初始化大致都是如此，第三方的扩展初始化时一般都会把app当做参数传进去
app = Flask(__name__)

# 路由，也有可能跟下面那个路由一样URL是带参数的，还可以指定参数类型
# '/user/<int: id>' 指定id为int
# '/user/<path: name>' 指定name为字符串
# '/user/<float: price>' 指定price为float
@app.route('/')
def index():
    # 返回值一般都是html字符串或者渲染后的模板
    # Flask默认的返回状态码是200，我们可以显示指定状态码为其他，如：
    # return 'bad request', 400
    return '<h1> Hello World!</h1>', 200

# 像这种被路由装饰器装饰过的方法叫做视图
# 是MVT（Model，View，Template）中的V部分，在视图中主要处理一些业务逻辑跟数据操作
# 而数据定义是在M层，页面展示在T层，这种分法很好的将项目工程分层
@app.route('/user/<name>')
def user(name):
    # 渲染模板并返回，name是传递给模板的参数
    return render_template('user.html', name=name)

# 直接运行这个文件就会启动Web Server，启动参数中设置了调试模式
# 默认启动本地5000端口
if __name__ == '__main__':
    app.run(debug=True)
```

说一下本章提到的两个比较基础又重要的概念。**上下文**和**URL映射与请求钩子**

+ **上下文**：

Flask的概念中共有两类上下文，程序上下文/请求上下文。顾名思义，程序上下文是指在当前app中可以全局使用，作用域在整个app范围，包括*current_app*与*g*两个变量，请求上下文是指在当前访问请求/会话中可以使用的变量，作用域只在当前请求/会话中，请求/会话结束后就会被撤销，包括*request*与*session*两个变量

|上下文|变量名|说明|
|:---|:---|:---|
|程序上下文|current_app|当前app的实例，就是上面代码中Flask类的实例|
|程序上下文|g|当前app全局可访问的变量，可以人为添加数据到g使这些数据在整个app可被访问，如数据库配置、最后登录的用户信息等|
|请求上下文|request|请求对象，封装了此次访问HTTP请求中的数据，包括请求头、Body之类的|
|请求上下文|session|会话，在多个请求中可共用的内容，比如存储了用户的cookies，当前用户的最近访问记录等|

+ **URL映射与请求钩子**

上面代码中有路由的概念，路由跟视图是一一对应的，这就是所谓的URL映射。而请求钩子的意思就是在当前的请求访问前后可能会执行的一些操作。比如有一个请求是获取数据，在调用这个视图前我们会先检查用户有没有权限去获取，检查权限的部分是请求钩子，如果过不了就无法进入到获取数据的视图中。请求钩子的装饰器有如下4种：

|钩子名|说明|
|:---|:---|
|before_first_request|第一个请求之前要做的操作，比如初始化数据库连接，初始化日志Handle等|
|before_request|在请求到来前要做的操作，比如权限检查、打印请求参数|
|after_request|请求正常结束之后要做的操作，比如记录相关日志|
|teardown_request|请求异常结束后要做的操作，比如发送警报邮件|

### 第三章 模板

Flask使用的是jinja2模板引擎，简单好用！具体的渲染方式如第二章的代码部分，使用render_template方法并传入相应参数。
注意在`{{ name }}`或`{% for page in pages %}`中两边的空格。

1. 变量

在html文件中插入`{{ name|capitalize }}`使用name变量，并对name使用过滤器capitalize使其首字母大写。更多的过滤器可以参考jinja2的官方文档。

2. 控制结构

\- 完(废弃) -
