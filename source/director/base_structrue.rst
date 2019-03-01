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

前后端交互
-------------
传统交互方式是利用url型api来进行交互，但是这样过于麻烦，除非是前后端分离式的开发，否则没有必要。
在director中，采用了两种前后端的交互方式。

ajax.py
    将函数写在ajax.py文件中，通过get_global函数暴露给director.views.ajax_view接口函数，前端通过请求
    '/d/ajax/{app_name}' post_data=[{fun:xxx}] 接口，直接调用app.ajax.py的对应函数

director
    在python文件的任意地方，对函数进行命名，该命令指定为director.base_data.director,
    通过director.ajax.py的director_view进行路由，直接调用。
    前端调用方式为ex.director({director_name},post_data,function(resp){})

