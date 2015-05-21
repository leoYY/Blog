# Git branch 开发步骤

由于在平时pr以后，同一个branch上的代码继续开发的话会进入那个pr中，因此需要branch不同
场景为master上pr了，但是需要继续开发其他功能，并已经写好代码
- git branch  XXX               // 创建branch XXX    
- git checkout XXX            
- git add ...                 
- git commit -m "..."        
- git checkout master         

- git push origin master        // 只push master上的代码

对于多分支开发仍然存在，之前一个分支提交的代码在这个分支中提交pr的时候带上了
- git stash
- git stash list
- git stash pop
- git stash apply
