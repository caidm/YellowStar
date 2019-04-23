# 数据库表设计

数据库名：``yellowstar``

创建数据库SQL语句：``CREATE DATABASE yellowstar;``

## 用户表

表名：``user``

```sql
CREATE TABLE IF NOT EXISTS yw_user (
    uid INT UNSIGNED NOT NULL AUTO_INCREMENT KEY COMMENT 'UID',
    loginname VARCHAR(20) NOT NULL UNIQUE comment '登录名',
    username VARCHAR(20) NOT NULL UNIQUE comment '用户名',
    password CHAR(32) NOT NULL COMMENT '密码',
    user_type TINYINT UNSIGNED NOT NULL COMMENT '用户类型'
);
```

## 房产信息表

表名：``house``

```sql
CREATE TABLE IF NOT EXISTS yw_house (
    hid INT UNSIGNED NOT NULL AUTO_INCREMENT KEY COMMENT '房产编号',
    user_name VARCHAR(20) NOT NULL comment '房产持有人',
    identity VARCHAR(20) NOT NULL comment '身份证号',
    phone VARCHAR(11) NOT NULL comment '手机号码',
    house_type VARCHAR(20) NOT NULL comment '房产类型',
    area INT UNSIGNED NOT NULL COMMENT '住房面积',
    gmt_buy DATE NOT NULL COMMENT '购房时间',
    building VARCHAR(20) NOT NULL comment '楼号',
    unit VARCHAR(10) NOT NULL comment '小区单元',
    house_num VARCHAR(10) NOT NULL COMMENT '门牌号',
    has_car TINYINT NOT NULL COMMENT '是否有车',
    location VARCHAR(20) comment '位置',
    licenseplatenumber VARCHAR(8) comment '车牌号'
);
```

## 水费、电费表

表名：``cost``

```sql
CREATE TABLE IF NOT EXISTS cost (
    id INT UNSIGNED NOT NULL AUTO_INCREMENT KEY COMMENT '编号',
    hid INT UNSIGNED NOT NULL  COMMENT '外键房产id',
    cost_type TINYINT UNSIGNED NOT NULL comment '费用类型',
    price DECIMAL(18,2) UNSIGNED NOT NULL comment '价格',
    gmt_create DATETIME DEFAULT CURRENT_TIMESTAMP NOT NULL COMMENT '创建时间',
    FOREIGN KEY(hid) REFERENCES yw_house(hid)
);
```

## 快递表

表名：``express``

```sql
CREATE TABLE IF NOT EXISTS express (
    eid INT UNSIGNED NOT NULL AUTO_INCREMENT KEY COMMENT '编号',
    hid INT UNSIGNED NOT NULL  COMMENT '外键房产id',
    is_take TINYINT UNSIGNED DEFAULT 0 COMMENT '是否领取',
    gmt_create DATETIME DEFAULT CURRENT_TIMESTAMP NOT NULL COMMENT '创建时间',
    FOREIGN KEY(hid) REFERENCES yw_house(hid)
);
```

## 设备表

表名：``device``

```sql
CREATE TABLE IF NOT EXISTS device (
    did INT UNSIGNED NOT NULL AUTO_INCREMENT KEY COMMENT '编号',
    device_name VARCHAR(20) NOT NULL comment '设备名称',
    device_type VARCHAR(20) NOT NULL comment '设备类型',
    is_service TINYINT UNSIGNED DEFAULT 0 COMMENT '是否维修',
    processing_opinion VARCHAR(20) NOT NULL comment '处理意见',
    uid INT UNSIGNED NOT NULL COMMENT 'UID',
    gmt_create DATETIME DEFAULT CURRENT_TIMESTAMP NOT NULL COMMENT '创建时间' 
);
```