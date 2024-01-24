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

### 字符串处理

```shell
str="hello world!"

echo "定义字符串 ${str}"
#计算字符串长度
echo "字符串的长度为 ${#str}"
#截取字符串
echo "截取索引从1开始，长度为4的子串 ${str:start:length}"
#字符串替换
echo "把老的字符串替换为新的字符串 ${str//${oldstr}/${newstr}}"
```

<!--more-->

### 正则匹配

```shell
str="hello world"
#方式一：
if [[ $(echo "${str}" | grep -E '^he.*ld$') ]]; then
    echo "匹配成功"
fi
# ---------- ---------- ---------- ---------- ----------
#方式二 正则表达式要用单引号引起来
if expr match "$str" 'he.*ld' > /dev/null; then
    echo "匹配成功"
fi
#等同
if expr  "$str" : 'he.*ld' > /dev/null; then
    echo "匹配成功"
fi

# expr 字符串匹配捕获
expr "$str" : 'he.*ld' 输出匹配的字符串的长度
expr "$str" : 'he.*ld\(xxx\)' 若匹配，则输出捕获的字符串 xxx

```

### 正则语法

> Bash 中的正则表达式分为基本正则表达式和扩展正则表达式两种类型。
>
> 基本正则表达式：它只支持最基本的正则表达式元字符，如 ^、$、.、[ ]、*、`` 等，不支持一些常用的元字符，如 +、?、| 等。在基本正则表达式中，圆括号 () 表示括号本身，而不是捕获组。
>
> 扩展正则表达式：它支持基本正则表达式中的所有元字符，同时还支持一些额外的元字符，如 +、?、| 等，以及一些高级语法，如 ( ) 捕获组、{ } 重复指定次数等。
>
> 因此，扩展正则表达式比基本正则表达式更加强大，可以实现更复杂的匹配和替换操作。在 Bash 中，grep、sed 等工具默认使用基本正则表达式，要使用扩展正则表达式，需要在正则表达式前面添加 -E 参数或者使用 egrep 命令。例如：
>

```shell
#使用基本正则表达式
grep "a*b" file.txt

# 使用扩展正则表达式
grep -E "a+b" file.txt
egrep "a+b" file.txt

```

> 需要注意的是，在不同的工具中，正则表达式的语法和功能可能也会略有不同，具体使用时需要查看对应的文档。

### 数组

#### 索引数组

```shell
declare -a arr

#赋值
arr=(234 2 3 4 5 6)
#添加数组元素
arr+="ss"
#所有元素
echo "${a[*]}"
#数组的长度
echo "数组的长度为 ${#arr[*]}"
#访问元素
echo "数组第一个元素的长度${#arr[0]}"
```

#### 关联数组

```shell
declare -A map 

map["google"]="www.google.com"
map["baidu"]="www.baidu.com"

#访问所有元素
echo "${a[*]}"
#获取数组的长度
echo "${#a[*]}"
#访问所有key
echo "${!a[*]}"
#根据key访问元素
echo "${a[${key}]}"
```

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

### `set --`

```
set -- "$args0" "$args1"

用于将变量 "$args0" 和 "$args1" 的值设置为脚本或函数的第一个和第二个位置参数。
在 Unix shell 中，"set" 命令用于设置或显示各种 shell 选项和参数。使用 "--" 选项时，表示选项结束，后续的任何参数都将作为位置参数处理。
```

### 输出当前脚本文件目录

```shell
dirname "$0"
```

