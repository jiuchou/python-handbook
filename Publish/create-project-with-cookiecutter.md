# 使用cookiecutter构建项目

> 参考：
>
> ​	[New Library Sprint](http://audreyr.gitbooks.io/new-library-sprint/content/)

## 使用cookiecutter构建项目

### Example

* 安装cookiecutter

```
D:\Reporter\python-handbook>pip install cookiecutter
# 查看版本
D:\Reporter\python-handbook>cookiecutter --version
Cookiecutter 1.6.0 from d:\windowssoftware\python37\lib\site-packages (Python 3.7)
```

* Run Cookiecutter with cookiecutter-pypackage

```bash
D:\Reporter\python-handbook\AppendixB\logger>cookiecutter https://github.com/audreyr/cookiecutter-pypackage.git
full_name [Audrey Roy Greenfeld]: jiuchou
email [audreyr@example.com]: 315675275@qq.com
github_username [audreyr]: jiuchou
project_name [Python Boilerplate]: logger
project_slug [logger]:
project_short_description [Python Boilerplate contains all the boilerplate you need to create a Python package.]: Python logger module contains all about log.
pypi_username [jiuchou]:
version [0.1.0]:
use_pytest [n]: y
use_pypi_deployment_with_travis [y]: y
add_pyup_badge [n]:
Select command_line_interface:
1 - Click
2 - No command-line interface
Choose from 1, 2 (1, 2) [1]:
create_author_file [y]:
Select open_source_license:
1 - MIT license
2 - BSD license
3 - ISC license
4 - Apache Software License 2.0
5 - GNU General Public License v3
6 - Not open source
Choose from 1, 2, 3, 4, 5, 6 (1, 2, 3, 4, 5, 6) [1]: 4
```

> 协议选择参考：
>
> ​	https://www.oschina.net/news/27273/main-os-license-comparison
>
> ​	![](D:/Reporter/python-handbook/Publish/image/%E4%B8%BB%E6%B5%81%E5%BC%80%E6%BA%90%E5%8D%8F%E8%AE%AE%E6%AF%94%E8%BE%83_1.jpg)



问题

Install过程： 配置文件未正确安装

Uninstall问题： 未清除所有安装内容

`setup.py`

```python
from setuptools import setup, find_packages

with open("README.md", "r") as f:
    long_description = f.read()
    
setup(
    name='publish',
    version=publish.__version__,
    url='http://github.com/jiuchou/python-handbook/AppendixB/publish',
    license='Apache Software License',
    author='jiuchou',
    author_email='315675275@qq.com',
    # tests_require=['pytest'],
    install_requires=[],
    # cmdclass={'test': PyTest},
    description='publish python project',
    long_description=long_description,
    packages=['publish'],
    include_package_data=True,
    platforms='any',
    # test_suite='publish.test.test_publish',
    classifiers = [
        'Programming Language :: Python',
        'Development Status :: 4 - Beta',
        'Natural Language :: English',
        'Environment :: Web Environment',
        'Intended Audience :: Developers',
        'License :: OSI Approved :: Apache Software License',
        'Operating System :: OS Independent',
        'Topic :: Software Development :: Libraries :: Python Modules',
        'Topic :: Software Development :: Libraries :: Application Frameworks',
        'Topic :: Internet :: WWW/HTTP :: Dynamic Content',
    ]
    #extras_require={
    #    'testing': ['pytest'],
    #}
)
```



## 扩展

* [Building and Distributing Packages with Setuptools](https://setuptools.readthedocs.io/en/latest/setuptools.html#id4)[¶](https://setuptools.readthedocs.io/en/latest/setuptools.html#building-and-distributing-packages-with-setuptools)
* [Packaging Python Projects](https://packaging.python.org/tutorials/packaging-projects/#packaging-python-projects)
  * [python工程代码如何打包](https://blog.csdn.net/weixin_39202719/article/details/81905326)
* [Python 库打包分发(setup.py 编写)简易指南](http://blog.konghy.cn/2018/04/29/setup-dot-py/)
* [关于python中的setup.py](http://python.jobbole.com/82077/)
* [Classifiers](https://pypi.org/classifiers/)

参考

* [以正确的方式开源 Python 项目](https://www.oschina.net/translate/open-sourcing-a-python-project-the-right-way)
* [Python中setup.py一些不为人知的技巧](https://www.cnblogs.com/yanxiatingyu/p/9278191.html)