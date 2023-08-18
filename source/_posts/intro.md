---
title: GithubPages 部署 Hexo 指南
---

1. 新建一个 github 仓库，仓库名：`username.github.io`

   > `username` 是你 `github` 的用户名

2. 将hexo 文件夹中的文件推送到github默认分支，默认分支通常名为 `main`

   ```git
   git push -u origin main
   ```

3. 查看`node`版本，几下版本号(例如：`v16.y.z`)

   ```bash
   node --version
   ```

4. 在项目根目录下中创建`.github/workflows/pages.yml`文件，填入一下内容（将`16`替换为上个步骤记下的版本号）

   ```yaml
   name: Pages
   
   on:
     push:
       branches:
         - main # default branch
   
   jobs:
     pages:
       runs-on: ubuntu-latest
       permissions:
         contents: write
       steps:
         - uses: actions/checkout@v2
         - name: Use Node.js 16.x
           uses: actions/setup-node@v2
           with:
             node-version: "16"
         - name: Cache NPM dependencies
           uses: actions/cache@v2
           with:
             path: node_modules
             key: ${{ runner.OS }}-npm-cache
             restore-keys: |
               ${{ runner.OS }}-npm-cache
         - name: Install Dependencies
           run: npm install
         - name: Build
           run: npm run build
         - name: Deploy
           uses: peaceiris/actions-gh-pages@v3
           with:
             github_token: ${{ secrets.GITHUB_TOKEN }}
             publish_dir: ./public
   ```

5. 部署页面, 首先在项目根目录安装`hexo-deployer-git`

   ```bash
   npm i hexo-deployer-git
   ```

   在`_config.yml` 文件中添加一下配置

   ```yaml
   deploy:
     type: git
     repo: https://github.com/<username>/<project>
     # example, https://github.com/hexojs/hexojs.github.io
     branch: gh-pages
   ```

   执行命令开始部署

   ```bash
   hexo clean && hexo d
   ```

6. 当部署作业完成后，产生的页面会放在储存库中的 `gh-pages` 分支。

7. 在储存库中前往 `Settings > Pages > Source`，并将 branch 改为 `gh-pages`。

   `Settings > Pages > General > Deault branch`，也改为`gh-pages`   

8. 重新执行部署命令

   ```bash
   hexo clean && hexo d
   ```

9. 在浏览器输入：`username.github.io` 查看网站（有时候需要清理缓存或者稍等1分钟左右）

## 更换Hexo主题

1. https://hexo.io/themes/ 官网找到一个自己喜欢的主题

2. 本网站使用`hexo-theme-bear`主题 (https://github.com/gary-Shen/hexo-theme-bear)

3. 在 `github` 上 `fork`  主题仓库

4. `git clone` 下载 `fork` 的主题仓库到本地，按自己的喜好修改`_config.yml`文件后上传

5. `hexo-theme-bear`主题需要安装的依赖`hexo-rnder-pug`

   ```bash
   npm i hexo-render-pug
   npm i
   ```

6. 下载主题到项目 （clone 地址更换成你fork的地址）

   ```bash
   cd your-hexo-site
   git clone https://github.com/gary-Shen/hexo-theme-bear themes/bear
   ```

7. 修改`_config.yml`文件更换主题

   ```bash
   theme:bear
   ```

8. 上传代码到github，执行部署命令

   ```bash
   git push -u origin main
   hexo clean && hexo d
   ```



🎊恭喜，登录到网站上查看下吧。