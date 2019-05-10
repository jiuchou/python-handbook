## 3 问题

* https://msd.misuland.com/pd/2884249965817760090?page=1
* https://blog.csdn.net/tanmx219/article/details/86518446

使用 `make` 编译完成后，控制台日志显示如下内容：

```
Python build finished successfully!
The necessary bits to build these optional modules were not found:
_bz2                  _curses               _curses_panel      
_dbm                  _gdbm                 _hashlib           
_lzma                 _sqlite3              _ssl               
_tkinter              _uuid                 readline           
To find the necessary bits, look in setup.py in detect_modules() for the module's name.


The following modules found by detect_modules() in setup.py, have been
built by the Makefile instead, as configured by the Setup files:
_abc                  atexit                pwd                
time                                                           
```

出现上述日志内容，表明机器中库依赖缺失，需进行安装库依赖。使用 `aptitude search gdbm` 搜索对应的包，使用 `apt-get` 进行安装，一般安装包名为 `libpackagename-dev`。



对应表如下

```bash
# _bz2 库
apt-get install libbz2-dev
_curses、_curses_panel
# _dbm/_gdbm 库
apt-get install libgdbm-dev
# _lzma 库
apt-get install liblzma-dev
# _sqlite3 库
apt-get install libsqlite3-dev
# _ssl 库（未生效）
apt-get install libssl-dev
# _tkinter 库
apt-get install tk-dev
# readline 库
apt-get install libreadline-dev
```



提示 `INFO: Can't locate Tcl/Tk libs and/or headers`

```bash
root@ubuntu:/opt/python3.7# apt-get install tk-dev
...
The following extra packages will be installed:
  libfontconfig1-dev libfontenc1 libfreetype6 libfreetype6-dev libpng12-0
  libpng12-dev libtcl8.6 libtk8.6 libutempter0 libxaw7 libxcb-shape0
  libxext-dev libxft-dev libxft2 libxmu6 libxrender-dev libxss-dev libxss1
  libxv1 libxxf86dga1 pkg-config tcl tcl-dev tcl8.6 tcl8.6-dev tk tk8.6
  tk8.6-dev x11-utils x11proto-render-dev x11proto-scrnsaver-dev
  x11proto-xext-dev xbitmaps xterm
Suggested packages:
  libxext-doc tcl-doc tcl-tclreadline tcl8.6-doc tk-doc tk8.6-doc mesa-utils
  xfonts-cyrillic
The following NEW packages will be installed:
  libfontconfig1-dev libfontenc1 libfreetype6-dev libpng12-dev libtcl8.6
  libtk8.6 libutempter0 libxaw7 libxcb-shape0 libxext-dev libxft-dev libxft2
  libxmu6 libxrender-dev libxss-dev libxss1 libxv1 libxxf86dga1 pkg-config tcl
  tcl-dev tcl8.6 tcl8.6-dev tk tk-dev tk8.6 tk8.6-dev x11-utils
  x11proto-render-dev x11proto-scrnsaver-dev x11proto-xext-dev xbitmaps xterm
The following packages will be upgraded:
  libfreetype6 libpng12-0
...
```

## 4 扩展

Python3.7 

### _ssl 库缺失

`make` 出现如日志

```
Could not build the ssl module!
Python requires an OpenSSL 1.0.2 or 1.1 compatible libssl with X509_VERIFY_PARAM_set1_host().
LibreSSL 2.6.4 and earlier do not provide the necessary APIs, https://github.com/libressl-portable/portable/issues/381
```

**OpenSSL**

* https://www.openssl.org/

**libressl**
