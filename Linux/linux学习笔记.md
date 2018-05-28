### Linux命令笔记
---
- **free** : 查看系统运行内存的使用情况，使用 `-h` 参数提升可读性。
- **df** : 查看硬盘的内存使用情况，使用 `-h` 参数提升可读性。
- **tar** : 根据参数实现解压或者压缩文件的功能
     >  **-zxvf** ：解压。  
     >  **-zcvf** ：压缩。
- **pwd** : 查看当前运行的路径。
- **rm** : 删除文件，使用 `-r` 参数实现递归删除。
- **sudo passwd root** : 此命令修改root用户的密码。
- **dpkg** : 软件包管理命令。
- **cp** : 拷贝文件到制定位置，使用 `-R` 参数实现递归操作。
- **readelf -h** : 查看 `elf` 类型文件的 `head` 信息。
- **top** : 查看各个程序的内存占用和 cpu 使用情况。
- **echo** : 可用于查看变量，`echo ${PATH}` 可以查看环境变量。
> -e : 换行符有效。  
- **tail** : 查看文件最后部分内容。使用 `-f` 参数实时查看文件内容。
- **less** : 查看文件，内容过多时自动实现分页。
- **strace** : 跟踪命令的执行过程，可用于命令执行的调试和排错。
    > **-f** : fork的子进程也进行跟踪。  
    > **-F** : vfork的子进程也进行跟踪。  
    > **-o [文件名称]** : 输出日志到指定文件中。  
    > **-p [进程id]** : 输出指定进程的调用情况。    
- **history** : 查看历史命令。    
- **w** : 查看登录了当前设备的用户。
- **last** : 查看登录过当前设备的用户详情。
- **du** : 查看文件或文件夹的大小。
> -s : 表示只计算指定的文件/文件夹大小。  
> -h : 使用更容易阅读的大小单位显示。    
> --max-depth = [n] : 设置计算文件夹大小时的遍历深度。    
> -X [*.jpg] : 根据匹配规则过滤文件。
- **fcitx-diagnose** : 检查输入法的状态。
- **uname -a** : 查看系统内核版本等信息。
- **lsb_release -a** : 查看系统发行商。
- **convert [fileName] -crop width x height + left + top [output]** : 裁剪图片命令。
- **for [item] in [Array] ; do ... done** : for 循环遍历数组，用于 bash 脚本，可遍历 `ls [dir]` 输出的文件名。
例 :
```bash
for fileName in `ls ./`
do
echo "文件名 :  ${fileName} , 无后缀 :  ${fileName%.*} , 文件类型 :  ${fileName##*.}"
convert "imgsrc/${fileName}" -crop 512x512+0+0 "imgdist/${fileName%.*}_00.${fileName##*.}"
done
```
- **sed 's///g' [fileName]** : 非交互的文件内容修改命令。结合 `for ... in ` 使用，可以批量修改文件或者合并多个文件。
> -e : 指定要执行的动作，可链接多个动作
```bash
# 去除最后一行的最后一个逗号
sed -e '$s/,$//' 
# 每一行的行首加双引号
sed -e 's/^/"/g'
# 每一行的行尾加双引号
sed -e 's/.$/"/g'
```
> -i 参数表示直接修改原文件内容。
例 :
```bash
for fileName in $(ls transform*)
do
# 使用 > 表示覆盖式写入文件， >> 则表示追加写入文件。
echo 'start' >> result.txt
sed 's/[\r ]/,/g' ${fileName} >> result.txt
echo 'end' >> result.txt
echo ${fileName%.*}' transform complete'
done
```
- **for i in {1..100..2};do ... done** : 表示 `for` 循环从 1~100，每次 +2。注意：大括号的数组扩展，必须使用 bash 命令执行。
- **$(ls [dirName])** : 使用 `()` 可以将命令执行完后再输出。
- **>> 和 >** : 可以将输出的内容写入到指定的文件当中，单个为覆盖写入，两个为追加写入。
- **=** : 等号用于给变量赋值，但 **左右两边不可以有空格**。
- **$1** : 在脚本当中表示第一个参数，其它参数以此类推。
- **$#** : 表示参数的总数。
- **$@** : 表示所有参数，通过 `for param in $@` 可以遍历命令的所有参数。
- **date** : 命令获取时间。
- **if [ statement ] then ... else ... fi** : 条件控制语句，这里的`statement` 表示语句的执行结果，为 `0` 表示执行成功，其它则表示执行失败。注意： `[]` 和 `statement` 之间必须有空格，否则命令会有异常。
```bash
if [ -e fileName ] : // 文件是否存在
if [ -d fileName ] : // 存在且为目录
if [ numA -ne numB ] : // 数字是否不等，注意数字不能使用 == 
if [ numA -eq numB ] : // 数字是否相等
if [ numA -lt numB ] : // 小于
if [ numA -gt numB ] : // 大于
if [ -z string ] : // 字符串长度为零
if [ -n string ] : // 字符串长度非零
if [ stringA == stringB ] : // 字符串是否相同
```
- **curl "地址字符串"** : 使用`curl`下载指定资源。
> -o [输出文件名] ：可以指定下载的文件名称。
> -O : 保持文件名不变。
- **wget** : 下载指定路径的文件。 
- **exit** : 退出脚本。
- **mkdir** : 创建文件夹     
> -p : 当父目录不存在，则创建父目录
- **grep -v [string]** : -v 表示不包含指定内容
