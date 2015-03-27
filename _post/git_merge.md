# Git merge 步骤

由于经常在github上的开发逻辑是先fork，然后改完pull request的方式，往往在commit前会发现fock的对象早已更改

- git remote -v 
- git remote add upstream repo.git
- git fetch upstream
- git branch -va
- git checkout master
- git merge upstream/master


参考[stackoverflow](http://stackoverflow.com/questions/7244321/how-to-update-github-forked-repository)
