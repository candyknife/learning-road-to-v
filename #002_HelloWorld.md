# 1.2 Hello World

## 1.2.1 第一个程序

    fn main() {
        println('hello world')
    }

将这段代码保存在一个文件中并命名为 `hello.v`。并且在终端中运行 `v run hello.v`。

> 此处默认你已经将 V 添加到环境目录中。如果没有，参考上一节。

恭喜！你刚刚已经编写运行了你的第一个 V 程序！

你也可以仅仅通过 `v hello.v` 来仅仅编译但不执行你的程序。其他更多支持的命令可以通过 `v help` 查看。

通过上面的例子，你可以看到函数是通过 `fn` 关键字来声明的。函数返回值的类型会紧跟在函数名后面具体写出。这个例子里的 `main` 函数不返回任何值，所以没有写出返回值类型。

就像许多其他编程语言一样（例如 C, Go 以及 Rust），`main` 是你整个程序的入口。

`println` 是一个内置函数。它会将传递给它的值打印出来。

`fn main` 声明在单文件程序中可以跳过。这在编写一些“脚本”类的小程序或者在学习这门语言的过程中很有用。出于简洁，`fn main` 在整个文档中都会略过不写。

因此上面的“Hello World”代码在 V 中实际上可以像如下一样简洁：

    println('hello world')

## 1.2.2 运行有多个文件的软件工程

假定你有一个有很多 .v 文件的文件夹，并且里面其中一个文件包括 `main` 函数，其他文件包括一些需要的函数。它们也许各自是按某种主题组织的，但结构又不足以分别成为独立的可复用的模块，这样的情况下你想将它们都编译进一个程序里。

在其他语言中，你也许得用 includes 或者 build 系统去
遍历所有文件，并将它们分别编译成 .o 文件，最后再将它们链接成一个最终的可执行文件。

但在 V 中，你可以仅仅用 `v run .` 将整个文件夹中的所有 .v 文件一起编译运行。于此同时你还可以传递你自己的参数：

    v run . --yourparam some_other_stuff

上面这行代码首先将你的所有文件编译成一个程序（按你的文件夹/工程名命名），然后将 `--yourparam some_other_stuff` 作为参数在程序执行时传入。

你的程序可以像这样使用 CLI 参数：

    import os

    println(os.args)

> 注意：编译完成的程序成功运行后，会被 V 自动删除。如果你想保留，使用 `v -keepc run .` 命令，或者用 `v .` 手动编译再手动运行。

> 注意：任何 V 编译器标志都应该在 `run` 命令之前传递。所有跟在源文件/目录后的内容都将原样传递而不被 V 编译器做任何处理。

## 1.2.3 注释

    // This is a single line comment.
    /*
    This is a multiline comment.
    /* It can be nested. */
    */

## 1.2.4 函数初识

    fn main() {
        println(add(77, 33))
        println(sub(100, 50))
    }

    fn add(x int, y int) int {
        return x + y
    }

    fn sub(x int, y int) int {
        return x - y
    }

再一次提醒，变量的类型跟在变量名之后。

就像 Go 和 C 一样，函数不能重载。这简化了代码，提高了可维护性和可读性。

### Hoistings

函数是可以在声明前就调用的：`add` 与 `sub` 都在 `main` 之后声明，但仍然可以在 `main` 中调用。这一点对 V 中的所有声明都成立，于是你不需要头文件或者考虑文件与声明的顺序。

### 返回多个变量

    fn foo() (int, int) {
        return 2, 3
    }

    a, b := foo()
    println(a) // 2
    println(b) // 3
    c, _ := foo() // ignore values using `_`

### 外部可见标志

    pub fn public_function() {
    }

    fn private_function() {
    }

函数都是默认私有的（不能被其他文件调用）。想让别的模块去调用，在函数前面加上 `pub`。对于其他常量与类型来说也是如此。

> 注意：`pub` 只能从一个已命名的模块中被调用。模块相关的内容参考xxx

