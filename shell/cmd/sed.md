# sed

## 描述

sed是一个很好的文件处理工具，本身是一个管道命令，主要是以行为单位进行处理，可以将数据行进行替换、删除、新增、选取等特定工作.

sed是非交互式的编辑器.它不会修改文件，除非使用shell重定向来保存结果.默认情况下，所有的输出行都被打印到屏幕上.

sed编辑器逐行处理文件（或输入），并将结果发送到屏幕.具体过程如下：首先sed把当前正在处理的行保存在一个临时缓存区中（也称为模式空间），然后处理临时缓冲区中的行，完成后把该行发送到屏幕上.sed每处理完一行就将其从临时缓冲区删除，然后将下一行读入，进行处理和显示.处理完输入文件的最后一行后，sed便结束运行.sed把每一行都存在临时缓冲区中，对这个副本进行编辑，所以不会修改原文件.

## 语法格式

```
sed [OPTIONS] [FILE...]
```
将多个命令合并使用,使用分号分隔

## 选项

- -d : 删除，删除选择的行
- -e ∶ 直接在指令列模式上进行 sed 的动作编辑；
- - i : 在行首插入内容
- - a : 在行末追加文本
- - c : 替换行
- -f ∶ 直接将 sed 的动作写在一个档案内， -f filename 则可以执行 filename 内的sed 动作；
- -i ∶ 直接修改读取的档案内容，而不在屏幕输出
- -n ∶ 使用安静(silent)模式。在一般 sed 的用法中，所有来自 STDIN的资料一般都会被列出到萤幕上。但如果加上 -n 参数后，则只有经过sed 特殊处理的那一行(或者动作)才会被列出来。
- -r ∶ sed 的动作支援的是延伸型正规表示法的语法.(预设是基础正规表示法语法)
- -= : 打印当前行号码

sed 's/要替换的字符串/新的字符串/g'（要替换的字符串可以用正则表达式）,末端的g表示在行内进行全局替换.替换时sed默认使用反斜杠（/）分割,紧跟在s命令后的字符就是查找串和替换串之间的分隔符.分隔符默认为正斜杠，但可以改变。无论什么字符（换行符、反斜线除外），只要紧跟s命令，就成了新的串分隔符.

参考:
- [sed命令详解](http://www.cnblogs.com/edwardlost/archive/2010/09/17/1829145.html)

## 例
```
$ sed -i "s:/static:/blog/static:" `grep /static -rl ./` # 检索当前目录下的文件,将其包含的字符串"/static"替换为"/blog/static".
$ sed -i  "s:"action='"'":"action='"'/blog":" `grep action= -rl ./` 将`action="/comment/{{.Content.Id}}/"`替换为`action="/blog/comment/{{.Content.Id}}/"`
$ sed -i '1,nd' 2016.txt # 删除前n行
$ sed 's/text/replace_text/' file  # 替换每一行的第一处匹配的text
$ sed 's/text/replace_text/g' file  # 全局替换
$ sed '/^$/d' file # 移除空白行
$ sed '/qq/d' file # 移除包含"qq"的行
$ echo this is en example | sed 's/\w+/[&]/g' # 已匹配的字符串通过标记&来引用
$ p=patten
$ r=replaced
$ echo "line con a patten" | sed "s/$p/$r/g" # 双引号会对表达式求值
$ sed -n '2,6p' access.log # 输出指定行(2~6)
$ sed -e 'i\head' access.log # 在每行的前面插入字符串"head"
$ sed -e 'a\end' access.log # 在每行的后面追加字符串"end"
$ sed -e '/google/c\hello' access.log # 将包含"google"的行替换成字符串"hello"
$ sed -n '1,5p;1,5=' access.log # 显示1~5行,并在结果的1~5行上添加行号
```
