### 大体流程
MINIT -> RINIT -> SCRIPT -> RSHUTDOWN -> MSHUTDOWN  
模块初始化->请求初始化->处理具体的业务：使用execute()执行op_array里的中间代码opcodes->关闭请求->关闭模块

### 主体流程
启动代码在sapi/cli/php_cli.c中  
代码从main函数开始执行  
主体运行流程：  
  1. 填充sapi模块的结构  
  2. 启动sapi，进行sapi的一些全局设置  
  3. 运行sapi模块的startup，对各种模块，扩展，资源进行注册和初始化（register、init）  
  4. 初始化请求  
  5. 编译php文件，然后把编译后的opcodes执行  
  6. 请求关闭及释放的相关工作  
  7. 相关的各种模块的关闭及释放  
  8. 关闭sapi相关资源sapi_shutdown

### php程序的编译
程序的编译包含这一系列过程：词法分析、语法分析、语义分析、中间代码生成（前面三步的作用是分析源程序）、代码优化、目标代码生成（前面三步的作用是构成目标程序）  
php没有后面三步，所以**PHP是解释类语言**，它生成的opcode，这只是php的一种内部数据结构（struct）。
#### 总体流程  
1. Scanning：Lexing，将PHP代码转换为语言片段（Tokens）  
注意：这里用token_get_all函数可查看php程序转换成的语言片段  
2. Parsing：将Token转换成简单而有意义的表达式  
Parsing首先会丢弃Tokens Array中的多余的空格，然后将剩余的Tokens转换成一个一个简单的表达式  
3. Compilation：将表达式编译成opcodes  
将Tokens编译成一个个op_array（一种结构体）
4. Execution：顺次执行opcodes，从而实现PHP脚本的功能。