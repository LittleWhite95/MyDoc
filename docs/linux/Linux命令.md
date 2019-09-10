

### 1.基本命令和操作

#### 	(1)基本命令

```
#创建一个名为 file 的文件，touch是一个命令,后面可创建多个文件
$ touch file[,file2]
#进入一个目录，cd是一个命令
$ cd /etc/
#返回上一级目录
$ cd ..
#查看当前所在目录
$ pwd
#列出当前目录下的所有文件
$ ll
#列出当前目录指定后缀名的文件
$ ls *.txt
#查看文件
$ cat 01.txt
#编辑文件 :q直接退出  :wq保存退出
$ vim/vi 01.txt 
#进入home目录
$ cd ~ 或者 cd /home/<你的用户名>
```

#### 	(2)常用快捷键

```
[Tab]
使用Tab键来进行命令补全，连续按两次 Tab 可以显示全部候选结果
[Ctrl+c]
强行终止当前程序
Ctrl+d	键盘输入结束或退出终端
Ctrl+s	暂停当前程序，暂停后按下任意键恢复运行
Ctrl+z	将当前程序放到后台运行，恢复到前台为命令fg
Ctrl+a	将光标移至输入行头，相当于Home键
Ctrl+e	将光标移至输入行末，相当于End键
Ctrl+k	删除从光标所在位置到行末
Alt+Backspace	向前删除一个单词
Shift+PgUp	将终端显示向上滚动
Shift+PgDn	将终端显示向下滚动
```

### 2.用户及文件权限管理

#### (1)查看用户

