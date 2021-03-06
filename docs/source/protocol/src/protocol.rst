Kafka消息 Speicification
------------------------

+---------+---------+---------+-------+
| 名字    | 类型    | 对应Java类 | 意义 |
|         |         | 型      |       |
+=========+=========+=========+=======+
| binlog  | 字符串  | String  | MYSQL |
|         |         |         | 的binl |
|         |         |         | og文件和 |
|         |         |         | offse |
|         |         |         | t，\ ` |
|         |         |         | 格式为of |
|         |         |         | fset@ |
|         |         |         | binlo |
|         |         |         | g-fil |
|         |         |         | e <ma |
|         |         |         | ilto: |
|         |         |         | 格式为of |
|         |         |         | fset@ |
|         |         |         | binlo |
|         |         |         | g-fil |
|         |         |         | e>`__ |
+---------+---------+---------+-------+
| time    | 64位整型 | long   | 以毫秒为单 |
|         |         |         | 位的Uni |
|         |         |         | x时间戳， |
|         |         |         | 代表此bi |
|         |         |         | nlog条 |
|         |         |         | 目产生的时 |
|         |         |         | 间    |
+---------+---------+---------+-------+
| canalTi | 64位整型 | long   | 以毫秒为单 |
| me      |         |         | 位的Uni |
|         |         |         | x时间戳， |
|         |         |         | 代表bin |
|         |         |         | log经过 |
|         |         |         | 到达Kaf |
|         |         |         | kaRiv |
|         |         |         | erCan |
|         |         |         | al程序的 |
|         |         |         | 时间，也可 |
|         |         |         | 视为消息进 |
|         |         |         | 入kafk |
|         |         |         | a的时间 |
+---------+---------+---------+-------+
| db      | 字符串  | String  | MYSQL |
|         |         |         | 一个数据库 |
|         |         |         | 的sche |
|         |         |         | ma名（一 |
|         |         |         | 般情况下与 |
|         |         |         | 数据库名一 |
|         |         |         | 样，某些情 |
|         |         |         | 况也可能不 |
|         |         |         | 一样，请咨 |
|         |         |         | 询相关数据 |
|         |         |         | 库的DBA |
|         |         |         | ）    |
+---------+---------+---------+-------+
| table   | 字符串  | String  | 此条bin |
|         |         |         | log影响 |
|         |         |         | 的MYSQ |
|         |         |         | L的一个表 |
|         |         |         | 的表名 |
+---------+---------+---------+-------+
| event   | 字符型  | char    | 代表bin |
|         |         |         | log事件 |
|         |         |         | 类型，目前 |
|         |         |         | 只解析出了 |
|         |         |         | inser |
|         |         |         | t,    |
|         |         |         | updat |
|         |         |         | e     |
|         |         |         | &     |
|         |         |         | delet |
|         |         |         | e（对应的 |
|         |         |         | 值为'i' |
|         |         |         | ,     |
|         |         |         | 'u'和' |
|         |         |         | d'）  |
+---------+---------+---------+-------+
| columns | JSON数组 | ``Array | MYSQL |
|         |         | List<Ob | 表一个ro |
|         |         | ject>`` | w的各个c |
|         |         |         | olumn |
|         |         |         | ，包含这次 |
|         |         |         | 事件影响的 |
|         |         |         | 数据，详见 |
|         |         |         | 表二  |
+---------+---------+---------+-------+
| keys    | JSON数组 | ``Array | MYSQL |
|         |         | List<St | keys  |
|         |         | ring>`` |       |
+---------+---------+---------+-------+

其中，columns数组的每个元素specification见表二。

