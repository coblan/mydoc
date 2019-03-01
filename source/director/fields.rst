fields
============
与form是相同的意思。为了避免与form产生冲突，所以更名为fields。包括 ``modelfields,fields`` 两个类。
modelfields直接用于model的编辑处理，而fields用于自定义的表单处理。

构建modelfields样例
---------------
::

    class TestFiels(modelfields):
        class Meta :
            model=model1
            exclude=[]

    director.update({'model_form':TestFiels}) 

构建fields
---------------
::

    class TestFields(fields):
        def get_heads():
            pass
        
        def get_row():
            pass
    
    director.update({'model_form':TestFiels}) 