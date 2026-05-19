---
source: youdao-note
youdao_id: WEB7ec91c66bc0135343c7393f3fe19bb9f
title: rust-mobile知识.note
captured: 2026-05-15
status: pending-review
---

cdylib 
是 Rust 编程语言中的一个 crate 类型，用于构建动态链接库（Dynamic Link Library，DLL）。
在 Rust 中，crate 是一个独立的模块单元，可以包含一组相关的代码、数据结构和功能。crate 可以是二进制可执行文件（executable）、库（library）或测试（test）等不同类型。
而 cdylib 则是一种特殊类型的库 crate，它用于构建动态链接库，也称为共享库（shared library）或动态库（dynamic library）。动态链接库是一种编译后的代码和数据的集合，可以在运行时被加载和使用，与静态链接库（static library）相对应。
使用 cdylib crate 类型可以将 Rust 代码编译为动态链接库，以供其他编程语言或系统使用。
这种动态链接库可以被其他编程语言调用和加载，实现跨语言的交互和共享功能。
在 Rust 中，使用 cdylib crate 类型可以通过 cargo 构建工具来构建动态链接库。
在 Cargo.toml 文件中设置 crate-type = ["cdylib"]，然后使用 cargo build 命令编译生成动态链接库。
例如，以下是一个简单的 cdylib crate 的示例：
// src/lib.rs#[no_mangle]pub extern "C" fn add(a: i32, b: i32) -> i32 {    a + b}
在这个示例中，我们定义了一个名为 add 的函数，它将两个 i32 类型的参数相加并返回结果。
#[no_mangle] 属性用于确保函数的名称在编译后保持不变，以便其他语言可以正确调用。
接下来，我们可以在 Cargo.toml 文件中将 crate 类型设置为 cdylib：
[package]name = "my_lib"version = "0.1.0"edition = "2021"[lib]crate-type = ["cdylib"][dependencies]
然后，使用 cargo build 命令构建动态链接库。
构建完成后，我们就可以将生成的动态链接库（如 .dll 文件）提供给其他编程语言使用，比如 C、C++、Python 等，以实现跨语言的交互和共享功能。
总结来说，cdylib 是 Rust 中用于构建动态链接库的一种 crate 类型，可以将 Rust 代码编译为可供其他编程语言调用和加载的动态链接库。
onCreate 是 
Android 应用开发中一个常见的生命周期回调方法，它是 Android Activity 或 Fragment 生命周期中的一个重要方法。
在 Android 中，onCreate 方法是在 Activity 或 Fragment 创建时被调用的，用于进行一些初始化操作和准备工作。它是在组件创建后但在用户可见之前被调用。
对于 Activity，onCreate 方法通常用于执行以下任务：
设置布局：在 onCreate 方法中，可以通过调用 setContentView 方法来设置 Activity 的布局，即指定显示的界面。
初始化变量和对象：在 onCreate 方法中，可以进行变量和对象的初始化操作。例如，可以创建和初始化 UI 控件、数据结构、适配器等。
绑定事件监听器：在 onCreate 方法中，可以为 UI 控件或其他对象绑定事件监听器，以响应用户的交互操作。
获取传递的数据：onCreate 方法可以接收 Intent 对象，并从中获取传递的数据，例如通过 getIntent().getStringExtra() 获取传递的字符串参数。
对于 Fragment，onCreate 方法的功能与 Activity 类似，但在使用上略有差异。在 Fragment 中，onCreate 方法通常用于执行以下任务：
初始化变量和对象：与 Activity 类似，可以在 
onCreate 方法中进行变量和对象的初始化操作。
设置布局（可选）：Fragment 可以选择在 
onCreateView 方法中设置布局，而不是在 onCreate 方法中。
获取传递的数据：与 Activity 类似，可以通过 
getArguments() 方法获取传递给 Fragment 的参数数据。
需要注意的是，onCreate 方法是生命周期的一部分，它在组件的创建阶段被调用。在 onCreate 方法执行完成后，系统会调用其他生命周期方法，如 onStart、onResume（对于 Activity）或 onViewCreated（对于 Fragment）等。
总结来说，onCreate 是 Android 应用开发中的一个生命周期回调方法，用于在 Activity 或 Fragment 创建时执行一些初始化和准备工作。它常用于设置布局、初始化变量和对象，以及获取传递的数据等任务。

