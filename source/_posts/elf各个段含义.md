---
title: ELF各个段含义
date: 2025-08-06
tags: c++
category: c++
---

##  1. [ELF文件结构](https://www.openeuler.openatom.cn/zh/blog/lijiajie128/2020-11-03-ELF%E6%96%87%E4%BB%B6%E6%A0%BC%E5%BC%8F%E8%A7%A3%E6%9E%90)

​        ELF文件的格式大致如下，其中比较重要的时文件头和段表：文件头描述文件的基本信息；段表类似所有段即section的指针表。

文件头定义了 ELF Magic Code、文件机器字节长度、数据存储方式、版本、运行平台、ABI 版本、ELF 重定位类型、硬件平台、硬件平台版本、入口地址、程序头入口与长度、Section Header 的偏移位置和长度以及 Section 数量等。

```SQL
ELF Header:
  Magic:   7f 45 4c 46 02 01 01 00 00 00 00 00 00 00 00 00
  Class:                             ELF64
  Data:                              2's complement, little endian
  Version:                           1 (current)
  OS/ABI:                            UNIX - System V
  ABI Version:                       0
  Type:                              REL (Relocatable file)
  Machine:                           Advanced Micro Devices X86-64
  Version:                           0x1
  Entry point address:               0x0
  Start of program headers:          0 (bytes into file)
  Start of section headers:          1000 (bytes into file)
  Flags:                             0x0
  Size of this header:               64 (bytes)
  Size of program headers:           0 (bytes)
  Number of program headers:         0
  Size of section headers:           64 (bytes)
  Number of section headers:         15
  Section header string table index: 14
```

**段表：**

​        段表顾名思义，存储不同段的地方，实际存储的是段的描述符，该描述符会描述段的类型，大小等信息。可通过`readelf -S main.o`查看，因为下面需要用到一些段因此贴到这里。

```SQL
There are 15 section headers, starting at offset 0x3e8:
Section Headers:
  [Nr] Name              Type             Address           Offset
       Size              EntSize          Flags  Link  Info  Align
  [ 0]                   NULL             0000000000000000  00000000 0000000000000000  0000000000000000           0     0     0
  [ 1] .text             PROGBITS         0000000000000000  00000040 000000000000003e  0000000000000000  AX       0     0     1
  [ 2] .rela.text        RELA             0000000000000000  00000310 0000000000000018  0000000000000018   I      12     1     8
  [ 3] .data             PROGBITS         0000000000000000  00000080 0000000000000005  0000000000000000  WA       0     0     4
  [ 4] .bss              NOBITS           0000000000000000  00000088 0000000000000005  0000000000000000  WA       0     0     4
  [ 5] .rodata           PROGBITS         0000000000000000  00000088 0000000000000007  0000000000000000   A       0     0     1
  [ 6] .data.rel.local   PROGBITS         0000000000000000  00000090 0000000000000008  0000000000000000  WA       0     0     8
  [ 7] .rela.data.rel.lo RELA             0000000000000000  00000328 0000000000000018  0000000000000018   I      12     6     8
  [ 8] .comment          PROGBITS         0000000000000000  00000098 000000000000002a  0000000000000001  MS       0     0     1
  [ 9] .note.GNU-stack   PROGBITS         0000000000000000  000000c2 0000000000000000  0000000000000000           0     0     1
  [10] .eh_frame         PROGBITS         0000000000000000  000000c8 0000000000000058  0000000000000000   A       0     0     8
  [11] .rela.eh_frame    RELA             0000000000000000  00000340 0000000000000030  0000000000000018   I      12    10     8
  [12] .symtab           SYMTAB           0000000000000000  00000120 0000000000000198  0000000000000018          13    12     8
  [13] .strtab           STRTAB           0000000000000000  000002b8 0000000000000051  0000000000000000           0     0     1
  [14] .shstrtab         STRTAB           0000000000000000  00000370 0000000000000076  0000000000000000           0     0     1
Key to Flags:
  W (write), A (alloc), X (execute), M (merge), S (strings), I (info),
  L (link order), O (extra OS processing required), G (group), T (TLS),
  C (compressed), x (unknown), o (OS specific), E (exclude),
  l (large), p (processor specific)
```

<!--more-->

具体含义：

