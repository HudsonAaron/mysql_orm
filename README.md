##**`mysql orm`操作库 `erlang`版本**
### 前言
这个工具，意在希望降低mysql开发难度

###（1）版本新增内容
+ `2023-08-07`
  + (a) `auto_increment`，支持自增ID
+ `2023-08-02`
  + (a) `json`，支持json数据格式
  + (b) 支持tinyint、smallint、int、bigint默认宽度
+ `2023-07-31`
    - (a) `add primary key`，支持添加主键索引
    - (b) `add unique index`，支持添加唯一索引
    - (c) `add index`，支持添加普通索引
    - (d) `drop primary key`，支持删除主键索引
    - (e) `drop index`，支持删除唯一索引、普通索引
+ `2023-07-27`
    - (a) `select`，支持子查询，不支持联表查询等复合查询，需要mysql开源库的支持
    - (a) `alter`，支持自动识别字段，存在则修改字段，不存在则添加字段
+ `2023-05-26`
    - (a) `select`，目前不支持子查询，联表查询等复合查询
    - (b) `delete`
    - (c) `update`
    - (d) `truncate`
    - (e) `insert`
    - (f) `replace`
    - (g) `drop`
    - (h) `alter`，目前不支持添加字段和修改字段时修改字段键值类型