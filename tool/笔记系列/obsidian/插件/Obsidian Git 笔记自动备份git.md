我们可以通过插件 `Obsidiam Git` 定时备份笔记到 `github` .

这是我本地的config 配置

```shell
[core]
	repositoryformatversion = 0
	filemode = false
	bare = false
	logallrefupdates = true
	symlinks = false
	ignorecase = true
[remote "origin"]
	url = git@personal:oneredka/obs.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
	remote = origin
	merge = refs/heads/main
[user]
	name = hong
	email = gg.hilock@gmail.com
```


