
# 页面

## login.vue

- 两个文本框用于输入用户名、密码
- “登录” 按钮，请求接口 login (post)，收到响应后
  - 若权限为 0，跳转到 manage.html
  - 若权限为 1，跳转到 reserve.html
- “注册” 按钮，跳转到 register.html



## register.vue

- 三个文本框，用于输入用户名、密码、确认密码
- “注册” 按钮，请求接口 register (post)，收到响应后
  - 注册成功，弹出提示框，跳转到 login.html
  - 注册失败，弹出提示框，显示失败原因



## manage.vue

- “管理自习室” 按钮，跳转到 manage-room.html
- “管理座位” 按钮，跳转到 manage-seat.html
- "注销" 按钮，跳转到 login.html



## manage-room.vue

- 默认请求接口 room(get) 获取第一页的自习室信息
- 每行末尾 “修改” 按钮，点击后隐藏 “修改” “删除” 按钮，显示 “确认” “取消” 按钮
  - “确认” 按钮，请求接口 room (put)，收到响应后
    - 删除成功，请求接口 room (get) 刷新页面
    - 删除失败，弹出提示框显示原因
  - “取消” 按钮，重置该行座位信息，隐藏 “确认” “取消” 按钮，显示 “修改” “删除” 按钮
- 每行末尾 “删除” 按钮，点击后弹出提醒框，确认是否删除，包含 “确认” “取消” 按钮
  - “确认” 按钮，请求接口 room (delete)，收到响应后
    - 删除成功，请求接口 room (get) 刷新页面
    - 删除失败，弹出提示框，显示原因
  - “取消” 按钮，关闭提醒框
- 下拉框 “自习室楼号” “自习室层号” “可用状态”，文本框 “自习室室号”
- “查询” 按钮，根据下拉框和文本框中的数据，请求符合条件的第一页座位信息
- 分页列表展示所有自习室信息
  - 页号按钮、前进按钮、后退按钮，请求接口 room (get)，获取对应页的自习室信息（要考虑最近一次查询的查询条件）
- 新增自习室窗口，包含 自习室编号 文本框，开放时间、结束时间 时间选择器，和 “新增” 按钮
  - “新增” 按钮，请求接口 room (post) ，收到响应后
    - 新增成功，请求接口 room (get) 刷新页面
    - 新增失败，弹出提示框，显示原因



## manage-seat.vue

- 默认请求接口 seat (get) 获取第一页的座位信息
- 每行末尾 “修改” 按钮，点击后隐藏 “修改” “删除” 按钮，显示 “确认” “取消” 按钮
  - “确认” 按钮，请求接口 seat (put)，收到响应后
    - 删除成功，请求接口 seat (get) 刷新页面
    - 删除失败，弹出提示框显示原因
  - “取消” 按钮，重置该行座位信息，隐藏 “确认” “取消” 按钮，显示 “修改” “删除” 按钮
- 每行末尾 “删除” 按钮，点击后弹出提醒框，确认是否删除，包含 “确认” “取消” 按钮
  - “确认” 按钮，请求接口 seat (delete)，收到响应后
    - 删除成功，请求接口 seat (get) 刷新页面
    - 删除失败，弹出提示框，显示原因
  - “取消” 按钮，关闭提醒框
- 下拉框 “自习室楼号” “自习室层号” “可用状态” “座位数” “是否能充电”，文本框 “自习室室号”
- “查询” 按钮，根据下拉框和文本框中的数据，请求符合条件的第一页座位信息
- 分页列表展示所有座位信息
  - 页号按钮、前进按钮、后退按钮，请求接口 seat (get)，获取对应页的座位信息（要考虑最近一次查询的查询条件）
- 新增座位窗口，包含 自习室编号、连坐数 两个文本框，可充电 勾选框，和 “新增” 按钮
  - “新增” 按钮，请求接口 seat (post) ，收到响应后
    - 新增成功，请求接口 seat (get) 刷新页面
    - 新增失败，弹出提示框，显示原因



## reserve.vue

- 默认请求接口 seat (get) 获取第一页的座位信息
- 每行末尾 “预约” 按钮（若座位不可用，则预约按钮变为灰色无法点击），点击后弹出提示框，包含 “预约时间段” 的时间选择器， “确认” “取消” 按钮
  - “确认” 按钮，请求接口 reserve (post)，收到响应后
    - 预约成功，弹出提示框，包含 “确认” 按钮，请求接口 seat (get) 刷新页面
    - 预约失败，弹出提示框，显示原因
  - “取消” 按钮，关闭提示框
- 下拉框 “自习室楼号” “自习室层号” “可用状态” “座位数” “是否能充电”，文本框 “自习室室号”
- “查询” 按钮，根据下拉框和文本框中的数据，请求符合条件的第一页座位信息
- 分页列表展示所有座位信息
  - 页号按钮、前进按钮、后退按钮，请求接口 seat (get)，获取对应页的座位信息（要考虑最近一次查询的查询条件）
- “历史记录” 按钮，跳转到 history.html



## history.vue

- 默认请求接口 record (get) 获取第一页的历史记录信息
- 分页列表展示所有座位信息
  - 页号按钮、前进按钮、后退按钮，请求接口 record (get)，获取对应页的历史记录信息