+---------+---------+---------+-------+
| 名字    | 类型    | 对应Java类 | 意义 |
|         |         | 型      |       |
+=========+=========+=========+=======+
| v       | 字符串  | String  | value |
|         |         |         | 的缩写，即 |
|         |         |         | 该列的值。 |
|         |         |         | 对于ins |
|         |         |         | ert，即 |
|         |         |         | 插入的新值 |
|         |         |         | ；对于up |
|         |         |         | date， |
|         |         |         | 即upda |
|         |         |         | te之后的 |
|         |         |         | 值；而对于 |
|         |         |         | delet |
|         |         |         | e，则为删 |
|         |         |         | 除前的值 |
+---------+---------+---------+-------+
| updated | 布尔    | boolean | 本次事件该 |
|         |         |         | 字段是否被 |
|         |         |         | 更新了。仅 |
|         |         |         | 对upda |
|         |         |         | te事件有 |
|         |         |         | 意义，对i |
|         |         |         | nsert |
|         |         |         | 和dele |
|         |         |         | te一概为 |
|         |         |         | true， |
|         |         |         | 因此略去 |
+---------+---------+---------+-------+
| t       | 字符串  | String  | type的 |
|         |         |         | 缩写，即这 |
|         |         |         | 个列的MY |
|         |         |         | SQL数据 |
|         |         |         | 类型。例如 |
|         |         |         | decim |
|         |         |         | al(10 |
|         |         |         | ,4)   |
+---------+---------+---------+-------+
| origin\ | 字符串  | String  | origi |
| _val    |         |         | n\_va |
|         |         |         | lue的缩 |
|         |         |         | 写，该列更 |
|         |         |         | 新之前的旧 |
|         |         |         | 值。仅对u |
|         |         |         | pdate |
|         |         |         | 事件，且u |
|         |         |         | pdate |
|         |         |         | d为tru |
|         |         |         | e的字段有 |
|         |         |         | 效。  |
+---------+---------+---------+-------+
| null    | 布尔    | boolean | 该字段的值 |
|         |         |         | 是否为nu |
|         |         |         | ll    |
+---------+---------+---------+-------+
| n       | 字符串  | String  | name的 |
|         |         |         | 缩写，即M |
|         |         |         | YSQL表 |
|         |         |         | 的一个列的 |
|         |         |         | 列名  |
+---------+---------+---------+-------+

INSERT消息样例：

::

    { 
    "binlog": "6816@mysql-bin.000070", 
    "time": 1450235092000,
    "canalTime": 1450235093370,
    "db": "TestCanal", 
    "table": "g_order_010",
    "event": "i",
    "columns": [ 
    { "n": "order_id", "t": "bigint(20)", "v": "126", "null": false }, 
    { "n": "driver_id", "t": "bigint(20)", "v": "123456", "null": false }, 
    { "n": "driver_phone", "t": "varchar(15)", "v": "13264494028", "null": false }, 
    { "n": "passenger_id", "t": "bigint(20)", "v": "654321", "null": false },
    { "n": "starting_lat", "t": "decimal(10,6)", "v": "121.445000", "null": false },
    { "n": "consult_time", "t": "timestamp", "v": "2015-08-10 13:08:13", "null": false }
    ],
    "keys": [ "order_id" ] }

UPDATE消息样例：

::

    {
    "binlog": "25521@mysql-bin.000070",
    "time": 1450236307000,
    "canalTime": 1450236308279,
    "db": "TestCanal",
    "table": "g_order_010",
    "event": "u",
    "columns": [
    {"n": "order_id", "t": "bigint(20)", "v": "126", "null": false, "updated": false},
    {"n": "driver_id", "t": "bigint(20)", "v": "123456", "null": false, "updated": false},
    { "n": "passenger_id", "t": "bigint(20)", "v": "654321", "null": false, "updated": false},
    {"n": "current_lng", "t": "decimal(10,6)", "v": "39.021400", "null": false, "updated": false},
    {"n": "current_lat", "t": "decimal(10,6)", "v": "120.423300", "null": false, "updated": false},
    { "n": "starting_lng", "t": "decimal(10,6)", "v": "38.128000", "null": false, "updated": false},
    { "n": "starting_lat", "t": "decimal(10,6)", "v": "121.445000", "null": false, "updated": false},
    { "n": "dest_name", "t": "varchar(100)", "v": "Renmin University", "origin_val": "知春路", "null": false, "updated": true}
    ],
    "keys": ["order_id"]
    }

DELETE消息样例：

::

    {
    "binlog": "58851@mysql-bin.000070",
    "time": 1450237034000,
    "canalTime": 1450237034492,
    "db": "TestCanal",
    "table": "g_order_010",
    "event": "d",
    "columns": [
    {"n": "order_id", "t": "bigint(20)", "v": "126", "null": false},
    {"n": "driver_id", "t": "bigint(20)", "v": "123456", "null": false},
    {"n": "driver_phone", "t": "varchar(15)", "v": "13264494028", "null": false},
    {"n": "passenger_id", "t": "bigint(20)", "v": "654321", "null": false},
    {"n": "current_lng", "t": "decimal(10,6)", "v": "39.021400", "null": false}
    ],
    "keys": ["order_id"]
    }
