# 安装

## 1 安装 Python

### 1.1 windows7

### 1.2 Liunx

#### 1.2.1 Ubuntu14.04

#### 1.2.2 CentOS6

## 2 安装 Python 包

### 2.1 pip

#### 2.1.1 在线安装

* [Pip Installation](https://pip.pypa.io/en/stable/installing/)

1. pip不存在

```bash
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3.7 get-pip.py
```

2. pip存在

```bash
# 使用默认Python安装
python -m pip install PackageName(==PackageVersion)
或者
pip install PackageName(==PackageVersion)

# 使用Python2.7安装
python2.7 -m pip install PackageName(==PackageVersion)
或
pip2.7 install PackageName(==PackageVersion)

# 使用Python3.7安装
python3.7 -m pip install PackageName(==PackageVersion)
或
pip3.7 install PackageName(==PackageVersion)
```

#### 2.1.2 离线安装

wheel包安装

#### 2.1.3 旧版本安装

**python2.6安装pip**

curl https://bootstrap.pypa.io/2.6/get-pip.py -o get-pip.py
```
DEPRECATION: Python 2.6 is no longer supported by the Python core team, please upgrade your Python. A future version of pip will drop support for Python 2.6
Collecting pip<10
...
You are using pip version 9.0.3, however version 19.1 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
```

### 2.2 Django

* [Django Installation](https://www.djangoproject.com/download/)

#### 2.2.1 在线安装

```bash
pip install Django==2.1.5
```

#### 2.2.2 离线安装

### 2.3 djangorestframework

* [djangorestframework Installation](https://www.django-rest-framework.org/#installation)

#### 2.3.1 在线安装

```bash
pip install djangorestframework
```

#### 2.3.2 离线安装

### 2.4 mysqlclient

* [mysqlclient Installation](https://pypi.org/project/mysqlclient/)

#### 2.4.1 在线安装

```bash
pip install mysqlclient
```

#### 2.4.2 离线安装

### 2.5 Pillow

* [Pillow Installation](https://pillow.readthedocs.io/en/latest/installation.html)

#### 2.5.1 在线安装

```bash
pip install Pillow
```

#### 2.5.2 离线安装

### 2.10 其他

* [Installation]()

#### 2.10.1 在线安装

#### 2.10.2 离线安装

## 3 virtualenv使用

* 参考: [廖雪峰的官方网站之virtualenv](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001432712108300322c61f256c74803b43bfd65c6f8d0d0000)

### 3.1 安装

pip3 install virtualenv

### 3.2 使用

1.创建目录
```bash
mkdir myproject
cd myproject
```
2.创建一个独立的Python运行环境，命名为venv
```bash
virtualenv --no-site-packages venv
```
3.退出当前的venv环境，使用deactivate命令

