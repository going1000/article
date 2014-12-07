# git初级使用 --- 概念和命令


## 一、基本概念

### 1. Commit & Snapshot & Hash

commit 为 git 的操作单元。

* commit 记录了版本变动的信息
* 每个 commit 都会生成一个 snapshot
* 每个 snapshot 都以 唯一的 hash 表示
* hash 的生成基于文件夹以及文件夹下地文件信息
* commit 是个链式结构


> [拓展阅读](http://eagain.net/articles/git-for-computer-scientists/)


### 2. Branch & Pointer

* Branch 是指向某个 commit 的 Pointer
* 可以有N个Pointer，所以可以有N个Branch

[参考](http://git-scm.com/book/en/v1/Git-Branching-What-a-Branch-Is)

### 3. Repository

* 所有代码以及git对象的存放集合
* .git/ 文件夹

## 二、Repository 内操作

### 命令

#### 1. Repository

	// init at local
	git init
	// clone from remote (protocal: ftp / ssh)
    git clone


#### 2. Branch

	git branch
	
	git branch new-branch
	
	git branch -h
	
#### 3. Commit

	git add .
	
	git commit -m -a ‘message’
	

### file 状态迁移


###  Merge vs Rebase 


> 拓展： fast forward

> 拓展： merge 和 rebase 对 hash 的影响


### 冲突处理

1. 命令

		git add 

### 回退修改

1. 单文件

		git checkout filename

2. 版本回退

		git reset hash

3. 回退单个 commit (创建个revert修改)

		git revert hash


## 三、Repository 间操作

作为一个DCVS，git的远程 Repository 和本地是一样的 【可能有些差异？】。所以将 Repository 间操作单独拿出来。

### 命令

1. fetch
	
	Download objects and refs from another repository

		// usage: git fetch [<options>] [<repository> [<refspec>...]]
	
		// eg.
		git fetch origin master:master
		

2. pull = fetch + merge (rebase)

	Fetch from and integrate with another repository or a local branch
	
	Incorporates changes from a remote repository into the current branch. In its default mode, git pull is shorthand for git fetch followed by git merge FETCH_HEAD.
	
		// git pull [-n | --no-stat] [--[no-]commit] [--[no-]squash] [--[no-]ff] [--[no-]rebase|--rebase=preserve] [-s strategy]... [<fetch-options>] <repo> <head>...
		// eg.
		git pull origin master

3. push

	Update remote refs along with associated objects
		
		// usage: git push [<options>] [<repository> [<refspec>...]]
		
		// eg.
		git push origin master:master
		

4. clone

	Clone a repository into a new directory






