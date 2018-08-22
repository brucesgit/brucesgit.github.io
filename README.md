# 我的博客 —— github+hexo
## 使用方法

> 源码存放在 `hexo` 分支，`hexo deploy` 命令执行的提交目标为`master` 分支。

### 更新博客方法

> 每次只要更新`hexo`分支的代码即可，提交博客步骤:

1. `hexo new 'new blog'`, 编辑对应的 new-blog.md 文件  
2. `hexo clean`, 清理public文件夹  
3. `hexo g`, 生成静态文件  
4. `hexo deploy`, 发布到github  

### 迁移方法

> 在新的设备上部署博客

1. `git clone https://github.com/lovanya/lovanya.github.io.git` 克隆库
2. `cd lovanya.github.io/` 进入博客目录
3. `npm install or yarn install` 安装依赖
4. 发布博客方法参照*更新博客方法*

> 博客在线地址为 https://lovanya.github.io