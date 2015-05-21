# Git branch 开发步骤

由于在平时pr以后，同一个branch上的代码继续开发的话会进入那个pr中，因此需要branch不同
场景为master上pr了，但是需要继续开发其他功能，并已经写好代码
- git branch  XXX             ----  创建branch XXX
- git checkout XXX            ----  切换到branch XXX
- git add ...                 ----  将更新后的代码add到该branch上
- git commit -m "..."         ----  commit到branch XXX 中
- git branch master           
- git checkout master         ----  恢复到master 最后一次commit的情况

- git push origin master      ----  只push master上的代码
