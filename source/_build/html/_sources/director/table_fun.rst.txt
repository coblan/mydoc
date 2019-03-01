table函数
==============
table函数用在table页面，被按钮触发。例如创建，删除。

创建，删除
--------------
如果director中包含了${table_name}.edit的modelfields,那么会自动生成创建于删除的button
::

    director.update({
        'my-table.edit':xxxForm
    })

selected_set_and_save
------------------------
设置选中项。前端函数位于jb_admin/js/node_store/table_store.js。在python端配置如下。
::

    {'fun': 'selected_set_and_save', 'editor': 'com-op-btn' ,
    'pre_set': 'rt={isrecommend:1}',
    'after_save': 'rt=scope.ts.search()','row_match':'one_row',
    'match_express':'scope.row.AccountType == 1','match_msg':'只有代理用户才能修改佣金比例',
    'label': '修改佣金比例','fields_ctx': yong.get_head_context(),
    'after_error':'scope.fs.showErrors(scope.errors)',
    }, 

pre_set:用于设置预先定义的字段。
row_match:可以选择 'one_row','many_row'。
fields_ctx：可以由modelfields.get_head_context()直接生成。 或者::

    'fields_ctx': {
                    'heads': [{'name': 'memo', 'label': '备注', 'editor': 'blocktext', }],
                    'ops': [{'fun': 'save', 'label': '确定', 'editor': 'com-op-btn', }],
                }

after_error:错误处理  // ex.eval(kws.after_error,{fs:field_store,errors:resp.save_rows.errors})

pop_panel
----------------------------
弹出一个自定义的窗口

arraySpanMethod
-------------------
控制table布局



