### stash —— 一个极度实用的Git操作

今天要介绍的 Git 操作就是 stash，毫不夸张地说，每个用 Git 的开发人员都一定要会懂怎么使用。

在介绍之前，不知道你有没有和我一样的经历：某一天，我正在一个 feature 分支上高高兴兴地写着（ba）代（a）码（ge）。突然线上环境报错了，是我负责的部分，此时当然是救火要紧哈，准备停下手中的工作准备切 master 分支 checkout 个 hotfix 分支出来。

脑袋正闪出这个想法的时候，咦，发现有点不对劲了 —— 此时我的 feature 分支功能还没做完，comment 上去没意义呀！将修改全部删掉更是不可能，这辈子都是不可能的，那这要怎么办呢？

如果这时能把这个 feature 分支中，还没写好的代码找个地方先藏起来，等到要用的时候再拿出去就完美了。

好了，今天要介绍的主角就能实现我们的需求。我们来看下 stash 这个功能到底是怎么使用的。

假如我现在的代码是这样的：

public static void main(String[] args) {
       System.out.println("我是 feature 分支原有的代码");
       // ...
       System.out.println("我是正在开发的代码");
}
接着上面的情景，我需要把正在开发的代码给藏起来，那么直接使用 git stash 命令即可，使用后就会变成这样的效果：

public static void main(String[] args) {
       System.out.println(我是 feature 分支原有的代码");
       // ...
}
好了，正在 feature 分支还没写完的代码已经被藏起来了，此时，好奇心满满的你想着，它是被藏到哪里去呢？一顿谷歌之后，你发现可以通过这个命令查看 git stash list。




你很牛皮，线上问题没一会功夫就搞定了，此时你再次切回刚才的 feature 分支，想要把刚才藏起来的代码拿出来。好了，一顿谷歌之后，你发现有两种拿的方法，分别是：

1、git stash pop

2、git stash apply

那这两者有什么不同呢？还记得刚才提交到 git stash list 命令显示的结果吗？—— stash@(0)

git stash pop 的是恢复刚才被藏起来的代码，同时删除 stash@(0) 这条记录也删了，此时你再使用 git stash list 命令就没有结果了：


明白 git stash pop 的作用后，那 git stash apply 命令也很好理解了，它们唯一的不同就是 git stash apply 命令不会删除stash@(0) 这条记录。

最后，如果你在一个分支上使用了 n 次 git stash 命令，那么就会有 stash@(0)、stash@(1)、...、stash@(n)，对应一共有 n 条记录。

那我们要这么多条记录有什么用呢？

答案就是我们可以指定 git stash pop/apply 哪条记录。假如我想要恢复 stash@(1) 记录。那么对应的命令是 git stash pop stash@(1) 或 git stash apply stash@(1)

