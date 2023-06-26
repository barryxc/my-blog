---
title: shell语法练习
date: 2023-06-23 19:51:02
tags: shell
category: shell
---

[牛客网练习](https://www.nowcoder.com/exam/oj?page=1&tab=SHELL%E7%AF%87&topicId=195)

## 查看可用的shell

```
cat /etc/shells
```

## shebang

```shell
#!/bin/sh
```

## 字符串

```shell
str="hello world!"

echo "定义字符串 ${str}"
echo "字符串的长度为 ${#str}"
echo "截取索引从1开始，长度为4的子串 ${str:1:4}"
```

## 数组

```shell
a=(234 2 3 4 5 6)

echo "定义数组 a=(${a[*]})"
echo "数组的长度为 ${#a[*]}"
echo "数组第一个元素的长度${#a[0]}"
```

<!--more-->

## 脚本参数传递

```shell
echo "执行的文件名 $0"
echo "脚本的所有的参数 $*"
echo "脚本的参数个数 $#"
echo "脚本的第一个参数 $1"
echo "脚本的第二个参数 $2"
```

## 流程控制语句

```shell
read -p "请输入字符串" input


#ifelse

# 字符串运算符
if [[ $input ]]; then
	echo "输入的字符串不为空"
else
	echo "输入的字符串为空"
fi

if [[ -n $input ]]; then
	echo "输入的字符串长度不为0"
else
	echo "输入的字符串长度为0"
fi
	
# 文件测试运算符
if [[ ! -e "./test.sh" ]]; then
	echo "./test.sh 文件不存在"
else
	echo "./test.sh 文件存在哈"
fi

```

## 换行
```shell
echo "这里显示换行"
echo "\n"
echo "这里显示换行"
```


## 选择分支语句

```shell
read -p "请输入0-9数字，会自动生成成语" num

case $num in
	1 )
		echo "一生一世"
		;;
	2)
		ehco "二龙戏珠"
		;;
	3)
		echo "三阳开泰"
		;;
	*)
		echo "输入了其他值"
		;;
esac
```


## 循环语句

```shell
read -p "请输入一句话，循环打印每个单词" words

for w in $words; do
	echo "${w}"
done


read -p "请输入0-9数字，循环打印数字" nums

while [[ $nums -gt 0 ]]; do
	echo "$nums" 
	nums=$((nums-1))
	# let nums=nums-1
done
```


## 数学运算
```shell
read -p "输入一个数字" inputNum
echo "减一得 $((inputNum-1))"
let inputNum=inputNum-2;
echo "减二得$inputNum"
```


## 函数调用

```shell
printfunc(){
	echo "printfunc() 函数被调用了"
	echo "函数的参数个数为$#"
	echo "第一个参数为$1"
	echo "第二个参数为$2"
	echo "第三个参数为$3"
	echo "第四个参数为$4"
}

printfunc 参数1 参数2 参数3 参数4 
echo "函数返回值 $?"
```
