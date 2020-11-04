# Redis数据类型

[Redis命令](http://redisdoc.com/)

##  1 String 字符串

### 1.1 命令

#### 1.1.1 SET、STENX、SETEX、PSETEX

```bash

127.0.0.1:6379> set str1 "hello" ## key 不存在时 为它设置值
OK
127.0.0.1:6379> get str1 
"hello"
127.0.0.1:6379> set str1 "hello1" ##key存在时 跟新其值
OK
127.0.0.1:6379> get str1 
"hello1"
127.0.0.1:6379> set str1 "hello1" NX  ##NX 当key 存在时 什么都不做
(nil)
127.0.0.1:6379> get str1 
"hello1"
127.0.0.1:6379> set str2 "123" NX  ##NX 当key 不存在时 为其赋值
OK
127.0.0.1:6379> get str2
"123"
127.0.0.1:6379> set str1 "hello2" XX ## 与NX 相反
OK
127.0.0.1:6379> get str1 
"hello2"
127.0.0.1:6379> set str1 "hello2" EX 10  ## EX 设置过期时间 单位秒
OK
127.0.0.1:6379> TTL str1
(integer) 6
127.0.0.1:6379> set str1 "hello2" PX 1000  ## PX 设置过期时间 单位毫秒
OK
127.0.0.1:6379> TTL str1
(integer) -2


127.0.0.1:6379> get str1
"123"
127.0.0.1:6379> setNX str1 "1234" ## 当key 不存在时 为其赋值
(integer) 0
127.0.0.1:6379> get str1
"123"

127.0.0.1:6379> SETEX str1 60  "321"  ## 将键 key 的值设置为 value ， 并将键 key 的生存时间设置为 seconds 秒钟，如果键 key 已经存在， 那么 SETEX 命令将覆盖已有的值。
OK
127.0.0.1:6379> get str1
"321"
127.0.0.1:6379> TTL str1
(integer) 48
127.0.0.1:6379> PSETEX str1 10000 "4321" ##这个命令和 SETEX 命令相似， 但它以毫秒为单位设置 key 的生存时间
OK
127.0.0.1:6379> get str1
"4321"
```
#### 1.1.2 GET 、GETSET

```bash
##如果键 key 不存在， 那么返回特殊值 nil ； 否则， 返回键 key 的值
127.0.0.1:6379> get str2
"123"
127.0.0.1:6379> get str3
(nil)
##getset 将键 key 的值设为 value ， 并返回键 key 在被设置之前的旧值。
127.0.0.1:6379> GETSET str2 "yyf"
"123"
127.0.0.1:6379> get str2
"yyf"
```

#### 1.1.3  STRLEN

```bash
127.0.0.1:6379> STRLEN str2
(integer) 3
127.0.0.1:6379> STRLEN str3
(integer) 0
```

#### 1.1.4 APPEND 

```bash
127.0.0.1:6379> APPEND str3 "123"
(integer) 3
127.0.0.1:6379> get str3
"123"
127.0.0.1:6379> get str2
"yyf"
127.0.0.1:6379> APPEND str2 "zhenshuai"
(integer) 12
127.0.0.1:6379> get str2
"yyfzhenshuai"
```

#### 1.1.5 SETRANGE 、GETRANGE

```bash
127.0.0.1:6379> SETRANGE str2 3 666
(integer) 12
127.0.0.1:6379> get str2
"yyf666nshuai"
127.0.0.1:6379> 
127.0.0.1:6379> SETRANGE str5 4 "666"
(integer) 7
127.0.0.1:6379> get str5
"\x00\x00\x00\x00666"

127.0.0.1:6379> GETRANGE str2 0 4
"yyf66"
127.0.0.1:6379> GETRANGE str2 -1 -5
""
127.0.0.1:6379> GETRANGE str2 -5 -1
"shuai"
127.0.0.1:6379> GETRANGE str2 0 -1 
"yyf666nshuai"
127.0.0.1:6379> GETRANGE str2 0 10086
"yyf666nshuai"

```

#### 1.1.6 INCR、INCRBY、INCRBYFLOAT

```bash
127.0.0.1:6379> set num1 1
OK
127.0.0.1:6379> INCR num1
(integer) 2
127.0.0.1:6379> get num1
"2"
127.0.0.1:6379> INCR num2 
(integer) 1
127.0.0.1:6379> get num2
"1"

127.0.0.1:6379> INCRBY num2 10
(integer) 11
127.0.0.1:6379> get num2
"11"
127.0.0.1:6379> INCRBYFLOAT num2 3.5
"14.5"
```

#### 1.1.7 DECR、DECRBY

```bash
127.0.0.1:6379> DECR num3
(integer) -1
127.0.0.1:6379> DECR num3
(integer) -2
127.0.0.1:6379> DECRBY num3 10
(integer) -12
```

#### 1.1.8 MSET、MSETNX、MGET

```bash
127.0.0.1:6379> mset key1 1 key2 2 key3 3
OK
127.0.0.1:6379> mget key1 key2 key3
1) "1"
2) "2"
3) "3"
127.0.0.1:6379> MSETNX key1 4 key2 5 key3 6
(integer) 0
127.0.0.1:6379> mget key1 key2 key3
1) "1"
2) "2"
3) "3"
```




## 2 List（列表）

## 3 Set （集合）

## 4 Hash(哈希)

## 5 zset (有序集合)
```

```