查看conda配置
```
conda config --show
```
.condarc文件配置
```
channels:
  - https://mirrors.aliyun.com/anaconda/pkgs/free/
  - https://mirrors.aliyun.com/anaconda/pkgs/main/
envs_dirs:
  - D:\Software\Anaconda\envs
  - C:\Users\tangxiaolong\.conda\envs
  - C:\Users\tangxiaolong\AppData\Local\conda\conda\envs
show_channel_urls: true
auto_activate_base: false
```
修改默认环境环境时，要注意改目录是否有写入权限。

创建pytorch环境
```
conda create --name pytorch python=3.9
```

查看环境
```
conda info --envs
```

激活pytorch环境
```
activate pytorch
```

切换为pytorch环境
```
conda activate pytorch
```

安装jupyter
```
conda install -y jupyter
```

打开jupyter
```
jupyter notebook
```
#### 修改jupyter默认打开路径

查看jupyter_notebook_config文件所在位置
```
jupyter notebook --generate-config
```
打开jupyter_notebook_config，修改，去掉#
```
c.NotebookApp.notebook_dir = 'D:\JupyterNotebook'
```
右键jupyter快捷方式，属性，删除`"%USERPROFILE%/"`


















