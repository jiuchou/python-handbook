# 打包发布

* 参考
  * [以正确的方式开源 Python 项目](https://www.oschina.net/translate/open-sourcing-a-python-project-the-right-way)

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

