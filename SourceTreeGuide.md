#SourceTreeGuide
##### 作者：Mark24
##### 邮箱：mark.zhangyoung@qq.com
##### 时间：2016.02.19
![Source Logo](http://ww1.sinaimg.cn/mw690/44894cbbgw1euiv3622uwj2074074dfu.jpg)


<hr>
###许可证
采用最新的GPL许可证

转载请注明来源
 
<hr>

##先来说说Git是咋么一回事##

写代码，写完了保存，这是一般文件的流程。Git多加了一个流程，就是保存后，你要提交。Git会追踪你每次保存，和上次保存之间的差别，然后把这些信息，保存在一个文件夹下，文件夹名叫.git。这个文件夹，Git的术语里称之为<strong>仓库</strong>，用仓库可以追踪代码，看到每次改变了什么，可以还原到以前的状态，也可以看别人改了什么，这就是代码版本控制的本质，一种高级的保存功能，自带时光机的那种


现在祭上图  
![git map](http://ww1.sinaimg.cn/mw690/44894cbbgw1euigc99z8wj20e40bpjsm.jpg)

咱们挨个挨个解释一下，解释完，大概就知道怎么回事了。
第一遍看不懂，不放多看几遍，或者看看其他的资料，对照着。每个人理解的点可能不一样。
最好把这张图，单独开在一个窗口，对照着，下面就来解释这个图  

首先看这张图中间，四个圆柱 ：

* Workspace:工作区，就是你正在写的代码  
* index：暂存区，一个本地的缓冲区  
* local repository：本地仓库  
* remote repository：远程仓库  

 
##Workspace工作区  

就是你正在写的代码，正在打开的编辑器里面的内容，解释完了，就这样  

 
##index暂存区

index照理应该翻译叫索引，这里叫暂存区  
暂存区是干嘛的？  
暂存区是Git和SVN的最重要的差别之一  
我们来看图，箭头就是代码流动的方向  

Git的流程工作流程就是：  
眼前正在写的代码（workspace）觉得差不多了  
add命令  
提交到暂存区（index）类似于保存一下  
然后你可以返回正在写的代码（workspace）继续写，写的到了一个阶段了  
add命令  
又提交到了暂存区（index）  

对就是这样子工作的！  

举一反三！！  
举一反三！！  
重要的事情说三遍，举一反三  

当你多次提交，基本工作完成的差不多了  
按照道理  
你应该每次都add到了index暂存区  

现在好了，任务完成  
要把暂存区里的东西，放到本地仓库(local repository)  

使用commit命令  

大家看图应该注意到  
worksp --> local repository  
有一个绿色的箭头 commit -a  
这条命令  
就是同时完成，把当前的修改，提交到暂存区，然后把暂存区的提交到  
本地仓库  

Git每次提交的，都是保存变化的改动，不是简简单单的复制一遍  

 
##本地仓库（local repository）

就是正式的代码保存的地方  

如果你本地所有的内容都被commit到本地仓库了  
表示你已经很满意所有的代码  
并且完成了所有的编写  

这个时候，你想把代码上传到Github或者公司的Git服务器，提交给别人  
看图  
local repository --> remote repository  
中间是push操作  

想对你正在工作的电脑，你电脑叫local，本地  
网络上的，就叫remote，远程  

 
##remote repository 远程仓库  
就是网络上的仓库  
一般是放在网络上保存  
或者和团队一起配合着干活  
网络仓库就成为一个中枢的感觉  

我们看图的上半部分  
提交的过程，按照箭头，由下往上：  

remote repository：远程仓库  
^  
|  
| push：就是“推”，把本地的正式的提交代码，推到网络上  
|  
local repository：本地仓库  
^  
|  
| commit：合并多次修改，提交到仓库保存  
|  
index :暂存区  
^  
|  
| add：一段阶段的代码，保存  
|  
Workspace：正在写代码，写的不错了  



再来看看这张图的下三路  

remote repository --> workspace  

这里有一个pull 黄颜色的，操作（rebase后面讲）  
pull就是“拉”的意思，拉动，把网络的代码，拉动到本地  
拉动的目标是workspace，就是你正在写的代码  

解释一下这里，比如你正在写代码，或者打开了一个项目  
编辑器Sublime Text上代码显示出来了，表示文件打开了  
这个时候，公司的小明告诉你，公司昨天几位同事加班加点，代码更新了  
让你更新一下代码,以获得人家工作一晚上加班的工作成果  
你这个时候就要pull，拉取最新的代码，以保证自己和大家的工作进度一致  
pull的意义在于，执行完操作，会刷新你的编辑器  
Sublime Text上的代码，会变化到最新的代码  
不信你试试  

TortoiseGit来pull的时候，编辑器刷新与否，似乎看心情 = =b  

下面来看红色，红色的两个箭头  
最左边有一个小字  
revert  
意思大概是反转，撤销的意思  

对啊，你光提交，万一提交错了呢？  
Git里有一套撤销的机制  
撤销的机制尤其复杂  
这里引用一篇文章[戳这里](http://www.jointforce.com/jfperiodical/article/796?m=d03)  
不过那些都不是我们要说的重点  
学习嘛，要抓住主干，细枝末节的，晚点再说，又不一定全都遇上  
Git复杂的就可能是撤消了，这些我们暂时不管  

下面还有两路灰色的，左边的说明是compare  
就是可以比较你每次修改的代码和之前的代码有什么区别  
这是Git最重要的作用，就是可以看到每次提交的不同  

这些也不说，放在后面说  

现在主要的就是把上三路和pull熟悉  

###小结

【工作区】->add->【暂存区】->commit->【本地仓库】->push->【远程仓库】  
 
【工作区】<------------------  pull ----------------- 【远程仓库】

记住：
add、commit、push、pull 



##可爱的Source Tree

![Source Logo](http://ww1.sinaimg.cn/mw690/44894cbbgw1euiv3622uwj2074074dfu.jpg)

Source Tree是一个优秀的，直觉式的Git的图形界面客户端  
Source Tree用了很优雅的方式和直觉化的流程，让你很优雅的使用Git  
基本上所有常用场景下，都可以胜任，如果实在情况特殊，使用命令行  

下面是Source Tree界面  
![Source Tree 界面](http://ww3.sinaimg.cn/mw690/44894cbbgw1euii84onscj212r0ntwke.jpg)

Source Tree的设计符合直觉  
这张图上面的图标，基本上是所有常用的操作了

* Clone/New：Clone就是克隆，copy拷贝的另一种称呼，这里意思是从远程仓库，拷贝一个项目到本地  

* Commit:大家一看就明白   

* Checkout:没讲，简单的说，你保存了一个版本到暂存区，然后继续写，写着写着后悔了，挨个挨个改回去太麻烦，checkout就是从暂存区的一个保存版本还原到正在写的编辑器，这一点，看第一地图，红色的短的checkout描述的就是这个意思（checkout HEAD后面讲)  

* Discard:丢弃  

* Stash：保存你目前的所有状态，到一个特别的文件-->我个人觉得这个很常用，一会提到  

* Add:把文件提到暂存区  

* Fetch：看看地图，远程仓库拉去到仓库，目前打开的编辑器不会变化  

* Pull：提过了  

* Branch：分支,这个不讲，一般项目负责人负责  

* Merge: 合并分支，同上

觉得难记没关系，SourceTree有中文界面可以挑  
用英文，主要是和Git的命令，对应起来，有助于找规律  

下面一个框区，就是diff，比较代码不同的地方  
红色是删掉的，标记为减号  
绿色是添加的，标记为加号  

Source Tree实时帮你显示，所以diff这个命令压根不需要你敲  

现在了解完毕Git的工作流程  
现在让我们用Source Tree走一遍

本篇文章就是在Github上建立的一个项目(如果不知道怎么做，请查询Github官方教程)  
然后clone到本地  
把项目添加到了Source Tree

![step1](http://ww1.sinaimg.cn/mw690/44894cbbgw1euivz8amudj20wa0lajwb.jpg)

把项目添加到Source Tree  
下面简称SourceTree为ST
然后用编辑器打开文件编辑，编辑完毕后，保存文件，这个一定要保存，然后可以把编辑器最小化了，然后可以看看ST  
点击如图，第一步，工作副本
这个要经常点，只要你点了，切换就会刷新  
稍微等一会，第二部的地方，就会出现文件的修改状态  
第二部所在的区域，就是工作区，就是你编辑器，编辑器的文件临时状态，可以部分选，也可以全选，选择后，会出现如下图：

![step2](http://ww3.sinaimg.cn/mw690/44894cbbgw1euivz8qdnkj20vi0ki430.jpg)

整个项目移动到上面，就是暂存区，右边是Diff状态，表示你修改了什么

提交按钮，就是Commit，点击他，进入下图：

![step3](http://ww2.sinaimg.cn/mw690/44894cbbgw1euivz9a1mpj20vi0kin23.jpg)

如图会跳出一个commit信息，看过Git的同学，应该知道，每次commit都会让你键入一个message，其实就是写明，你做了什么，改了什么，这样子等到回退，撤销的时候，一看信息就明白了

下面有一个按钮，和上面的推送是一样的  
可以先commit，然后push  
如果仓库是配置好的  

按一下，就可以提交代码了  

提交好代码后，可以看到如图：

![step4](http://ww1.sinaimg.cn/mw690/44894cbbgw1euivz9ommyj20wa0la79d.jpg)

左边的分支，可以看到整体情况  
右边的字段：  
图表：一种分支图，可以看清项目合并情况  
描述：就是commit的message  
提交：提交生成的hash码  
作者：谁提交的，这个团队配合作用救命掀了

真正的复杂的项目，上一张图，让大家感受下：

![step5](http://ww3.sinaimg.cn/mw690/44894cbbgw1euivzaquodj20vj0iladg.jpg)

分支情况会特别的复杂，感受下。

###小结

ST确实用图形界面把Git的操作简化到十分优雅的地步  
Git提交代码的流程，已经描述完毕  
是不是十分简单



