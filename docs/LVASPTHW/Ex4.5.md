# Ex4.5: VASP任务的批量提交-1

在提交VASP任务之前，我们先学习一下在Linux系统中常用的批量处理任务文件的办法。本书的宗旨是：稳中求快，欲速则不达。因此，不是所谓的速成教材，不是10分钟学会XXX的理想手册，更不是鼠标的点点操作。每一节的内容，都需要认真阅读，亲自上手操作练习。如果耐不住性子，请放弃本书的学习。而大师兄VASP多年的经验告诉我，批量处理在新手学习上有着非常重要的作用。新手刚接触VASP，总是面临着参数不知道怎么去选择的问题，总是很疑惑，怕自己设置错了，浪费纳税人的钱和自己的时间，其实更多的是怕被老板骂。其实，这种情况有时候很好处理，找个简单例子，不同参数批量测试下就可以了。这里的简单例子指的是几分钟或者更短就可以算完的。没必要千万别用耗时很长的例子做测试。



#### 大家常用的测试方法

在VASP官网上，亦或者百度里面搜索的VASP教程里面，你可以找到很多个测试参数的小脚本，大部分都是这样的：参考链接：https://www.vasp.at/wiki/index.php/Cd_Si

```bash
#! /bin/bash
BIN=/path/to/your/vasp/executable
rm WAVECAR SUMMARY.dia
for i in  5.1 5.2 5.3 5.4 5.5 5.6 5.7 ; do
cat >POSCAR <<!
cubic diamond
   $i 
 0.0    0.5     0.5
 0.5    0.0     0.5
 0.5    0.5     0.0
  2
Direct
 -0.125 -0.125 -0.125
  0.125  0.125  0.125
!
echo "a= $i" ; mpirun -n 2 $BIN
E=`awk '/F=/ {print $0}' OSZICAR` ; echo $i $E  >>SUMMARY.dia
done
cat SUMMARY.dia
```

然而，很多新手对linux的基本命令还不是很熟悉，更不用说脚本了。由于对于本书所默认的Linux基础为0的`VASPie`来说，上面的脚本会有些难度。因此，本节需要学习在linux系统下（确切点是在一个Terminal，终端里），一些基本的命令以及大师兄本人常用的批量处理任务文件的一个办法。这时候你要问了，师兄，你的这个方法和VASP官网中的那个比起来，哪个更好啊？其实本质是一样的。只是操作思路稍微有些区别。这个没有最好的，要根据你所要达到的目标，目前对程序的理解水平来定的。但是，你必须要学会一种适合自己思路的，一个好的开始对于大家的后程发力和高效解决日常任务非常重要。

**任务来了：**

现在我们需要完成下面的任务，具体要求如下：

1）有个文件夹名字为：0.01，里面有INCAR，KPOINTS，POSCAR， POTCAR。 INCAR中SIGMA的取值为：`SIGMA = 0.01`;

2） 创建共9个文件夹：0.02，0.03，0.04, 0.05，.... ，0.10;

3）每个文件夹中都有与0.01文件夹中相同KPONTS, POSCAR，POTCAR;

4）每个文件夹中都有INCAR，但INCAR中SIGMA这个参数的取值和文件夹的名字一样，其他参数保持不变。

从任务可以看出，我们是在准备测试SIGMA取值对计算影响的输入文件。为实现这个小目标，我们可以这样做：将0.01复制成0.02,0.03...0.10，然后挨个修改里面的INCAR文件。如下：

```
cp 0.01 0.02
cp 0.01 0.03
......
cp 0.01 0.10
vi 0.02/INCAR
vi 0.03/INCAR
......
vi 0.10/INCAR
```

* 小窍门-1：运行完第一个命令后，敲一下键盘的向上箭头，就会出现刚刚运行的命令，直接修改最后一个数字即可。
* 小窍门-2：尝试着使用`Control +R`搜索终端里面的历史命令；具体操作自行百度或者google， 关键词：`Control R Linux`



