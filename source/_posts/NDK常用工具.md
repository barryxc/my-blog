---
title: NDK常用工具
date: 2023-03-31 14:24:31
tags: 
- symbols
- ndk
category: android
---

## readelf

`readelf` 是一个用于显示 ELF（Executable and Linkable Format）文件信息的命令行工具，它是 GNU Binutils 包的一部分。ELF 文件格式是在 Unix 系统上广泛使用的标准二进制格式，用于可执行文件、目标代码、共享库和核心转储（core dumps）。

以下是 `readelf` 的一些核心用法：

### 查看文件头信息（File Header）

```sh
readelf -h <ELF file>
```

这个命令显示 ELF 文件的文件头信息，包括 ELF 类型（如可执行文件、共享对象等）、入口点地址、程序头表位置、段头表位置等。

### 查看程序头表（Program Headers）

```sh
readelf -l <ELF file>
```

程序头表描述了文件在内存中的映射。这个命令显示了每个段的信息，如类型（如 `LOAD`、`DYNAMIC` 等）、偏移、虚拟地址、物理地址、文件大小和内存大小等。

### 查看段头表（Section Headers）

```sh
readelf -S <ELF file>
```

段头表包含了文件中所有段的信息。这个命令显示了每个段的名称、类型、地址、偏移、大小、链接信息、对齐和其他属性。

### 查看符号表（Symbol Table）

```sh
readelf -s <ELF file>
```

符号表包含了文件中的符号信息，如函数和变量名。这个命令显示了每个符号的名称、类型、大小、值（地址）和绑定信息。

### 查看动态段信息（Dynamic Section）

```sh
readelf -d <ELF file>
```

动态段包含了动态链接信息，这个命令显示了动态链接器需要的条目，如所需的共享库和符号。

### 查看重定位信息（Relocations）

```sh
readelf -r <ELF file>
```

重定位条目是由链接器用来修正指针和引用地址的。这个命令显示了重定位条目的信息，包括偏移、类型和符号。

### 查看所有信息

```sh
readelf -a <ELF file>
```

这个命令显示了 ELF 文件的所有重要信息，包括文件头、段头表、程序头表、符号表等。

### 查看版本信息（Version Info）

```sh
readelf -V <ELF file>
```

这个命令显示了文件的版本信息，包括版本符号表和版本需求表。

### 查看注释段（Note Sections）

```sh
readelf -n <ELF file>
```

注释段通常包含了额外的系统特定信息，这个命令显示了这些信息。

`readelf` 是一个功能强大的工具，它可以帮助开发者深入理解 ELF 文件的结构和内容。上述命令是 `readelf` 的一些核心用法，但它还有更多的选项和功能，可以通过 `readelf --help` 或 `man readelf` 来查看更多信息。

## NM

`nm` 是一个在 Unix-like 系统中用于检查二进制文件中符号信息的命令行工具，它是 GNU Binutils 包的一部分。符号通常指的是变量、函数、对象等编程元素的名称。`nm` 能够列出从目标文件（如 `.o` 文件）、库文件（如 `.a` 或 `.so` 文件）或可执行文件中提取的符号列表。

以下是 `nm` 的一些核心用法：

### 列出所有符号

```sh
nm <file>
```

这个命令会列出指定文件中的所有符号，包括变量名、函数名等。输出通常包括符号的地址、符号类型和符号名称。

### 只显示未定义的符号

```sh
nm -u <file>
```

使用 `-u` 选项可以只显示未定义的符号，即那些在目标文件中引用但未定义的符号，这些符号需要在链接时由其他目标文件或库提供。

### 按照地址排序

```sh
nm -n <file>
```

使用 `-n` 或 `--numeric-sort` 选项可以按照符号地址排序输出结果。

### 显示符号大小

```sh
nm --size-sort <file>
```

使用 `--size-sort` 选项可以按照符号大小排序输出结果。

### 解码（Demangle）C++ 符号名称

