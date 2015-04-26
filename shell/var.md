#变量与运算

## 获取变量VAR的长度
${#VAR} 

## echo $line| awk –F’\t’ 达不到预期效果
需使用echo "$line” | awk –F’\t’ 

## 变量展开
   * ${param:+expr} 如果param设置并且不为空，展开expr
   * URL=${URL:-http://localhost:8080} 如果URL没有设置则设置为http://localhost:8080

## 检查一个变量是否存在
   * ${name:?error message}
   * 如果一个bash的脚本需要一个参数，也许就是这样一个表达式 input_file=${$1:?usage: $0 input_file}。

## 截取字符串
   * `${var%suffix}`   
   * `${var#prefix}`   
   示例：
```bash
if var=foo.pdf
then 
echo ${var%.pdf}.txt # 输出 foo.txt
fi
```

## 删除字符串中的第一个或者最后一个字符
```bash
$ str="aremoveb"
$ echo "${str#?}"
removeb
$ echo "${str%?}"
aremove
$ echo "${str%??}"
aremov
$ echo "${str:1:-1}"
remove
```
关于变量替换的内容参见 man bash

## 删除环境变量
`unset LD_TRACE_LOADED_OBJECTS`

##命令提示符
PS1环境变量


## 数字运算
   * let
```bash
n1=1
n2=2
let n3=n1+n2
let n1++
```
       **备注** 
      * 变量前无 $
      * \+ += ++等前后不能有空格

   * [ ]
```bash
n3=$[ n1+n2]
n3=$[$n1+n2]
```
   * (( )) 
      * 与[ ]类似
   * expr
```bash
n3=`expr $n1 + $n2`
```
      **备注**  
      * 变量前使用$
      * \+ 前后要有空格

前几种方式只能用于整数

   * bc
```bash
echo "$n1+$n2" | bc
```

## crontab与环境变量
Unix/Linux下使用crontab时的运行环境已经不是用户环境了，因此原本用户下的一些环境变量的设置就失效了。
因此，可以在crontab运行的脚本中设置环境变量或执行*rc等配置脚本，或者使用全路径等。