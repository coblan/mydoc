基本架构
=====================

页面分类
---------
管理后台主要由前端页面、数据处理层、model映射数据库三个部分组成。按照前后端以及中间过程的数据类型分析，
可以分类为

1. 包含多行的table型数据。
2. 包含一行的form型数据。

所以，管理后台页面可以分为包含table型数据的table页，包含一行数据的form页。

数据注入
------------
利用jsonify自定义的标签，在django.template.context中将数据一次性注入前端页面。所以，在前端页面的源代码
script部分，可以看到所有由后端注入的数据。
::

    {% load jsonify %}

    tabs={{ tabs | jsonify | default:'[]' }}

前后端交互
-------------
传统交互方式是利用url型api来进行交互，但是这样过于麻烦，除非是前后端分离式的开发，否则没有必要。
在director中，采用了两种前后端的交互方式。

ajax.py
    将函数写在 ``ajax.py`` 文件中，通过 ``get_global`` 函数暴露给 ``director.views.ajax_view`` 接口函数，前端通过请求
    接口，直接调用 ``app.ajax.py`` 的对应函数
::
    
    # 后端代码
    def fun1():
        pass
    
    def get_global():
        return gloabals()

    //前端代码
    ex.post('/d/ajax/{app_name}' post_data=[{fun:xxx,arg1:xx,arg2:xxx}]


director
    通过一个全局的 ``director`` 字典，对函数进行命名注册。在js端，可以利用注册名直接调用函数。
    该字典定位在 ``director.base_data.director`` ，请求的路由是通过 ``director.ajax.py`` 
    的 ``director_view`` 。
::

    # 通过装饰器
    @director_view('test.myfun1')
    def myfun(arg1):
        pass
    # 或者直接用字典注册
    director.update({'test.myfun1':myfun})

    //前端调用方式为
    ex.director('test.myfun1',{arg1:xxx},function(resp){})