```sh
nm -C <file>
```

使用 `-C` 或 `--demangle` 选项可以解码（demangle）C++ 符号名称，使得它们更易于阅读。C++ 符号名称经过修饰（mangling）以包含类型和作用域信息，`nm` 可以将这些修饰过的名称转换回人类可读的形式。

### 显示行号信息

```sh
nm -l <file>
```

使用 `-l` 选项可以显示与符号相关的源代码行号信息（如果可用）。

### 显示符号类型

`nm` 输出中的每个符号旁边通常会有一个字符表示符号的类型，例如：

- `T` 表示符号在文本（代码）段中定义。
- `U` 表示符号未定义。
- `B` 表示符号在未初始化的数据段（bss）中定义。
- `D` 表示符号在初始化的数据段中定义。
- `R` 表示符号在只读数据段中定义。
- `?` 表示符号类型未知。

符号类型字符可能是大写或小写，大写通常表示全局符号，小写表示局部符号。

`nm` 是一个非常有用的工具，特别是在调试和分析二进制文件的符号信息时。上述命令是 `nm` 的一些基本用法，但它还有更多的选项和功能，可以通过 `nm --help` 或 `man nm` 来查看更多信息。

## objdump

`objdump` 是 GNU Binutils 包中的一个工具，用于显示二进制文件（如可执行文件、目标文件和库文件）的各种信息。它可以用来反汇编代码、显示二进制文件的结构、查看节（section）的内容等。

以下是 `objdump` 的一些核心用法：

### 反汇编代码

```sh
objdump -d <file>
```

使用 `-d` 或 `--disassemble` 选项可以反汇编文件中的机器代码，将其转换为汇编语言。这对于理解程序的执行流程非常有用。

### 显示所有头信息

```sh
objdump -x <file>
```

使用 `-x` 选项可以显示文件的所有头信息，包括文件头、程序头、节头等。

### 显示特定节的内容

```sh
objdump -s -j .text <file>
```

使用 `-s` 或 `--full-contents` 选项，结合 `-j` 或 `--section` 选项，可以显示指定节（如 `.text` 节）的内容。

### 显示符号表

```sh
objdump -t <file>
```

使用 `-t` 或 `--syms` 选项可以显示文件的符号表，包括函数和变量的名称、地址等信息。

### 显示重定位信息

```sh
objdump -r <file>
```

使用 `-r` 或 `--reloc` 选项可以显示文件的重定位信息，这对于理解链接器如何解析符号非常有用。

### 显示动态符号表

```sh
objdump -T <file>
```

使用 `-T` 选项可以显示动态符号表，这对于分析共享库中的符号特别有用。

### 显示文件的节和段信息

```sh
objdump -h <file>
```

使用 `-h` 或 `--section-headers` 选项可以显示文件的节头信息，包括每个节的名称、大小、地址等。

### 显示汇编代码和源代码

```sh
objdump -S <file>
```

使用 `-S` 或 `--source` 选项可以将汇编代码与源代码交错显示，这需要编译时包含调试信息。

### 反汇编特定函数

```sh
objdump -d --start-address=<address> --stop-address=<address> <file>
```

使用 `--start-address` 和 `--stop-address` 选项可以反汇编从某个地址开始到另一个地址结束的代码区域。这对于只查看特定函数的汇编代码非常有用。

`objdump` 是一个非常强大的工具，它提供了多种选项来查看和分析二进制文件的不同方面。上述命令是 `objdump` 的一些核心用法，但它还有更多的选项和功能，可以通过 `objdump --help` 或 `man objdump` 来查看更多信息。

## ndk-stack

`ndk-stack` 是一个随 Android Native Development Kit (NDK) 提供的工具，它用于将 Android 应用程序的原生崩溃日志（通常包含内存地址）转换为更易于理解的符号化堆栈跟踪，其中包括函数名、源文件名和行号。这个工具特别有用，因为它可以帮助开发者分析和调试 C 或 C++ 代码中的崩溃问题。