![image](https://doc.shiyanlou.com/document-uid735639labid3timestamp1531731170296.png/wm)

```
$ who am i
或者
$ who mom likes  第二列的 pts/0 中 pts 表示伪终端

# 查看当前用户名
whoami
```

#### (2)创建用户

```
su <user> 可以切换到用户 user，执行时需要输入目标用户的密码
shiyanlou 用户密码可以通过 sudo passwd shiyanlou 命令进行设置
# 新建一个叫 lilei 的用户：
$ sudo adduser lilei
# 使用如下命令切换登录用户
$ su -l lilei
```

#### (3)用户组

- 查看用户所属的用户组，使用 groups 命令

```
$ groups shiyanlou
```

![img](https://doc.shiyanlou.com/document-uid13labid3timestamp1454035714557.png/wm)

- 将其它用户加入 sudo 用户组，使用拥有root权限的用户操作

```
$ su shiyanlou # 此处需要输入 shiyanlou 用户密码，shiyanlou 的密码可以通过 `sudo passwd shiyanlou` 进行设置。
$ groups lilei
$ sudo usermod -G sudo lilei
$ groups lilei
```

- 删除用户

  ```
  $ sudo deluser lilei --remove-home
  ```

### 3.文件权限

#### (1)查看文件权限

```
$ ll
```

![img](https://doc.shiyanlou.com/document-uid735639labid3timestamp1531731455816.png/wm)

![img](https://doc.shiyanlou.com/linux_base/3-9.png/wm)

![img](https://doc.shiyanlou.com/linux_base/3-10.png/wm)

**一个目录同时具有读权限和执行权限才可以打开并查看内部文件，而一个目录要有写权限才允许在其中创建其它文件**

- 查看当前目录下的所有文件，包含隐藏文件

  ```
  $ ll -A
  ```

- 查看某一个目录的完整属性

  ```
  $ ls -dl <目录名>
  ```

#### (2)变更文件所有者

原来iphone6的权限为lilei

![img](https://doc.shiyanlou.com/document-uid600404labid3timestamp1532311534658.png/wm)

- 修改权限拥有者

  ```
  sudo chown shiyanlou iphone6
  ```

  修改后的权限拥有者为shiyanlou:

  ![img](https://doc.shiyanlou.com/document-uid735639labid3timestamp1531731650844.png/wm)

#### (3)修改文件权限

![img](https://doc.shiyanlou.com/linux_base/3-14.png/wm)

- 修改权限为其他用户无法读写

  ```
  方式1 ：二进制数字表示
  $ chmod 600 iphone6
  ```

  ![3-3.3-1](https://doc.shiyanlou.com/document-uid735639labid3timestamp1531731724644.png/wm)

  ```
  方式2：加减赋值操作[g、o 还有 u 分别表示 group、others 和 user，+ 和 - 分别表示增加和去掉相应的权限。]
  $ chmod go-rw iphone6
  ```

### 4.目录结构和文件基本操作

![img](https://doc.shiyanlou.com/linux_base/4-1.png/wm)

![æ­¤å¤è¾å¥å¾ççæè¿°](https://doc.shiyanlou.com/document-uid18510labid59timestamp1482919171956.png/wm)

#### (1)新建

- 新建空白文件

  ```
  $ touch test
  ```

- 新建目录

  ```
  $ mkdir mydir
  
  使用 -p 参数，同时创建父目录
  $ mkdir -p father/son/grandson
  ```

#### (2)复制

- 复制文件

  ```
  复制test文件到grandson目录中
  $ cp test father/son/grandson 
  ```

- 复制目录

  ```
  要成功复制目录需要加上 -r 或者 -R 参数，表示递归复制
  $ mkdir family
  $ cp -r father family
  ```

#### (3)删除

- 删除文件

  ```
  普通删除一个文件
  $ rm test
  强制删除一个文件
  $ rm -f test
  ```

- 删除目录

  ```
  $ rm -r family
  ```

#### (4)移动文件与文件重命名

- 移动文件

  ```
  mv 源目录文件 目的目录：
  $ mv file1 Documents
  ```

- 重命名文件

  ```
  mv 旧的文件名 新的文件名：
  $ mv file1 myfile
  ```

- 批量重命名

  ```
  $ cd /home/shiyanlou/
  
  # 使用通配符批量创建 5 个文件:
  $ touch file{1..5}.txt
  
  # 批量将这 5 个后缀为 .txt 的文本文件重命名为以 .c 为后缀的文件:
  $ rename 's/\.txt/\.c/' *.txt
  
  # 批量将这 5 个文件，文件名和后缀改为大写:
  $ rename 'y/a-z/A-Z/' *.c
  ```

#### (5)查看文件

- 使用 cat，tac 和 nl 命令查看文件【 cat为正序显示，tac为倒序显示】

  ```
  $ cat passwd
  可以加上 -n 参数显示行号
  $ cat -n passwd
  
  nl 命令，添加行号并打印
  -b : 指定添加行号的方式，主要有两种：
      -b a:表示无论是否为空行，同样列出行号("cat -n"就是这种方式)
      -b t:只列出非空行的编号并列出（默认为这种方式）
  -n : 设置行号的样式，主要有三种：
      -n ln:在行号字段最左端显示
      -n rn:在行号字段最右边显示，且不加 0
      -n rz:在行号字段最右边显示，且加 0
  -w : 行号字段占用的位数(默认为 6 位)
  ```

- 使用 more 和 less 命令分页查看文件

  ```
  使用 more 命令打开 passwd 文件：【可以使用 Enter 键向下滚动一行，使用 Space 键向下滚动一屏，按下 h 显示帮助，q 退出。】
  $ more passwd
  ```

- 使用 head 和 tail 命令查看文件

  ```
  $ tail /etc/passwd  //默认显示头10行内容
  自定义查看多少行，加上 -n 参数，后面紧跟行数：
  $ tail -n 1 /etc/passwd
  实现不停地读取某个文件的内容并显示。这可以让我们动态查看日志，达到实时监视的目的。
  $tail -f passwd
  ```

(6)查看文件类型

- file命令

  ```
  $ file /bin/ls
  ```

### 5.环境变量与文件查找

#### (1)环境变量

- 使用 `declare` 命令创建一个变量名为 tmp 的变量：

  ```
  $ declare tmp
  ```

- 使用 `=` 号赋值运算符，将变量 tmp 赋值为 shiyanlou：

  ```
  $ tmp=shiyanlou
  ```

- 读取变量的值，使用 `echo` 命令和 `$` 符号（**$ 符号用于表示引用一个变量的值，初学者经常忘记输入**）：

  ```
  $ echo $tmp
  ```

  **变量名只能是英文字母、数字或者下划线**



- `set`，`env`，`export`。这三个命令很相似，都是用于打印环境变量信息，区别在于涉及的变量范围不同

| 命 令    | 说 明                                                        |
| -------- | ------------------------------------------------------------ |
| `set`    | 显示当前 Shell 所有变量，包括其内建环境变量（与 Shell 外观等相关），用户自定义变量及导出的环境变量。 |
| `env`    | 显示与当前用户相关的环境变量，还可以让命令在指定环境中运行。 |
| `export` | 显示从 Shell 中导出成环境变量的变量，也能通过它将自定义变量导出为环境变量。 |

#### (2)命令的查找路径与顺序

- 查看 PATH 环境变量的内容：

  查看 `PATH` 环境变量的内容：

  ```
  $ echo $PATH
  ```

#### (3)添加自定义路径到“ PATH ”环境变量

- 添加自定义路径：

  ```
  $ PATH=$PATH:/home/shiyanlou/mybin
  注意这里一定要使用绝对路径。
  ```

- 在每个用户的 home 目录中有一个 Shell 每次启动时会默认执行一个配置脚本，以初始化环境，包括添加一些用户自定义环境变量等等。zsh 的配置文件是 `.zshrc`，相应 Bash 的配置文件为 `.bashrc` 

  我们可以简单地使用下面命令直接添加内容到 `.zshrc` 中：

  ```
  $ echo "PATH=$PATH:/home/shiyanlou/mybin" >> .zshrc
  ```

  **上述命令中 >> 表示将标准输出以<u>*追加的方式*</u>重定向到一个文件中，注意前面用到的 > 是<u>*以覆盖的方式*</u>重定向到一个文件中，使用的时候一定要注意分辨。在指定文件不存在的情况下都会创建新的文件。**

#### (4)修改和删除已有变量

- 变量修改

  | 变量设置方式                   | 说明                                         |
  | ------------------------------ | -------------------------------------------- |
  | `${变量名#匹配字串}`           | 从头向后开始匹配，删除符合匹配字串的最短数据 |
  | `${变量名##匹配字串}`          | 从头向后开始匹配，删除符合匹配字串的最长数据 |
  | `${变量名%匹配字串}`           | 从尾向前开始匹配，删除符合匹配字串的最短数据 |
  | `${变量名%%匹配字串}`          | 从尾向前开始匹配，删除符合匹配字串的最长数据 |
  | `${变量名/旧的字串/新的字串}`  | 将符合旧字串的第一个字串替换为新的字串       |
  | `${变量名//旧的字串/新的字串}` | 将符合旧字串的全部字串替换为新的字串         |

  ```
  $ path=$PATH
  $ echo $path
  $ path=${path%/home/shiyanlou/mybin}
  # 或使用通配符,*表示任意多个任意字符
  $ path=${path%*/mybin}
  ```

- 变量删除

  可以使用 `unset` 命令删除一个环境变量：

  ```
  $ unset temp
  ```

#### (5)让环境变量立刻生效

- 使用 `source` 命令来让其立即生效

  ```
  $ cd /home/shiyanlou
  $ source .zshrc
  ```

  `source` 命令还有一个别名就是 `.`，上面的命令如果替换成 `.` 的方式就该是：

  ```
  $ . ./.zshrc
  ```

  在使用`.`的时候，需要注意与表示当前路径的那个点区分开。

  注意第一个点后面有一个空格，而且后面的文件必须指定完整的绝对或相对路径名，source 则不需要。

#### (6)搜索文件

- **whereis 简单快速**

```
$ whereis who
$ whereis find
```

- **locate 快而全**

  如查找 /etc 下所有以 sh 开头的文件：(有时候你刚添加的文件，它可能会找不到，需要手动执行一次 <u>***updatedb***</u> 命令（在我们的环境中必须先执行一次该命令）)

  ```
  $ sudo apt-get update
  $ sudo apt-get install locate
  $ locate /etc/sh
  ```

  ![1562591146936](C:\Users\wit16\AppData\Roaming\Typora\typora-user-images\1562591146936.png)

- **which 小而精**

  ```
  $ which man
  ```

- **find 精而细**

```
$ sudo find /etc/ -name interfaces
```

![1562591210718](C:\Users\wit16\AppData\Roaming\Typora\typora-user-images\1562591210718.png)

> **注意 find 命令的路径是作为第一个参数的， 基本命令格式为 find [path] [option] [action] 。**

与时间相关的命令参数：

| 参数     | 说明                   |
| -------- | ---------------------- |
| `-atime` | 最后访问时间           |
| `-ctime` | 最后修改文件内容的时间 |
| `-mtime` | 最后修改文件属性的时间 |

列出 home 目录中，当天（24 小时之内）有改动的文件：

```
$ find ~ -mtime 0
```

列出用户家目录下比 Code 文件夹新的文件：

```
$ find ~ -newer /home/shiyanlou/Code
```



### 6.文件打包和解压缩

#### (1)zip 压缩打包程序

- 使用 zip 打包文件夹：

```
$ cd /home/shiyanlou
$ zip -r -q -o shiyanlou.zip /home/shiyanlou/Desktop
$ du -h shiyanlou.zip
$ file shiyanlou.zip
```

`-r` 参数表示递归打包包含子目录的全部内容，`-q` 参数表示为安静模式，即不向屏幕输出信息，`-o`，表示输出文件，需在其后紧跟打包输出文件名。

- 设置压缩级别为 9 和 1（9 最大，1 最小），重新打包：

```
$ zip -r -9 -q -o shiyanlou_9.zip /home/shiyanlou/Desktop -x ~/*.zip
$ zip -r -1 -q -o shiyanlou_1.zip /home/shiyanlou/Desktop -x ~/*.zip
```

这里添加了一个参数用于设置压缩级别 `-[1-9]`，1 表示最快压缩但体积大，9 表示体积最小但耗时最久。最后那个 `-x` 是为了排除我们上一次创建的 zip 文件，否则又会被打包进这一次的压缩文件中，**注意：这里只能使用绝对路径，否则不起作用**。

用 `du` 命令分别查看默认压缩级别、最低、最高压缩级别及未压缩的文件的大小：

```
$ du -h -d 0 *.zip ~ | sort
```

> 通过 man 手册可知：
>
> - h， --human-readable（顾名思义，你可以试试不加的情况）
> - d， --max-depth（所查看文件的深度）

- 创建加密 zip 包

使用 `-e` 参数可以创建加密压缩包：

```
$ zip -r -e -o shiyanlou_encryption.zip /home/shiyanlou/Desktop
```

如果你想让你在 Linux 创建的 zip 压缩文件在 Windows 上解压后没有任何问题，那么你还需要对命令做一些修改：

```
$ zip -r -l -o shiyanlou.zip /home/shiyanlou/Desktop
```

需要加上 `-l` 参数将 `LF` 转换为 `CR+LF` 来达到以上目的。



#### (2)使用 unzip 命令解压缩 zip 文件

将 `shiyanlou.zip` 解压到当前目录：

```
$ unzip shiyanlou.zip
```

使用安静模式，将文件解压到指定目录：

```
$ unzip -q shiyanlou.zip -d ziptest
```

上述指定目录不存在，将会自动创建。如果你不想解压只想查看压缩包的内容你可以使用 `-l` 参数：

```
$ unzip -l shiyanlou.zip
```

使用 `-O`（英文字母，大写 o）参数指定编码类型：(解压乱码问题)

```
unzip -O GBK 中文压缩文件.zip
```

#### (3)tar打包工具

- 创建一个 tar 包：

```
$ cd /home/shiyanlou
$ tar -cf shiyanlou.tar /home/shiyanlou/Desktop
```

上面命令中，`-c` 表示创建一个 tar 包文件，`-f` 用于指定创建的文件名，注意文件名必须紧跟在 `-f` 参数之后，比如不能写成 `tar -fc shiyanlou.tar`，可以写成 `tar -f shiyanlou.tar -c ~`。你还可以加上 `-v` 参数以可视的的方式输出打包的文件。上面会自动去掉表示绝对路径的 `/`，你也可以使用 `-P` 保留绝对路径符。

- 解包一个文件（`-x` 参数）到指定路径的**已存在**目录（`-C` 参数）：

```
$ mkdir tardir
$ tar -xf shiyanlou.tar -C tardir
```

- 只查看不解包文件 `-t` 参数：

```
$ tar -tf shiyanlou.tar
```

- 保留文件属性和跟随链接（符号链接或软链接），有时候我们使用 tar 备份文件当你在其他主机还原时希望保留文件的属性（`-p` 参数）和备份链接指向的源文件而不是链接本身（`-h` 参数）：

```
$ tar -cphf etc.tar /etc
```

对于创建不同的压缩格式的文件，对于 tar 来说是相当简单的，需要的只是换一个参数，这里我们就以使用 `gzip` 工具创建 `*.tar.gz` 文件为例来说明。

- 我们只需要在创建 tar 文件的基础上添加 `-z` 参数，使用 `gzip` 来压缩文件：

```
$ tar -czf shiyanlou.tar.gz /home/shiyanlou/Desktop
```

- 解压 `*.tar.gz` 文件：

```
$ tar -xzf shiyanlou.tar.gz
```

![此处输入图片的描述](https://doc.shiyanlou.com/document-uid735639labid61timestamp1532339561961.png/wm)

现在我们要使用其它的压缩工具创建或解压相应文件只需要更改一个参数即可：

| 压缩文件格式 | 参数 |
| ------------ | ---- |
| `*.tar.gz`   | `-z` |
| `*.tar.xz`   | `-J` |
| `*tar.bz2`   | -j   |

#### (4)总结

 常用命令：

- zip：
  - 打包 ：zip something.zip something （目录请加 -r 参数）
  - 解包：unzip something.zip
  - 指定路径：-d 参数
- tar：
  - 打包：tar -cf something.tar something
  - 解包：tar -xf something.tar
  - 指定路径：-C 参数