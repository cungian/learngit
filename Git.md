# Git教程总结
[](https://www.liaoxuefeng.com/%20%E5%BB%96%E9%9B%AA%E5%B3%B0)


git(分布式版本控制系统)，每台电脑有自己的版本库（仓库，repository），‘中央服务器’方便交换修改，安装后需设置名字和Email地址。

 **创建版本库：**
            1、`mkdir learngit        #创建空目录，即工作区`
            2、`git init         #初始化形成git可管理的仓库，.git目录是Git跟踪管理版本库的`
                （只能跟踪文本文件的改动，图像、视频等二进制文件不能跟踪变化）

***版本库文件操作：***
            1、`git add readme.txt        #把文件添加到Git仓库 （添加到暂存区Stage）`
            2、`git commit -m "a readme file"        #把文件提交到仓库，-m指定说明文字`
                （把Stage内容提交到当前分支）
            3、`git status         #查看仓库当前状态`
            4、`git diff readme.txt          #查看修改`
            5、`git log     #查看历史改动记录`
                （`git log --pretty=online        #查看精简记录`）
            6、`git reset --hard HEAD^`        #版本回退（上上版本为HEAD^ 往上100版本为HEAD~100，HEAD指定当前版本）
                （`git reset --hard 3628164`(版本号，前几位即可)）
hard含义
            7、`git reflog        #查看每次的命令，可显示commit id，结合版本回退`
            8、`git checkout -- readme.txt        #撤销修改，回到最近一次git commit或git add时的状态`
                 （`git reset HEAD readme.txt        # 可以撤销暂存区的修改放回工作区`）
            9、`rm readme.txt    #删除工作区文件`
                   1） `git rm readme.txt    #从版本库中删除文件`
                          git commit    #提交删除操作
                   2）`git checkout -- readme.txt    #恢复删除`（git checkout 用版本库的版本替换工作区的版本）

**远程仓库：**
               1、在GitHub上创建新的仓库
               2、`git remote add origin git@github.com:*/learngit.git    #把本地仓库关联到Github仓库，远程库的名称是origin`
               3、`git push -u origin master    #把本地库内容推送到远程库上`
                （第一次推送加-u,实现关联和推送，之后直接使用git push origin master）
               4、 `git clone git@github.com:*/learngit.git`
                      ( Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快)

***分支管理：***(master分支是主分支，HEAD指向master，master指向提交)
                1、`git checkout -b dev        #创建新的分支dev并切换到dev`
                (等价于: 1)`git branch dev            #创建dev分支`
                             2)`git checkout dev         #切换到dev分支`）
                 2、`git branch        #查看当前分支`
                 3、`git checkout master        #切换到master分支`
                 4、1）`git merge dev            #合并分支成果`（Fast forward模式）
                       2）`git merge --no-ff -m "merge with no-ff" dev        #禁用Fast forward模式的合并 ，会生成一个新的commit`
                 5、`git branch -d dev        #删除分支`  
                 6、`git log --graph --pretty=online --abbrev-commit        #查看合并情况，git log --graph可以看到分支合并图`
 
 ***bug分支：***
                 7、`git stash        #储存当前工作现场`
                      （git checkout mater        #确定出bug的分支
                          git checkout -b issue-101        #在出bug的分支创建临时分支
                          git checkout master         #修复完成切换到原分支
                          git  merge --no-ff -m "merged bug fix 101" issue-101        #合并分支
                           git branch -d issue -101）        #删除分支
                 8、`git stash list        #查看存储的现场`
                 9、`git stash pop        #恢复stash内容并删除`
                      （等价于：1）`git stash apply        #恢复内容`
                                       2）`git stash drop        #删除stash`）

***feature分支：***
                 10、`git branch -D feature-vulcan        #强制删除一个没有被合并过的分支`
                 11、`git remote        #查看远程库信息`
                        （`git remote -v        #查看远程库详细信息`）
                 12、`git push origin master        #推送指定分支`
                 13、`git checkout -b dev origin/dev        #创建远程origin的dev分支到本地`
                 14、`git pull        #把最新的提交抓取下来`
                 15、`git branch --set-upstream dev origin/dev        #设置dev和origin/dev的链接`

***标签管理：***
                1、`git tag v1.0        #对当前分支打标签，默认打在最新提交的commit上`
                    （git tag v0.9 6224937        #对指定commit打标签
                      git tag -a v0.1 -m "v0.1 released" 2628164        #-a指定标签名，-m指定说明文字
                      git tag -s v0.2 -m "v0.2 released" fec145a         #-s用私钥签名一个标签,采用PGP签名，需安装gpg）
                2、`git tag        #查看所有标签`
                3、`git show v0.9        #查看标签信息`
                4、`git tag -d v0.1        #删除本地的标签信息`
                5、`git push origin :refs/tags/v0.9        #删除远程标签信息`
                6、`git push origin v1.0        #推送标签到远程`
                    （`git push origin --tags        #一次性推送全部尚未推送到远程的本地标签`）

**github:**
                1、Fork:在自己账户克隆一个仓库
                2、`git clone git@github.com:*/bootstrap.git`





