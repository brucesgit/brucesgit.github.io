
# 我的博客 —— github+hexo

## 环境
1. 安装 hexo 
   `npm install hexo-cli -g`

## 使用方法

源码存放在 `hexo` 分支，`hexo deploy` 命令执行的提交目标为`master` 分支。

### 更新博客方法

每次只要更新`hexo`分支的代码即可，提交博客步骤:

1. `hexo new 'new blog'`, 编辑对应的 new-blog.md 文件  
2. `hexo server`  部署到本地
3. `hexo clean`, 清理public文件夹  
4. `hexo g`, 生成静态文件  
5. `hexo deploy`, 发布到github

### 迁移方法

在新的设备上部署博客

1. `git clone https://github.com/lovanya/lovanya.github.io.git` 克隆库
2. `cd lovanya.github.io/` 进入博客目录
3. `git checkout hexo` 切换到 hexo 分支
4. `git clone -b v5.1.4 https://github.com/iissnan/hexo-theme-next themes/next
` 安装 next 5.1.4 版本的主题
5. `npm install or yarn install` 安装依赖
6. 发布博客方法参照*更新博客方法*  
7. 提交源码
    ``` bash
    git add .
    git commit -m "add files"
    git push origin hexo
    ```

### 部署问题

部署的时候要是出现错误 `in unpopulated submodule '.deploy_git'` 则

```bash
rm -rf .deploy_git
hexo g
hexo d
```

### 配置主题

在 `source/_data/next.yml`下配置 next 主题，不要在`themes/next/_config.yml` 下配置，这样才能将配置保存到 github。这种方式要求 hexo 的版本必须为 3 以上

博客在线地址为 https://lovanya.github.io
