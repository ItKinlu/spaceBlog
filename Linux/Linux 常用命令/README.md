# Linux 常用命令

- ls 命令

  > 就是 list 的缩写，通过 ls 命令不仅可以查看 linux 文件夹包含的文件，而且可以查看文件权限(包括目录、文件夹、文件权限)查看目录信息等等

  常用参数搭配：

  ```bash
    ls -a 列出目录所有文件，包含以.开始的隐藏文件
    ls -A 列出除.及..的其它文件
    ls -r 反序排列
    ls -t 以文件修改时间排序
    ls -S 以文件大小排序
    ls -h 以易读大小显示
    ls -l 除了文件名之外，还将文件的权限、所有者、文件大小等信息详细列出来
  ```

  实例：
  (1) 按易读方式按时间反序排序，并显示文件详细信息

  ```bash
  ls -lhrt
  ```

  (2) 按大小反序显示文件详细信息

  ```bash
  ls -lrS
  ```

  (3)列出当前目录中所有以`t`开头的目录的详细内容

  ```bash
  ls -l t*
  ```

  (4) 列出文件绝对路径（不包含隐藏文件）

  ```bash
  ls | sed "s:^:pwd/:"
  ```

  (5) 列出文件绝对路径（包含隐藏文件）

  ```bash
  find $pwd -maxdepth 1 | xargs ls -ld
  ```

- cd 命令

  > (changeDirectory),命令语法：cd [目录名]。说明：切换当前目录至 dirName

  实例：
  (1) 进入根目录

  ```bash
  cd /
  ```

  (2) 进入'家'目录

  ```bash
  cd ~
  ```

  (3) 进入上一次工作路径

  ```bash
  cd -
  ```

  (4) 把上个命令的参数作为 cd 参数使用。

  ```bash
  cd !$
  ```

- pwd 命令

  > 查看当前工作目录路径

  实例：
  (1) 查看当前路径

  ```bash
  pwd
  ```

  (2) 查看软链接的实际路径

  ```bash
  pwd -P
  ```

- mkdir 命令

  > 创建文件夹

  常用参数搭配

  ```bash
  mkdir -m 对新建目录设置存取权限,也可以用chmod命令设置
  mkdir -p: 可以是一个路径名称。此时若路径中的某些目录尚不存在,加上此选项后,系统将自动建立好那 些尚不在的目录,即一次可以建立多个目录;
  ```

  实例：
  (1) 当前工作目录下创建名为 t 的文件夹

  ```bash
  mkdir t
  ```

  (2) 在 tmp 目录下创建路径为 test/t1/t 的目录，若不存在，则创建

  ```bash
  mkdir -p /tmp/test/t1/t
  ```

- rm 命令

  > 删除一个目录中的一个或多个文件或目录，如果没有使用- r 选项，则 rm 不会删除目录。如果使用 rm 来删除文件，通常仍可以将该文件恢复原状 用法：`rm [选项] 文件…`

  实例：
  (1) 删除任何.log 文件；删除前逐一询问确认

  ```bash
  rm -i *.log
  ```

  (2) 删除 test 子目录及子目录中所有档案删除,并且不用一一确认

  ```bash
  rm -rf test
  ```

  (3) 删除以-f 开头的文件

  ```bash
  rm – -f*
  ```

- rmdir 命令

  > 从一个目录中删除一个或多个子目录项，删除某目录时也必须具有对其父目录的写权限。注意：不能删除非空目录

  实例：
  (1) 当 parent 子目录被删除后使它也成为空目录的话，则顺便一并删除

  ```bash
  rmdir -p parent/child/child11
  ```

- mv 命令

  > 移动文件或修改文件名，根据第二参数类型（如目录，则移动文件；如为文件则重命令该文件）。当第二个参数为目录时，可刚多个文件以空格分隔作为第一参数，移动多个文件到参数 2 指定的目录中

  实例：
  (1) 将文件 test.log 重命名为 test1.txt

  ```bash
  mv test.log test1.txt
  ```

  (2) 将文件 log1.txt,log2.txt,log3.txt 移动到根的 test3 目录中

  ```bash
  mv log1.txt log2.txt log3.txt /test3
  ```

  (3) 将文件 file1 改名为 file2，如果 file2 已经存在，则询问是否覆盖

  ```bash
  mv -i log1.txt log2.txt
  ```

  (4) 移动当前文件夹下的所有文件到上一级目录

  ```bash
  mv * ../
  ```

- cp 命令

  > 将源文件复制至目标文件，或将多个源文件复制至目标目录。注意：命令行复制，如果目标文件已经存在会提示是否覆盖，而在 shell 脚本文件中，如果不加-i 参数，则不会提示，而是直接覆盖！

  常用参数：

  ```bash
  cp -i 提示
  cp -r 复制目录及目录内所有项目
  cp -a 复制的文件与原文件时间一样
  ```

  实例：
  (1) 复制 a.txt 到 test 目录下，保持原文件时间,如果原文件存在提示是否覆盖

  ```bash
  cp -ai a.txt test
  ```

  (2) 为 a.txt 建议一个链接（快捷方式）

  ```bash
  cp -s a.txt link_a.txt
  ```

- cat 命令
  cat 主要有三大功能： 1.一次显示整个文件:cat filename 2.从键盘创建一个文件:cat > filename 只能创建新文件,不能编辑已有文件. 3.将几个文件合并为一个文件:cat file1 file2 > file

  参数:
  -b 对非空输出行号
  -n 输出所有行号

  实例：
  (1) 把 log2012.log 的文件内容加上行号后输入 log2013.log 这个文件里

  ```bash
  cat -n log2012.log log2013.log
  ```

  (2) 把 log2012.log 和 log2013.log 的文件内容加上行号（空白行不加）之后将内容附加到 log.log 里

  ```bash
  cat -b log2012.log log2013.log log.log
  ```

- 显示日期的指令： date

- 显示日历的指令：cal

- 重要的几个热键[Tab],[ctrl]-c, [ctrl]-d
  [Tab]按键—具有『命令补全』不『档案补齐』的功能
  [Ctrl]-c 按键—让当前的程序『停掉』
  [Ctrl]-d 按键—通常代表着：『键盘输入结束(End Of File, EOF 戒 End OfInput)』的意思；另外，他也可以用来取代 exit

- 打包压缩相关命令

  ```bash
  gzip：
  bzip2：
  tar: 打包压缩
  -c 归档文件
  -x 缩文件
  -z gzip压缩文件
  -j bzip2压缩文件
  -v 显示压缩或解压缩过程 v(view)
  -f 使用档名
  ```

  实例：
  (1) tar -cvf /home/abc.tar /home/abc 只打包，不压缩
  (2) tar -zcvf /home/abc.tar.gz /home/abc 打包，并用 gzip 压缩
  (3) tar -jcvf /home/abc.tar.bz2 /home/abc 打包，并用 bzip2 压缩
  当然，如果想解压缩，就直接替换上面的命令 tar -cvf / tar -zcvf / tar -jcvf 中的“c” 换成“x” 就可以了。

- 关机/重启机器
  shutdown
  shutdown -r 关机重启
  shutdown -h 关机不重启
  shutdown now 立刻关机
  shutdown halt 关机
  shutdown reboot 重启
