# bishopmarcel.github.io

### 利用 GitHub Pages 搭建个人博客流程

~~~
1. Create a new repository
        bishopmarcel.github.io
        Add a README file
	
2. New SSH keys
        git config --global user.name "bishopmarcel"
        git config --global user.email "bishopmarcel@163.com"
        git config --global --list
        
        # 方便后续推送
        ssh-keygen -t rsa -C "bishopmarcel@163.com"
        .ssh/id_rsa.pub
	
3. Clone
        git clone git@github.com:bishopmarcel/bishopmarcel.github.io.git
	
4. Branch
		# 切换目录
		cd bishopmarcel.github.io
        # 新建分支
        git branch gh-pages
        
        [git checkout gh-pages]
        [git branch]
        
        # 推送分支
        git push -u origin gh-pages
        
        # 移除分支
        # 切换到删除分支外的分支
        [git checkout main]
        # 删除分支
        [git branch -d gh-pages]
        # 强制删除分支
        [git branch -D gh-pages]
        # 删除远程分支
        [git push origin --delete gh-pages]
        # 简化命令删除远程分支
        [git push origin :gh-pages]

5. GitHub Pages
		https://github.com/bishopmarcel/bishopmarcel.github.io/settings/pages
		GitHub Pages > Build and deployment > Branch > gh-pages > Save

5. .gitignore
        .idea/
        blog/node_modules/
        blog/public/
        blog/db.json

6. Hexo
        npm install hexo-cli -g
        hexo init blog
        cd blog
        npm install
        npm install hexo-deployer-git --save
        
        [hexo new "My First Blog"]
        [hexo generate]
        [hexo server]
        
        _config.yml
        ...
        # Deployment
        ## Docs: https://hexo.io/docs/one-command-deployment
        deploy:
          type: 'git'
          repo: git@github.com:bishopmarcel/bishopmarcel.github.io.git
          branch: gh-pages
        
        # blog/_config.fluid.yml 文件内容 与 blog/_config.yml 保持一致
          
        hexo generate -d
        # 简写
        [hexo g -d]
        
 8. Visit site
        https://bishopmarcel.github.io/
~~~