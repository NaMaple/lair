[MySQL 5.7参考手册/第十一章数据类型](http://www.searchdoc.cn/rdbms/mysql/dev.mysql.com/doc/refman/5.7/en/data-types.com.coder114.cn.html)
<p>数值类型
<p>数字类型
<p>整数类型：tinyint、smallint、mediumint、int、bigint

| 类型 | 字节  | 范围(有符号) | 范围(无符号) | 
| :---: | :---: | :---: | :---: |
| tinyint | 1 | -128~127| 0~255 |
| smallint | 2 | -32768~32767 | 0~65535 |
| mediumint | 3 | -8388608~8388607| 0~16777215 |
| int | 4 | -2147483648~2147483647 | 0~4294967295 |
| bigint | 8 | -9223372036854775808~9223372036854775807| 0~18446744073709551615 |

1个字节，8位，2的8次方，11111111，无符号255，有符号占1位符号位。
4个字节，32位，2的32次方。

tinyint(1)和tinyint(4)区别
位字段类型，M表示每个值的位数，范围1-64，默认1

M代表的并不是存储在数据库中的具体的长度，以前总是会误以为int(3)只能存储3个长度的数字，int(11)就会存储11个长度的数字，这是大错特错的。

tinyint(1) 和 tinyint(4) 中的1和4并不表示存储长度，显示宽度，并不影响实际的取值范围，只有字段指定zerofill是有用，如tinyint(4)，如果实际值是2，如果列指定了zerofill，查询结果就是0002，左边用0来填充。和显示的宽度有关系。

```
CREATE TABLE `M` (
  `id` tinyint(4) NOT NULL AUTO_INCREMENT,
  `tiny_1` tinyint(1) NOT NULL,
  `tiny_2` tinyint(2) NOT NULL,
  `tiny_3` tinyint(3) NOT NULL,
  `tiny_4` tinyint(4) NOT NULL,
  `tiny_5` tinyint(5) NOT NULL,
  `tiny_6` tinyint(6) NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

ZEROFILL属性，补零，(6)，127，000127。

<p>定点类型：decimal、numeric