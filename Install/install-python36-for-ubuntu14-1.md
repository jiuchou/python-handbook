# Ubuntu14.04 编译安装 Python3.6

> 本文适用于Python3.6版本（本文档内容基于Python3.6.8版本演示），不适用Python3.7。
>
> 版本说明：
>
> * Ubuntu系统：Ubuntu14.04.3 LTS, Trusty Tahr
> * Python版本：python3.6

## 1 获取安装包

* 官网地址： https://www.python.org/downloads/release/python-368/

```bash
wget https://www.python.org/ftp/python/3.6.8/Python-3.6.8.tar.xz
```

## 2 编译安装

* 官方指南 `Using Python on Unix platforms`： https://docs.python.org/3.6/using/unix.html

官方介绍如下

>If you want to compile CPython yourself, first thing you should do is get the [source](https://www.python.org/downloads/source/). You can download either the latest release’s source or just grab a fresh [clone](https://devguide.python.org/setup/#getting-the-source-code). (If you want to contribute patches, you will need a clone.)
>
>The build process consists in the usual
>
>```bash
>./configure
>make
>make install
>```
>
>invocations. Configuration options and caveats for specific Unix platforms are extensively documented in the [README.rst](https://github.com/python/cpython/tree/3.6/README.rst) file in the root of the Python source tree.
>
>```
>Warning: `make install` can overwrite or masquerade the `python3` binary. `make altinstall` is therefore recommended instead of `make install` since it only installs `*exec_prefix*/bin/python*version*`.
>```

翻译过来就是

> 如果你想要自己编译安装 `Python`， 首先你需要获取发行版源码包。你也可以下载最新的发行版本源码包或者从代码仓库下载最新版本的源码。（如果你想要安装补丁，你可能需要从代码从库下载最新版本的源码）
>
> 通常情况下，编译步骤包括
>
> ```
> ./configure
> make
> make install
> ```

不覆盖原有机器上的Python版本，安装独立的Python版本。将Python3.6安装到 `/opt/python3.6` 目录下，操作内容如下

```bash
mkdir -p /opt/python3.6
tar xf Python-3.6.8.tar.xz -C /opt
cd /opt/Python-3.6.8
# --prefix 参数指定 Python 安装目录
./configure --prefix=/opt/python3.6
make
make install
```
