# mmpic
python爬取美女图片站，djongo框架构建web站点展示图片

mmpic修改版

## 演示站
[52mmpic.com](http://www.52mmpic.com)

## 安装教程
### 1.环境配置
```sh
#安装mysql
如对LINUX不熟悉，建议使用宝塔面板一键安装
Mysql版本建议 > 5.6

安装宝塔面板：
wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh

如果没有wget，则运行安装
yum -y install wget

p.s 进入centos的root用户命令：
sudo su

#安装EPEL和IUS软件源
#yum -y install epel-release
#yum -y install https://centos7.iuscommunity.org/ius-release.rpm

#安装Python3.6
yum -y install python36

#创建python3连接符
#ln -s /usr/bin/python3.6 /usr/bin/python3

#安装pip3
yum -y install python36-pip

#创建pip3链接符
ln -s /usr/bin/pip3.6 /usr/bin/pip3

#安装python-dev
yum install python36-devel

```

### 2.克隆程序
```sh
为保持与源码配置一致，请将源码克隆至/root目录下。

如果要放置到其他目录，请自行打开uwsgi.ini进行配置修改。
git clone https://github.com/initialf2020/52mmpic.git

进入程序目录
cd mmpic

安装程序依赖
pip3 install -r requirements.txt
```

### 3.程序设置
```sh
1、修改silumz下settings.py文件中数据库的配置

DATABASES = {
'default': {
'ENGINE': 'django.db.backends.mysql',
'NAME': '数据库名',
'USER': '数据库用户名',
'PASSWORD': ‘数据库密码',
'HOST': '127.0.0.1',
'PORT': '3306',
    }
}

2、将模板目录下的pagination.html文件放入python安装目录的/site-packages/dj_pagination/templates/pagination/下
（centos7 cp pagination.html /usr/lib/python3.6/site-packages/dj_pagination/templates/pagination/)

3.导入数据库文件
导入数据库文件mmpic.sql到mysql数据库

4.运行程序
uwsgi --ini uwsgi.ini

-4.1 提示”bash: uwsgi: command not found“
 找出uwsgi位置，执行命令 find / -name uwsgi
 比如得到 /usr/local/bin/uwsgi
 链接命令 ln -s /usr/local/bin/uwsgi /usr/bin/uwsgi

5.访问网站
浏览器访问 ip:8000 可以正常访问即搭建成功
访问前请确保服务器防火墙已开启8000端口

如果发现端口被占用了，执行命令
fuser -k 80/tcp
查看80端口被谁占用了，然后执行
kill -9 进程ID
杀掉对应的进程
然后注意要开通80端口的安全组策略

```

## 爬虫文件说明

1. 爬虫位于crawler目录下，每一个文件都是独立的，可单独执行。
1. 爬虫主要修改对应的数据库名、数据库用户名及密码。
1. 例： python3 mzt.py
1. 注意脚本一定要在/root/mmpic/crawler/目录下执行，否则会导致写入的文件读取不到

## 修改模板文件

1. 修改settings.py文件中的 'mmpic' 为 templates目录下模板文件名
'DIRS': [os.path.join(BASE_DIR, 'templates'+"/"+"mmpic")]
2. 将模板目录下的pagination.html文件放入python安装目录的/site-packages/dj_pagination/templates/pagination/下
（centos7 cp pagination.html /usr/lib/python3.6/site-packages/dj_pagination/templates/pagination/)
