---
title: shell语法
date: 2023-06-23 00:57:32
tags: shell语法
category: shell
---

## 基础语法
|         语法               |
| ------------------------------------------------------------ |
| [变量](https://www.runoob.com/linux/linux-shell-variable.html) |
| [参数传递](https://www.runoob.com/linux/linux-shell-passing-arguments.html) |
| [数组使用](https://www.runoob.com/linux/linux-shell-array.html) |
| [运算符](https://www.runoob.com/linux/linux-shell-basic-operators.html) |
| [echo命令](https://www.runoob.com/linux/linux-shell-echo.html) |
| [流程控制](https://www.runoob.com/linux/linux-shell-process-control.html) |
| [函数](https://www.runoob.com/linux/linux-shell-func.html)   |
| [输入输出重定向](https://www.runoob.com/linux/linux-shell-io-redirections.html) |
| [文件包含](https://www.runoob.com/linux/linux-shell-include-file.html) |



## 语法练习

> [牛客网](https://www.nowcoder.com/exam/oj?page=1&tab=SHELL%E7%AF%87&topicId=195)

### 查看可用的shell

```shell
cat /etc/shells
```

### 查看当前正在使用的shell

```shell
#注意SHELL一定要是大写。可以看到，我目前使用的shell是/bin/bash
echo $SHELL
```

### 修改我的 shell 为zsh

```
 chsh -s /bin/zsh
```

### shebang

```shell
#!/bin/sh
```

### 字符串

```shell
str="hello world!"

echo "定义字符串 ${str}"
echo "字符串的长度为 ${#str}"
echo "截取索引从1开始，长度为4的子串 ${str:1:4}"
```

### 数组

```shell
a=(234 2 3 4 5 6)

echo "定义数组 a=(${a[*]})"
echo "数组的长度为 ${#a[*]}"
echo "数组第一个元素的长度${#a[0]}"
```

<!--more-->

### 脚本参数传递

```shell
echo "执行的文件名 $0"
echo "脚本的所有的参数 $*"
echo "脚本的参数个数 $#"
echo "脚本的第一个参数 $1"
echo "脚本的第二个参数 $2"
```

### 流程控制语句

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

### 换行

```shell
echo "这里显示换行"
echo "\n"
echo "这里显示换行"
```


### 选择分支语句

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


### 循环语句

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


### 数学运算

```shell
read -p "输入一个数字" inputNum
echo "减一得 $((inputNum-1))"
let inputNum=inputNum-2;
echo "减二得$inputNum"
```


### 函数调用

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

