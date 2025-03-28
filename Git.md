<h1 style="text-align: center;">Git版本控制</h1>

### 查询：
1.查询仓库中已经存在的版本：
```cmd
git tag -l
```
2.同步远程仓库标签（版本）：
```cmd
git fetch --tags
```

### 上传：
1.初始化本地仓库信息：
```cmd
cd 目录
git init
git config --global user.name "RyanLee-Ch"
git config --global user.email "ryanlee990929@gmail.com"
```
2.配置`.gitignore`更新忽略文件：
```md
11
```
3.文件添加至暂存区：
```cmd
git add .
```
4.创建版本：
```cmd
git commit -m "当前版本说明
git remote add origin 仓库https链接
git branch -M main
```
5.推送至Github仓库：
```cmd
git push -u origin main
```
5.创建版本号和标签：
```cmd
git tag -a v版本号 -m "当前版本说明"
```
6.推送标签：
```cmd
git push origin --tags
```

### 更新
1.进入项目目录
```cmd
cd 项目目录：
```
2.推送新版本；
```cmd
git add .
git commit -m "新版本说明"
git push origin main
```
3.创建新标签：
```cmd
git tag -a v版本号 -m "新版本说明"
git push origin --tags
```

### 版本回退
1.进入项目目录：
```cmd
cd 项目目录：
```
1.回退：
```cmd
git checkout main
git reset --hard v版本号
```
2.清理为跟踪文件：
```cmd
git clean -fd
```