```
- .text段
  存储程序的可执行代码（机器指令），是只读的。编译后的二进制代码段在此存放，确保代码不会被意外修改。例如，C语言编译后的函数实现会存储在此段。
- .data段
  存储已初始化的全局变量和静态变量。例如，`int a = 10;` 这样的全局变量会被编译到此段。运行时该段内容会被加载到内存中。
- .bss段 (block started by symbol)
  存储未初始化的全局变量和静态变量。例如，`int b;` 这样的全局变量会被编译到此段。运行时系统会将其初始化为0，并分配内存空间。
- .rodata段
  存储只读数据，包括字符串常量（如`"hello"`）、`const`修饰的常量变量等。例如，`const char* str = "test";` 中的字符串常量会存储在此段。
- .symtab段
  符号表，记录函数和全局变量的符号信息（如名称、地址、类型等），用于链接阶段解析符号引用。
- .strtab段
  字符串表，存储符号表中引用的字符串常量和变量名，用于符号解析。
- .dynsym段
  动态符号表，记录动态链接所需的符号信息（如动态库中的函数和变量），用于运行时动态链接。
- .got.plt段
  全局偏移表（Global Offset Table），保存外部函数的绝对地址。动态链接时，通过此表重定向到实际函数地址。
- .rel.plt段
  PLT（Procedure Linkage Table）重定位表，用于关联`.dynsym`和`.got.plt`，实现动态链接时的地址修正。
- .data.rel.ro段
  存储只读的已初始化数据（如`const`修饰的全局变量），运行时会被标记为只读。
- .rela.dyn段
  动态重定位表，记录需要重定位的数据段（如`.data`、`.data.rel.ro`）的地址修正信息。
- .eh_frame段
  存储异常处理（Exception Handling）相关的调试信息，用于栈展开和错误恢复。
- .note.GNU-stack段
  标记栈的执行权限（如是否允许执行），用于安全防护。
```

**重定位表：**

​        重定位表主要记录了目标文件中所有需要重定位的符号所在的段以及相对（相对于该段开始）偏移位置。可以使用`objdump -r main.o`查看该表的内容，从内容中能够看到存储的时相关函数和变量的在目标文件中的相对位置。

```SQL
Relocation section '.rela.text' at offset 0x310 contains 1 entry:
  Offset          Info           Type           Sym. Value    Sym. Name + Addend
000000000033  000c00000002 R_X86_64_PC32     0000000000000000 _Z3addii - 4

Relocation section '.rela.data.rel.local' at offset 0x328 contains 1 entry:
  Offset          Info           Type           Sym. Value    Sym. Name + Addend
000000000000  000500000001 R_X86_64_64       0000000000000000 .rodata + 0

Relocation section '.rela.eh_frame' at offset 0x340 contains 2 entries:
  Offset          Info           Type           Sym. Value    Sym. Name + Addend
000000000020  000200000002 R_X86_64_PC32     0000000000000000 .text + 0
000000000040  000200000002 R_X86_64_PC32     0000000000000000 .text + 14
```

**字符串表:**

​        字符串表中存储ELF文件中使用到的字符串，一般有三种字符串表分别为`shstrtab`保存`section`头中保存的字符串；`strtab`保存elf中使用到的字符串；`dynstr`保存了动态链接字符串表，表中存放了一系列字符串，这些字符串代表了符号名称，以空字符作为终止符。

## 2 链接中的符号

### 1.1 符号

​        程序需要链接的原因时因为程序的每个文件特别是C类的语言时单独分模块编译的，每个编译单元仅仅知道当前编译单元中的信息，当引用到其他编译单元的函数或者变量时无法明确该变量或者函数的地址。因此需要在连接时将这些符号的地址明确，一般函数和变量统称为符号，函数名和变量名为符号名。

​        编译时每个编译单元都会有一个符号表表明对应的符号在当前编译单元中的地址和值，因此在链接时需要将多个编译单元的符号表合并。

​        使用`readelf -s main.o`查看符号表，能够看到符号表中包含符号的名称、索引、值、尺寸、作用域等信息。