### 核心用法

要使用 `ndk-stack`，你需要提供崩溃时的日志和未剥离（包含调试符号的）的二进制文件。以下是 `ndk-stack` 的基本用法：

```sh
ndk-stack -sym <path-to-unstripped-libs> -dump <path-to-crash-log>
```

- `-sym <path-to-unstripped-libs>`：这个选项后面跟的是包含未剥离二进制文件（如 `.so` 文件）的目录路径。这些文件包含了必要的调试符号，`ndk-stack` 需要它们来解析崩溃日志中的地址。

- `-dump <path-to-crash-log>`：这个选项后面跟的是包含崩溃日志的文件路径。你可以从设备的 `logcat` 输出中获取这个日志。

### 实时解析

如果你想要实时地从 `adb logcat` 解析崩溃日志，可以使用管道（pipe）将 `logcat` 的输出直接传递给 `ndk-stack`：

```sh
adb logcat | ndk-stack -sym <path-to-unstripped-libs>
```

这个命令会启动 `logcat` 并实时显示日志输出，同时 `ndk-stack` 会读取这些输出并将崩溃相关的地址符号化。

### 注意事项

- 确保你使用的是与崩溃时应用程序相匹配的未剥离的二进制文件。如果版本不匹配，符号化的输出可能是不准确的。
- `ndk-stack` 只能解析由 NDK 编译的原生代码崩溃。对于 Java 层的崩溃，你需要使用其他工具，如 Android Studio 或 `logcat`。

`ndk-stack` 是一个非常有用的工具，它可以大大简化 Android 原生代码崩溃分析的过程。通过将内存地址映射到源代码中的具体位置，开发者可以更快地定位和修复崩溃的原因。

## addr2line

`addr2line` 是 GNU Binutils 包中的一个工具，它用于将程序的地址转换为源代码中的文件名和行号。这个工具在分析程序崩溃时特别有用，因为它可以帮助开发者从崩溃日志中的地址信息定位到源代码的具体位置。

### 核心用法

要使用 `addr2line`，你需要提供程序的地址和包含调试信息的二进制文件（通常是未剥离的可执行文件或共享库）。以下是 `addr2line` 的基本用法：

```sh
addr2line -e <executable-or-library> <address>
```

- `-e <executable-or-library>`：这个选项后面跟的是包含调试信息的二进制文件的路径。这个文件用于查找地址对应的源代码位置。

- `<address>`：这是你想要转换的内存地址。这个地址通常来自于程序的崩溃日志或者堆栈跟踪。

### 解析多个地址

如果你有多个地址需要解析，可以将它们一起传递给 `addr2line`，每个地址占一行：

```sh
addr2line -e <executable-or-library> <address1> <address2> <address3>
```

或者，你可以将地址列表保存到一个文件中，然后使用输入重定向：

```sh
addr2line -e <executable-or-library> < addresses.txt
```

### 显示函数名

```sh
addr2line -f -e <executable-or-library> <address>
```

使用 `-f` 或 `--functions` 选项可以显示地址对应的函数名，这有助于更好地理解崩溃的上下文。

### 解码（Demangle）C++ 符号名称

```sh
addr2line -C -f -e <executable-or-library> <address>
```

使用 `-C` 或 `--demangle` 选项可以解码（demangle）C++ 符号名称，使得它们更易于阅读。

### 注意事项

- 确保你使用的是与崩溃时应用程序相匹配的未剥离的二进制文件。如果版本不匹配，`addr2line` 的输出可能是不准确的。
- `addr2line` 默认假设地址是相对于可执行文件或库的基地址的。如果你的地址是从共享库中获取的，你可能需要计算库被加载时的基地址偏移。

`addr2line` 是一个非常有用的工具，它可以帮助开发者快速从程序的地址信息定位到源代码的具体位置，从而加速调试和问题解决的过程。
