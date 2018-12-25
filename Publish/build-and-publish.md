# 打包发布现有项目

> 说明：
>
> 1. 无法实现安装时将配置文件拷贝到固定目录
> 2. 无法实现卸载时完全删除安装时涉及的目录

## 前提

* [以正确的方式开源 Python 项目](https://www.oschina.net/translate/open-sourcing-a-python-project-the-right-way)

## setuptools 和 setup.py文件

### setup 特殊参数说明

> packages
>
> ​	packages = []
>
> ​	packages = find_packages()
>
> include_package_data = True
>
> classifiers = []



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

* [Distributing Python Modules (Legacy version)](https://docs.python.org/2/distutils/index.html)
* [Building and Distributing Packages with Setuptools](https://setuptools.readthedocs.io/en/latest/setuptools.html#building-and-distributing-packages-with-setuptools)
* [Python Packaging User Guide](https://python-packaging-user-guide.readthedocs.org/)
* [PEP 427 -- The Wheel Binary Package Format 1.0](https://www.python.org/dev/peps/pep-0427/)
* [Packaging Python Projects](https://packaging.python.org/tutorials/packaging-projects/#packaging-python-projects)
  * [python工程代码如何打包](https://blog.csdn.net/weixin_39202719/article/details/81905326)
* [Python 库打包分发(setup.py 编写)简易指南](http://blog.konghy.cn/2018/04/29/setup-dot-py/)
* [关于python中的setup.py](http://python.jobbole.com/82077/)
* [Classifiers](https://pypi.org/classifiers/)

参考

* 
* [Python中setup.py一些不为人知的技巧](https://www.cnblogs.com/yanxiatingyu/p/9278191.html)
* [将python包发布到PyPI和制作whl文件](https://blog.csdn.net/winycg/article/details/80025432)

