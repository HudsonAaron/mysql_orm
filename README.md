# mysql_orm
+ **描述|desc**
</br>这个是erlang版本的mysql orm开源操作库，这里有些操作方式给你们。
</br>This is a library for mysql by erlang. Here are operation manual for you.
+ **erlang version**
</br>OPT25
+ ___当前版本库支持以下关键词|this library support so many keywords in current version___
</br>and, or, in, as, avg, sum, count, max, min, from_unixtime, like, primary, unique, index, unsigned, comment, after, tinyint, smallint, mediumint, int, bigint, char, varchar, tinytext, text, mediumtext, longtext and so on, and more keywords will coming soon.
+ **额外|extra**
</br>除此之外，你们还需要三个库，下面是url路径：
</br>In addition, you need three libraries, here you are the urls:
</br>***(1) mysql***
</br>https://github.com/mysql-otp/mysql-otp
</br>***(2) poolboy***
</br>https://github.com/devinus/poolboy
</br>***(2) mysql-poolboy***
</br>https://github.com/mysql-otp/mysql-otp-poolboy

+ **用例|cases**
</br>更多详细用例可以看 db_test.erl
</br>More use cases in db_test.erl
```erlang
-record(role, {
  id = 0,
  name = "",
  age = 0,
  score = 0
}).

Map = #{
    ?DB_TABLE_FIELDS => record_info(fields, aaa),
    ?DB_TABLE_NAME => aaa,
    ?DB_CREATE_KEYS => [
        #db_field{
            field_name = #aaa.id,
            data_type = ?DB_TINYINT(1),
            key = ?DB_KEY_PRI,
            default = 0,
            comment = "测试ID"
        },
        #db_field{
            field_name = #aaa.name,
            data_type = ?DB_VARCHAR(20),
            comment = "test name"
        }
    ],
    ?DB_COMMENT => "测试表格"
},
{ok, SQL} = db_util:create_string(Map),
Result = mysql_poolboy:query(mypool, SQL).

Map = #{
    ?DB_TABLE_FIELDS => [id, name, age, score],
    ?DB_TABLE_NAME => role,
    ?DB_SELECT_KEYS => [?DB_COUNT_ALL, ?DB_COUNT(id), name],
    ?DB_WHERE => [?DB_NE(id, 111), ?DB_AND, ?DB_NE(name, "测试")],
    ?DB_ORDER_BY => [?DB_ASC([id])],
    ?DB_LIMIT => 1
},
{ok, SQLFormat, WhereVals} = db_util:select_string(SelectMap),
Result = mysql_poolboy:query(mypool, SQL).

Map = #{
    ?DB_TABLE_FIELDS => record_info(fields, aaa),
    ?DB_TABLE_NAME => aaa,
    ?DB_REPLACE_KEYS => [#aaa.id, #aaa.name],
    ?DB_REPLACE_VALS => [4, "测试12", 5, "aaa"]
},
{ok, SQLFormat, Vals} = db_util:replace_string(Map),
Result = mysql_poolboy:query(mypool, SQLFormat, Vals).

Map = #{
    ?DB_TABLE_FIELDS => record_info(fields, aaa),
    ?DB_TABLE_NAME => aaa,
    ?DB_UPDATE_SETS => [{#aaa.name, "aadsada"}],
    ?DB_WHERE => [?DB_OR(?DB_EQ(#aaa.id, 2), ?DB_EQ(#aaa.id, 5)), ?DB_AND, ?DB_EQ(#aaa.name, "测试1")]
},
{ok, SQLFormat, Vals} = db_util:update_string(Map),
Result = mysql_poolboy:query(mypool, SQLFormat, Vals).
```
