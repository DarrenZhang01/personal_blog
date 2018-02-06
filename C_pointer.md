C语言指针(pointer)是C语言不同于其他编程语言的一大特性，它在进行参数传递、参数修改起着重要的作用。当我们在使用指针指代字符串字面量(string literal, 注意不是string, C语言中没有string这种类型)时， 常常会与字符数组(char array)混淆。这两者之间究竟有什么共同和不同之处，我会根据我学习C语言的一点心得举例并加以总结，不足之处请多多指教

首先回顾一下C语言的内存机制(memory model):
||
| :-: |
| Code |
| Global Variable |
|Stack|
|Constant|
|Heap|
|Operating System|

**先说指针的声明，假设现在有赋值语句如下(Assignment Statement)**
```
char *a = "this is a string literal!";
```
我们初始化了一个(char \*) 类型的变量a，等号右边的是一个字符串字面量， 它实际存在于memory model 中的Constant 模块，是只读的；当执行如上赋值语句时，在内存里发生的事情就是， a会被在stack里分配一块char \*大小的空间（通常是4或8字节）用于存放a指向的地址；而这个字面量的起始地址，也就是字符 't' 的位置，被赋给了变量(char *)a。因为这是一个字符串字面量，所以默认在其结尾处有一个结束符(NULL terminator)来代表它的结束。所以，假设t的地址是0x400，那么如果我们现在做 “a == 0x400” 的测试，结果应该返回的是 1。

**来看字符数组的声明(char array)**
```
char b[] = "another string literal!";
```
在以上过程中，another string literal!被储存在Constant module中。当我们声明字符数组b时，栈stack开辟一块儿空间复制constant string literal中的每一个字符到b数组对应的index中（包括null terminator），作为对数组b的初始化（initialization）

注意，如果我们不指明数组的大小(size)，系统就会按照strlen(string_literal) + 1自动在栈stack内分配空间，不需要手动添加null terminator，因为string literal自带null terminator('\0')。但如果你更改了字符数组中的字符使b表示新的字符串，不要忘记手动更改null terminator的位置，否则会导致垃圾的出现


###两者的共同点：
数组和指针均可用下标(index)来获取对应位置上的字符
```
printf("equal: %d\n", a[1] == 'h');
printf("equal: %d\n", b[0] == 'a');
```
两者均会打印出1
###不同点（！！！）：
**1.从内存的角度来说，最显著的区别，char array在栈stack内做了string literal的复制而char pointer没有**
**2.char array不可以做字符字面量的整体更改而char pointer可以轻松的更改**
```
a = "want to change and succeed!"
b = "want to change but fail!"
```
  a对，b错并且b会给出编译时错误(compile error)
**3. char pointer 不可通过下标index做某个字符的单独修改，因为constant module中的字符串字面量是只读的。但char array可以。简单的理解就是a的字符串还是别人的，你不能动，但是对b来说我已经有一份自己的字符串了，我想咋动咋动**
```
a[0] = 'b'; // Fail
b[0] = 'a'; // OK
```
a不会给出编译时错误compile error，但是运行时会给出run time error - bus error，因为我们试图去修改只读变量
**4.char pointer可以做指针运算(pointer arithmetic)，而char array不行**
```
a++; //OK
b++; //Fail
```
a的本质是一个指针，你可以任意改变它的位置通过改变它的数值，当我们做自增一运算的时候，指针会自动移动到constant module里string literal第二个字符的位置，也就是在原地址的基础上加一个char的size。而b的本质是一个数组，所以你不能随意更改b的指向。

