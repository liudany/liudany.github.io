# PyCharm Remote Deployment

这次是本地建立，然后上传到服务器，和平常git clone然后下载到本地还有些不同。

1. 新建工程
2. Tools - Deployment - Configuration - Mapping 修改deployment path on server，这里要注意把你工程的名字也打上，不然会直接把项目文件传到/home/dyliu/这下面。
3. 左侧选中项目文件，然后Tools - Deployment - Upload to 自动传到刚才的路径。

4. 在Deployment - Options里，选择每次显式保存时同步文件。
5. Pycharm - Preferences - Interpreter 选择40023的远程解释器。
6. Upload时，选中你要upload的东西，就可以不用每次都上传所有的。已经上传过的就直接显式保存，同步。
7. 选中 Deployment - Configuration - Mapping 中的use this server as default，就可以c+s自动上传。

# 搭一个Jupyter Lab

```shell
pip install Jupyter #服务器安装Jupyter
jupyter notebook --generate-config #生成Jupyter配置文件
vim ~/.jupyter/jupyter_notebook_config.py #进入上述文件地址，修改配置

c.NotebookApp.ip = '0.0.0.0' #所有绑定服务器的IP都能访问，若想只在特定ip访问，输入ip地址即可
# 这里不可以是*，会报错

c.NotebookApp.port = 6666 #将端口设置为自己喜欢的吧，默认是8888
c.NotebookApp.open_browser = False #我们并不想在服务器上直接打开Jupyter Notebook，所以设置成False
c.NotebookApp.notebook_dir = '/root/jupyter_projects' #这里是设置Jupyter的根目录，若不设置将默认root的根目录，不安全
c.NotebookApp.allow_root = True # 为了安全，Jupyter默认不允许以root权限启动jupyter 
```

平常使用分为两步：

1. 服务器上开一个screen，然后启动`jupyter notebook`。设置的port是8765。

2. 在自己的电脑上，执行端口转换。

   ```shell
   ssh -N -f -L localhost:5555:localhost:8765 dyliu@202.121.180.97 -p 40023
   ```


3. 浏览器登录localhost:5555页面。

# 数据预处理

## 划分集合

要注意**分布均匀**，需要打乱了以后再切割。

## 读取CSV

用`from python import csv`来做的话，实现方式为：

```python
with open('data/train.csv', 'r') as train:
  reader = csv.reader(train)
  rows = [row for row in reader]
  text = [row[3] for row in rows[1:]]
  label = [row[4] for row in rows[1:]]
```

## 分词

先tokenize✅，然后根据频率建立词表，然后将每个句子，按照token对应的vocab中的序号转换为一个ids序列。

### 问题

要去掉标点吗？

用torchtext来建立词表会简单一些吗

## Embedding