```SQL
Symbol table '.symtab' contains 17 entries:
   Num:    Value          Size Type    Bind   Vis      Ndx Name
     0: 0000000000000000     0 NOTYPE  LOCAL  DEFAULT  UND
     1: 0000000000000000     0 FILE    LOCAL  DEFAULT  ABS main.cpp
     2: 0000000000000000     0 SECTION LOCAL  DEFAULT    1
     3: 0000000000000000     0 SECTION LOCAL  DEFAULT    3
     4: 0000000000000000     0 SECTION LOCAL  DEFAULT    4
     5: 0000000000000000     0 SECTION LOCAL  DEFAULT    5
     6: 0000000000000000     0 SECTION LOCAL  DEFAULT    6
     7: 0000000000000004     1 OBJECT  LOCAL  DEFAULT    3 _ZZ4mainE8static_a
     8: 0000000000000004     1 OBJECT  LOCAL  DEFAULT    4 _ZZ4mainE8static_b
     9: 0000000000000000     0 SECTION LOCAL  DEFAULT    9
    10: 0000000000000000     0 SECTION LOCAL  DEFAULT   10
    11: 0000000000000000     0 SECTION LOCAL  DEFAULT    8
    12: 0000000000000000    20 FUNC    GLOBAL DEFAULT    1 _Z3addii
    13: 0000000000000000     8 OBJECT  GLOBAL DEFAULT    6 file
    14: 0000000000000000     4 OBJECT  GLOBAL DEFAULT    3 glob_a
    15: 0000000000000000     4 OBJECT  GLOBAL DEFAULT    4 glob_b
    16: 0000000000000014    42 FUNC    GLOBAL DEFAULT    1 main
```

**特殊符号**：链接生成可执行文件时会连接器会定义很多特殊符号：

- `executable_start`：程序起始地址；
- `etext,_etext,__etext`：代码段的结束地址；
- `edata,_edata`：数据段的结束地址；
- `end,_en`：程序的结束地址。

```C
#include <stdio.h>

extern char __executable_start[];
extern char etext[], _etext[], __etext[];
extern char edata[], _edata[];
extern char end[], _end[];

int main(){
    printf("executable start %X\n", __executable_start);
    printf("text end %X %X %X\n", etext, _etext, __etext);
    printf("data end %X %X\n", edata, _edata);
    printf("executable end %X %X\n", end, _end);

    return 0;
}
```

​        运行结果：

```SQL
executable start CB200000
text end CB20075D CB20075D CB20075D
data end CB401010 CB401010
executable end CB401018 CB401018
```

### 1.2 函数签名

​        编译器为了更好的引用其他模块中的符号对模块中使用到的符号进行符号修饰，即符号签名。签名规则：

- 所有的符号都以"_Z"开头，对于嵌套的名字（在名称空间或在类里面的），后面紧跟"N"；
- 然后是各个名称空间和类的名字，每个名字前是名字字符串长度，再以"E"结尾。比如`N::C::func`经过名称修饰以后就是`_ZN1N1C4funcE`；
- 对于一个函数来说，它的参数列表紧跟在"E"后面，对于int类型来说，就是字母"i"。所以整个`N::C::func(int)`函数签名经过修饰为`_ZN1N1C4funcEi`；
- 符号签名中包含参数类型也是C++实现函数重载的基础，但是C++也常常需要使用C的接口，如果使用C++的符号签名则无法找到对应的接口。可利用C++中的`extern "C"`关键字保证对应的函数的符号签名使用C的规则。

### 1.3 弱符号和强符号

​        C中存在强符号和弱符号，强符号不允许多重定义，弱符号允许多个定义但是实际运行时只有一个实体。对于C语言来说，编译器默认函数和初始化了的全局变量为强符号，未初始化的全局变量为弱符号(C++并没有将未初始化的全局符号视为弱符号)。

对于它们，下列三条规则使用：

- 同名的强符号只能有一个，否则编译器报"重复定义"错误；
- 允许一个强符号和多个弱符号，但定义会选择强符号的；
- 当多个弱符号时，选择占用空间最大的；
- 当有多个弱符号相同时，链接器选择最先出现那个，也就是与链接顺序有关。

​        强引用和弱引用主要针对函数，强引用如果未找到定义则报错，二弱引用未找到定义则不报错。如果未定义，连接器会将弱引用设定为0或者特殊值，弱引用可以用于接口设计。
