---
title: MATLAB Coding style
date: 2021-07-17 19:02:02
tags: MATLAB
---

# MATLAB 编程风格指南

如何写出整洁、干净、可读性高的MATLAB代码，这是一个从开始就必须认真思考的问题，干净整洁的代码风格可以帮助我们更好的维护、理解、共享，同时它也更加容易调试与修改，也伴随着更少的错误。

作为一个从事于工程领域的学生，MATLAB软件是科研生活中不可缺少的计算软件，但是由于MATLAB是面向过程的编程语言，在编写代码的过程中，有些时候为了方便而产生的变量会使整个程序变得混乱，不适当的编写代码块也使得代码的可读性变得很差，尤其是做大型计算的时候，有时候因为代码过于混乱在调用前面变量时会出现错误。所以对于一些大型的计算程序，干净整洁可读性强的代码风格是很重要的。

本文列举了一些比较通用实践效果较好的代码风格建议。:bowtie:



## 1 命名规则

### 变量

变量的命名必须记录变量的用途以及意义，增加代码的可读性，以便后续对代码的维护。

在这个地方推荐**CODELF**，在你不知道为变量命名的时候，可以在这个网站进行搜索，可以找到适合变量的命名

**CODEDL**：[root - CODELF (unbug.github.io)](https://unbug.github.io/codelf/#root)

其他要求：

1. 变量名必须以小写开头，大小写混合组合；其次可以用下划线分割复合变量名的各个部分（注意在**MATLAB**图例变量中下划线 _ 会被读取为下标切换）

   ```matlab
   linearity, credibleThreat, qualityOfLife
   linearity, credible_Threat, quality_Of_Life
   ```

2. 作用域较大的变量必须具有有意义的名称，作用域范围小的变量可以拥有较短的名称，比如整数的临时变量：

   ```matlab
   i, j, k, m, n, x, y, z
   ```

3. 前缀**n**通常用来表示对象的数量，而在**MATLAB**中也用**m**表示行数，例如：

   ```matlab
   nFiles, n_element, mRows
   ```

4. 将所有变量名设为单数或者复数，如果为了避免单数复数只有最后的后缀s不同而难以分辨，可以采用后缀**Array**来表示复数：

   ```matlab
   points, point, pointArray
   ```

5. 表示单个临时变量可以以**i**为前缀：

   ```matlab
   iPoint, iTable
   ```

6. 迭代器的临时变量应该用**i，j，k**命名：

   ```matlab
   for iPoint = 1:nPoint
   :
   end
   ```

7. **bool**变量应加上**is**或者**not**的前缀：

   ```matlab
   isAnimal, notAnimal
   ```

8. 首字母缩略词，即使其通常采用大写表示，在变量命名时也该使用小写：

   ```matlab
   html
   ```

9. 避免使用关键词或者特殊名称作为变量名。



合适的变量名称是程序可读性高的基础。



### 常数

常数的命名比较特殊，应该遵循以下两个原则：

1. 命名常量应该全部使用大写字母，且使用下划线进行语义分割。

   ```matlab
   MAX_PATH_LENGTH
   ```

2. 尽量使用较多的信息说明常量的意义。

   ```matlab
   COLOR_RED
   ```



### 结构体（类）

1. 类的名称应该用大写开头，来区别于变量。

   ```matlab
   Dense, Model
   ```

2. 类的名称不应该被包含在类的成员里面。

   ```matlab
   Model.layer
   ```



### 函数

函数的名称应该含有自身用途的信息。

1. 函数名应该全部使用小写字母。

   ```matlab
   call, compute
   ```

2. 函数名必须是有意义的名字。

   ```matlab
   plotpoint， maxlen
   ```

3. 如果函数只有一个单个的输出，可以用输出参数命名。

4. 没有输出参数的函数应该用函数的用途进行命名。

5. 前缀**get、set**通常保留用于访问后者设置对象的属性。

   ```matlab
   getobj(), get_length
   ```

6. 前缀**compute**也常被用于函数的命名当中。

   ```matlab
   computeweight()
   computespread()
   ```

7. 前缀**find**通常被用于查找类函数的命名当中。

   ```matlab
   findmaxlength()
   ```

8. 前缀**initialize**被用于对象或者概念被建立和初始化参数时。

   ```matlab
   initializebias
   ```

9. 前缀**is**通常被用于**bool**函数。

10. 避免出现相同的函数名称，这样在调用函数的时候会出现错误。



### 通用规则

1. 变量和常量的名称通常带有表示单复数的后缀。
2. 避免命名中的缩写，除非是人尽皆知的缩写，后期检查不利于维护代码。
3. 所有的命名都应该使用英文。



## 2 文件和结构

在文件之间和文件内的代码构建十分重要，对于后期维护和理解代码有着很大的帮助，对代码的分区与排序是关键。



### M文件

1. 模块化，编写大程序的最佳方法就是将设计好的小模块组装起来， 这样可以减少查看代码正在做什么时候的代码阅读量。长度超过两个编辑器屏幕的代码最好进行分区处理。

   ```matlab
   %% 分区 1
   code
   
   %% 分区 2
   code
   ```

2. 函数交互清晰明确，函数通过输入和输出与其他代码进行交互， 尽量避免使用全局变量或者非常多的输入参数。

3. 分区，所有的子函数和函数只需要解决一个问题，避免一个体量庞大的函数产生。

4. 尽可能使用已经建立好的函数，一个函数可以由多个子函数构成，所以开发一个正确且可读性高、灵活的函数是一项重要的任务。

5. 出现在多个**M**文件的代码块都应该被封装成为一个函数。

6. 子函数，仅由一个其他函数使用的函数应作为其子函数打包在同一文件中， 这使得代码更易于理解和维护。

7. 测试脚本，为每一个函数编写一个测试脚本。这种做法将提高代码的质量和更改版本的可靠性。



### 输出与输出文件

1. 制作输入输出模块， 提高代码的可维护性。
2. 格式化输出以方便使用。



## 3 声明



### 变量和常量

1. 除非内存限制需要，否则不应该重复使用变量， 通过确保唯一表示概念来提高代码的可读性， 从而减少因误解定义而出错的机会。

2. 可以在同一行声明相同类型的变量， 不应该在同一行中声明不相关的变量。

   ```matlab
   float x, y, z
   global LENGTH, MAX_POINT
   ```

3. 一定要在文件的开头附近注释重要变量的意义，包括输入输出参数。

4. 在变量声明的同一行末尾可以记录变量的意义。

   ```matalb
   THRESHOLD = 10;    % Maximum noise level found by experiment
   ```

   



### 全局声明

1. 应该尽可能地减少使用全局变量， 代码和程序的可维护性受益于参数的传递而不是过多的使用全局变量，一些全局变量可以用持久变量persistent代替。
2. 应尽可能减少使用全局常量，可以使用特定的M文件或者mat文件来定义常量的值，可以有效的避免无效定义。



### 循环

1. 循环变量应该在循环之前立即初始化，第一提高了循环的速度，第二防止循环索引出现错误。

   ```matlab
   for i = 1:1:n
   :
   end
   ```

2. 应该尽量减少在循环中使用**continue**和**break**，其可能会破坏程序的结构。

3. 在嵌套循环的结束行应该有注释，用来阐明哪些语句在哪些循环中执行了哪些任务。



### 条件

1. 应该避免复杂的条件表达式，而是使用临时的逻辑变量，更易于阅读或者调试。

   ```matlab
   isVaild = (value >= lowerLimit) & (value <= upperLimit);
   isNew = ~ismember(value, valueArray)
   if (isVaild & isNew)
   :
   end
   ```

2. 通常的情况应该放在if部分，而异常情况一般放在**if else**或者**else**部分，这种做法主要防止异常遮挡正常的程序执行路径。

3. 条件表达式 **if 0** 不应该被使用。

4. switch 语句应该包含其他条件，如果遗漏会导致意想不到的结果。

   ```matlab
   switch (condition):
   case A
   	statement;
   case B
   	statement;
   otherswise
   	statement;
   end
   ```

5. switch 变量通常为字符串，字符串在这种情况下表现得更好。



### 通用规则

1. 首先第一个，避免神秘代码，不要写自己接下来看不懂得代码，使得代码的可维护性变得很差，如果看不懂的代码也应该及时给予注释解释其含义。

2. 使用括号，虽然**MATLAB**有运算符优先级的判定，但是加上括号使得逻辑表达式更加清晰。

3. 尽量减少在表达式中使用数字， 可更改的数字通常应命名为常量，更改常量比更改文件中所有的相关的数字文本要容易很多。

4. 浮点数常量应该在小数点前写一个数字。

   ```matlab
   NUMBER = 0.5
   ```

5. 浮点数的比较大小应该慎重。



## 4 布局、注释、文档



### 布局

布局的目的是帮助读者阅读理解代码， 缩进特别有助于解释结构问题。

1. 每个文件的代码应保持在**80**列左右，**80** 列是编辑器、终端仿真器、打印机和调试器的通用尺寸，多人共享的文件应保持在这些限制范围内。如果在程序员之间传递文件时避免了无意的换行，则可读性会提高。

2. 行应该被点分开，一般而言，应在逗号或者空格后换行，或者运算符号后换行，新行与上一行表达式的开头对齐。

   ```matlab
   totalSum = a + b + c + ...
   		   d + e;
   fuction = (param1, param2, ...
              param3)
   ```

3. 基本的缩进应使用**Tab**进行缩进。

4. 一般来说一行语句只包含一个可执行语句。

5. 简单的单个语句**if**、**for**、或**while**语句可以写在一行上面。

   ```matlab 
   if (condition), statement; end
   while (condition), statement; end
   for i = 1:n, statement; end
   ```

   

### 空格

空格可以使语句看上去漂亮整齐可读性高。

1. 在运算符号前后都使用空格。

   ```matlab
   simpleAverage = (first + last) / 2
   ```

2. 在逗号后面可以使用空格。

3. 一行中多个命令的分号或者逗号应跟一个空格。

   ```matlab
   if (condition), statement; end
   ```

4. 关键词后面可以跟上一个空格， 可以帮助辨别函数的关键词。

5. 一个代码块内的逻辑语句应该用空行分割。

6. 在任何地方尽量使用对齐。

   ```matlab
   totalSum = a + b + c + ...
   		   d + e;
   fuction = (param1, param2, ...
              param3)
   ```



### 注释

注释的目的是向代码添加信息。注释的典型用途是解释用法、提供参考信息、证明决策的合理性、描述限制、提及需要的改进。经验表明，最好在编写代码的同时编写注释，而不是打算稍后添加注释。

1. 注释写的不好，代码也就不好。
2. 注释应与代码表达的意思一致，但不仅仅是重述代码。
3. 注释应该通俗易懂。
4. 注释通常与所引用的语句具有相同的缩进。
5. 函数开头的注释应该支持help和lookfor函数。
6. 函数开头注释应该讨论对输入参数的任何特殊要求。
7. 函数头注释应该描述任何作用。
8. 一般来说，最后一行函数头注释应该重述函数行，这允许用户浏览帮助打印输出并查看输入和输出参数用法。
9. 标题注释和其余注释之间应该有一个空行，这样它们就不会在响应帮助时显示出来。
10. 所有评论应以英文书写。



### 文档



1. README 文档，有用的文档应该包括对代码应该做什么（要求）、它如何工作（设计）、它依赖哪些功能以及它如何被其他代码使用（接口）以及它如何进行测试的可读描述.对于额外的信用，文档可以包括对替代解决方案的讨论以及扩展或维护的建议。
2. 考虑先编写文档，一些程序员认为最好的方法是“先编码，然后回答问题”。通过经验，我们大多数人了解到开发设计然后实施它会导致更令人满意的结果。开发项目几乎从未如期完成。如果将文档和测试留到最后，它们将被缩短。首先编写文档可确保完成并可能会减少开发时间。
3. 变化，管理和记录代码更改的专业方法是使用源代码控制工具。对于非常简单的项目，在函数文件中添加更改历史注释肯定比没有好。



<img src="MATLAB-Coding-style/1.jpg" alt="1" style="zoom:20%;" />