**神奇的for循环**

但大师兄不想挨个创建这9个文件夹，也不想挨个编辑修改INCAR文件中的SIGMA数值。想必大家都不想这么做，因此，在这里教给大家使用一个for循环来快速实现我们的小目标。



```bash
qli@bigbrosci Ex02 % ls 0.01 
INCAR    KPOINTS  POSCAR   POTCAR
qli@bigbrosci Ex02 % cat 0.01/INCAR 
SYSTEM = O atom 
ISMEAR = 0       
SIGMA = 0.01      
qli@bigbrosci Ex02 %  
qli@bigbrosci Ex02 % for i in 0.{02..10}; do cp 0.01 $i ;done 
qli@bigbrosci Ex02 % ls
0.01/ 0.02/ 0.03/ 0.04/ 0.05/ 0.06/ 0.07/ 0.08/ 0.09/ 0.10/
qli@bigbrosci Ex02 % ls *
0.01:
INCAR  KPOINTS  POSCAR  POTCAR

0.02:
INCAR  KPOINTS  POSCAR  POTCAR

0.03:
INCAR  KPOINTS  POSCAR  POTCAR
........
```

**for循环详解:**

1）  `0.{02..10}` 是为了获取从0.02到0.09的所有数字， 有以下几点需要注意:

* `for i in 0.{02..05}` 和 `for i in 0.02 0.03 0.04 0.05`  效果是一样的

* 用的是花括号， 花括号中02和10中间有两个点` ..  `; 两个点之间没有空格，02, 09与两个点之间也没有空格。

* 不要用中文输入法敲命令。

2）大家还可以练习下面这几个命令来看一下效果:  `echo`是打印输出的命令。

```
echo {1..100} 
echo {A..Z}
echo {a..z}
echo {a..z}{1..10}{A..Z}
```

3） `for i in {02..10} `: 翻译过来就是：对于从02到10的任意数字 i (i在这里是一个变量) ；我们给 i 赋值，值的范围是 从02到09 ; 两点需要注意:

*  i 只是个人喜好而已， 你也可以用` for sigma in  XXX` ; `for bigbro in XXX;  `

* in 后面是一个集合; 怎么选取这个集合决定了for循环的威力;

4） ` for i in XXX`;  这个句字后面跟着一个分号`;`，如果没有便会出错。分号前后可以有空格，也可以没有，为了让自己写的东西更加直观，建议加上空格; 

5） do 翻译过来就是： 我们要实现什么任务，要干嘛，也就是目的。 do 后面跟一个空格， 或者几个空格；然后就是具体的命令；

6） `cp 0.01  $i  `

* 把文件夹`0.01`复制成 $i变量所对应的文件夹，也就是从0.02到0.10

* $i 被替换成for后面变量 i 的值;

7） 复制完成后，后面跟着一个分号;  

8） done 完成任务。

9）大家可以尝试着其他类似的命令： `for i in XXX; do XXX ; done`  比如: 

```
for bigbro in {A..Z}; do echo bigbro is $bigbro ; done
```

这个例子只是为了说明：

+ for 后面的变量如果你用` i` 表示，那么后面就用`$i` 来引用；

- 如果用`bigbro` 来表示，后面则用`$bigbro`; 
- `$`和后面的变量之间`bigbro`没有空格。（你可以加上空格，看看有什么错误出现！）



**小结:**

通过本小节的学习我们要初步掌握`for`循环来实现批量处理的效果。学会使用`echo`，掌握`{}` 的用法；

```bash
for i in XXX ; do something ; done
```

本节的for循环，我们只完成了一半的任务，每个文件夹中的INCAR还没有修改，下一节我们介绍for循环结合`sed`命令实现批量处理文件的方法来。再次强调一下，`linux`的命令操作有很多的小技巧，大家一定要多多去网上搜集，加以练习，这对于提高工作效率及其有帮助。