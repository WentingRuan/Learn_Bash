# 6 if语句 bash

标签（空格分隔）： bash

---
#基本语法
```
if <TEST>; then

else

fi
```

`<TEST>` 可以是一个 `[  ]`, `[[  ]]`, `((  ))`, 也可以是进程输出结果

##条件是单中括号表达式`[ ]`
数字比较

```shell
a=1
[ $a -lt 0 ]
```
```shell
if [ $a -lt 0 ];then echo right;else echo wrong; fi
```
```shell
if [ $a -lt 0 ]; then
   echo right
else 
   echo wrong
fi
```
数字比较,先将字符串转化成数字再比较
```bash
b="122"
a=123
let b=b+1

[ $a -eq $b ] && echo hi
[ $a = $b ] && echo hi
[ $a -lt "123" ] && echo hi
```
单括号内部使用`<` `>`和 `\<`
目前来看，是无意义的比较，无需再试
数字
```
$ [ "123" \> 31 ] && echo hi

$ [ "123" \< 31 ] && echo hi
hi

$ [ 123 < 31 ] && echo hi
bash: 31: No such file or directory
```
字母比较
```
#ASCII 由小到大是 0123456789A-Za-z
[ a \< A ] && echo hi  #错
[ a < A ] && echo hi #hi
```
![image_1b9dhbdas1v9319ju12hll82e729.png-15.4kB][1]

变量还原
```bash
unset a
unset: usage: unset [-f] [-v] [-n] [name ...]
```
单括号比较，不加`\`是无意义的
```
$ [ a > A ] && echo hi
hi

41914@DESKTOP-6SI2VOE MINGW64 ~/test
$ [ a < A ] && echo hi
hi
```

##条件是双中括号表达式`[[  ]]`
也就是字符串比较
About Matching Of **String**
`=~`
```bash
[[ "123" =~ 123* ]]
[[ "123" =~ [0-9]+ ]]
[[ "123" =~ [0-9]{0} ]]

```
比较`>` `=`
```bash
[[ "123" > 1* ]] && echo hi
[[ "123" = "123"* ]] && echo hi
```
双中括号里数字与字符串的比较区别
```
[[ "123" < 23 ]] && echo hi
[[ 123 < 23 ]] && echo hi
```
比较`[]`
```
[ "123" = 123 ]
```

Others:

```
ls /tmp
[[ -e /tmp || -e /NOT_EXIST ]] && echo hi
[ -e /tmp -o -e /NOT_EXIST ] && echo hi

Same with `-a` and `&&`

[[ -e /tmp && -e a.log ]] && echo hi

```

字符串比较
```
[[ 3 > 19 ]] && echo hi 
[ "3" \> "19" ] && echo hi
```
```
[[ A > a ]] && echo hi 
[[ A < b ]] && echo hi #bourne定义 从小到大：0-9aA-zZ
```
单括号的字符串比较，第一个大于即可。
```
[ a21 \> A210 ] && echo hi
```
双括号的字符串比较，第一个大于,或其余字符都相等时，任意一个大于另一个即可。
```
[[ A21 > a21 ]] && echo hi
[[ A21 > a210 ]] && echo hi #错

[[ A21 < A12 ]] && echo h

[[ A21 > a2* ]] && echo hi # *==space

[[ a > 10000000* ]] && echo hi 

```

|比较定义|从小到大|编码|
|---|---|---|
|bouren定义|由小到大|0123456789aAbBcCdD...zZ|
|ASCII| 由小到大| 0123456789A-Za-z|

## 条件是双小括号表达式`((  ))`

For math operation

```
a=1
let a=a+1
(( a=a+1 ))
echo $? #0
(( a=a+1, a==4 ))
echo $?
```
##条件是进程
```bash
 if cat -n a.log | head -n 3 ;then echo hi;else echo bi; fi
```
```
#bash_in_vim
if ps | grep pty4 ; then
  echo hi
else 
  echo bi 
fi
```
###多重条件用&&和||连接
```bash
 if cat -n a.log | head -n 3 && [[ -e /NOT_EXIST ]];then 
 echo hi;
 else echo bi; 
 fi
```

#判断命令
##数字
|数字类型命令|解释|
|---|---|
|-lt |is less than|
|-le| is less or equal|
|-gt|is greater than|
|-ge|is greater or equal|
|-eq|is equal to|
|-ne|is not equal to |

##文字
|文字类型命令|解释|
|---|---|
|-e|文件（夹）是否存在   |
|-f|文件是否存在|
|-d|目录是否存在|

##文件
|文件权限测试命令|解释|
|---|---|
|-w|文件存在且可写入|
|-r|文件存在且可读取|
|-x|文件存在且可执行|
|-u|文件具有SUID权限|

##字符串
|字符串测试|解释|
|---|---|
|=|等于|
|！=|不等于|
|n|非空，存在|
|>|大于|

##变量
|变量|解释|
|---|---|
|-z|变量是否不存在|
```bash
#变量是否不存在，是则返回True
 [ -z $a ] && echo a

```


  [1]: http://static.zybuluo.com/419145138/jukp8swt3ak9mwhb6xo9islv/image_1b9dhbdas1v9319ju12hll82e729.png