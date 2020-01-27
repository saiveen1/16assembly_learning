## assembly
汇编语言学习中的写下的代码

### 4asm
	inc用法
	[BX]使用
	1.18.2.02
		line 21
			+ codesg ends
			+ mov ax,4c00h
			+int 21h
			
### 5asm
	loop用法
		1.18.17.36
			line 18
				start end----end start

### 6asm
	loop用法2
		1.18.18.04
			line 3
				codesg end:-----codesg end
				
### 7asm
	loop用法3
		
### 8asm
	loop用法4 
	将内存FFFF:0 B中的数据拷贝到0:200 20B中
		改进版使用es段寄存器存放另一组数据 同ds
			
			MOV AX,0FFFFH
			MOV DS,AX
			MOV AX,0020H
			MOV ES,AX
			MOV BX,0
			MOV CX,12
		S:
			MOV DL,[BX]
			MOV ES:[BX],DL
			INC BX
			LOOPS
			
### 9asm
	9条指令包含结束指令 向内存0:200-0:23F依次写入0-3fh(64)
		
		1 没有用cx控制循环次数 mov cx,63
		2 忘记结束语句
			MOV AX,4C00H
			INT 21H
		3 并没有达到要求9行指令 多了一行 百思不得其解	
	作为第一次自己写的 属实不太行 这还是建立在抄了8次代码的基础上
	
	错误代码如下
		assume cs:cdsg

		cdsg segment

		start:
			mov ax,0
			mov ds,ax
			mov bx,200h
			mov cx,64
			
		s:
			mov [bx],ax
			inc ax
			inc bx
			loop s

			mov ax,4c00h
			int 21h
			
		cdsg ends

		end start


### 10asm
	4c00h之前的指令复制到内存中

### 11asm
	计算存储在cs中8个数据的和 结果放在ax寄存器中

### 12asm
	利用栈逆序存放存储在cs段中的数据
	
### 13asm
	熟悉强化segment 栈指令
		cpu执行程序 程序返回前 data中的的数据为多少
			0123 .....
		
		cpu执行程序 程序返回前 cs ss ds分别为多少
			04B2 04B1 04B0
		
		程序加载后 code段地址为x data段 stack段地址分别为多少
			X-2 X-1
		
### 14asm
	和上一题一样 目前并不清楚有什么作用 只是8个数据变成两个
		cpu执行程序 程序返回前 data中的的数据为多少
			0123 .....
		
		cpu执行程序 程序返回前 cs ss ds分别为多少
			04B2 04B1 04B0
		
		程序加载后 code段地址为x data段 stack段地址分别为多少
			X-2 X-1
			
		对于定义如下的段：
			NAME SEGMENT
				...
			NAME ENDS
		如果段中的数据占N个字节 程序加载后 该段实际占有的空间为
			16*（n/16 + 1）

### 15asm
	将定义数据段和栈段放在代码段之后 观察地址变化
		cpu执行程序 程序返回前 data中的的数据为多少
			0123 .....
		
		cpu执行程序 程序返回前 cs ss ds分别为多少
			04B0 04B4 04B3
				这里先设的data段所以data在前 但是04B1到哪里了呢
		
		程序加载后 code段地址为x data段 stack段地址分别为多少
			x+3	x+4
		
		如果上述三题最后一条伪指令END START改为 END
			即不指名程序入口 那么哪一个程序可以正确执行
				是15asm 因为根据段如12asm的使用 不指名数据段 栈段的话
				相应的地址被放到了cs段中 那么程序自然不会正常执行
	
	ps 14 15均未实际操作
	
### 16asm
	编写code段中代码 将a b段中的数据依次相加 将结果存到c段

### 17asm
	用push指令将a段中前8个字型数据 逆序存储到b段
			
### 18asm
	将uNiX全部转换为大写

### 19asm
	将datasg段中每个单词的头一个字母改为大写
	
### 20asm
	将datasg段中每个单词改为大写

### 21ASM
	将datasg段中每个单词的前四个字母改为大写
		嵌套循环

### 22ASM
	用div计算data段中读一个数据除以第二个数据后的商
	存放在第三个数据的存储单元
			
### 23asm
	实验7 寻址在结构化数据中的应用
			
### 24asm
	实验8 一个奇怪的程序

### 25asm 
	实验9 屏幕中间分别显示绿 绿底红 白底蓝的字符串'WELCOME TO MASM！'
	
### 26asm
	检测点10.5
		call offset 的应用回顾

### 27asm
	实验10 1
		把显存显示实现为一个接口 以8行三列绿色为例子