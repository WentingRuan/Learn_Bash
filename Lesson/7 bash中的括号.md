# 7 bash中的括号

标签（空格分隔）：bash
---
#( )
( program ) run a program
( program ) > a.log
put the program into a.log,if you cat the file, the program will be executed.
```
for i in `seq 3`;do echo hi; done > b.log
( for i in `seq 3`;do echo hi; done ) > b.log
```
a=( program )

```bash
(`seq 3`) # run `seq 3`,command 1 not found
a=( `seq 3`) #将seq 3的结果赋给a，a是一个数组
echo $a
```
(program)
```
(
echo a
echo b
echo c
)

# == ( echo a; echo b; echo c;)

a=123
(
echo $a
echo $1
echo $2
)

# == (echo $a; echo $1; echo $2 ;) 

```
```
a=`seq 10`
a=$(seq 10)

```



