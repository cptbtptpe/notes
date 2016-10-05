
## Shell

- [x] \$\$ 
> Shell本身的PID（ProcessID） 

- [x] \$! 
> Shell最后运行的后台Process的PID 

- [x] \$? 
> 最后运行的命令的结束代码（返回值） 

- [x] \$- 
> 使用Set命令设定的Flag一览 

- [x] \$_
> 上一条执行的命令的参数部分

- [x] \$* 
> (命令行中)所有参数列表。如"\$*"用「"」括起来的情况、以"\$1 \$2 … \$n"的形式输出所有参数。 

- [x] \$@ 
> (命令行中)所有参数列表。如"\$@"用「"」括起来的情况、以"\$1" "\$2" … "\$n" 的形式输出所有参数。 

- [x] \$# 
> (命令行中)添加到Shell的参数个数 

- [x] \$0 
> (命令行中)Shell本身的文件名 

- [x] \$1～\$n 
> (命令行中)添加到Shell的各参数值。\$1是第1参数、\$2是第2参数…。 

- [x] result=\$(ls)
> 将括号中的表达式以命令方式执行并把结果赋值给变量result

- [x] result=\${abc}
> {}中的将和\$合并解析成变量，同 result="\$abc"

- [x] result=\$((\$a + \$b))
> 计算变量a和变量b的和，同 result=\$[\$a + \$b]、result=\$(expr \$a + \$b)

- [x] 动态获取变量
> abhehe=hello world
c=hehe
varName=abc\${c}
echo \${!varName}  # hello world

- [x] 动态定义变量
> c=hehe
declare -r \$c='hello world'
echo \${hehe} # hello world

- [x] 动态定义数组变量
> a=arr
declare -a arr
((\$a[1]=111))
((\$a[2]=222))
echo \${arr[1]} # 111
echo \${arr[2]} # 222

- [x] 获取字符串的长度
> str=helloworld
echo \${#str}

- [x] 获取数组的长度
> arr=("a" "b" "c")
echo \${#arr[@]}

- [x] 双小括号表达式 (())
> 所有表达式可以像c语言一样，如：a++,b--,c+=1等
所有变量可以不加入\$符号进行调用
可以进行逻辑运算，四则运算
扩展了for,while,if条件测试运算
支持多个表达式运算，各个表达式之间用逗号分开
d=\$((1,2,3,4,5)) \$d的值为最后一个表达式的值
