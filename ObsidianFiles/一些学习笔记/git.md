# 将本地项目上传至GitHub
1.  在GitHub上新建一个repository（仓库）
2. 设置git用户名和邮箱
	```
	git config –global
	```
3. 在GitHub上设置SSH Key
4. 对应项目文件夹下
	 ```
	 git init
	 ```
5. 
	```
	git add .
	```
6. 提交至本地仓库
	```
	git commit -m "提交文件"
	```
7. 上传至远程仓库
	```
	git remote add origin git@github.com:xltangcs/MarkdownFiles.git
	git push -u origin master
	```

# git GUI 中文乱码问题

edit
option
修改为 utf-8

