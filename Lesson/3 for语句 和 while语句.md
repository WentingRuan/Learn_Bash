# 3 for语句 和 while语句

标签（空格分隔）： bash

---


#for语句


```
for i in `seq 10`; do echo hi; done
```
```bash
 for i in `seq 3`; do
   echo $d
   echo d
   echo $i
done
```


#while语句

```bash
while True; do echo hi; done
```

```bash
d="True"
while $d; do
  echo $d
  sleep 1m
done 
```
##在bash直接用while
```shell
d="True"
while $d;do echo hi;done
```
#循环+条件
```
echo start =========================
d=True
for i in `seq 10`;do
  if $d;then echo $i
  else echo wrong
  fi;
done
```
```
echo =========================
a=1
 for i in `seq 10`;do
  if [ $a -le 10 ]
   then echo $a
    let a=$a+1
   else break
  fi
done
```   


