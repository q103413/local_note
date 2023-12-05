# git强制更新并覆盖本地修改

1.git fetch --all //从远程拉取最新的代码 不merge

2.git reset --hard origin/develop //使用指定分支的代码（此处develop）强制覆盖代码

3.git pull //从远程拉取最新的代码 自动merge