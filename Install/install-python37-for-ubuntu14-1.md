function update_openssl() {
    cd ${ROOTPATH}
    pushd ${ROOTPATH}/packages/PythonRelevant
    tar zxf libressl-2.8.2.tar.gz
    cd libressl-2.8.2
    ./config --prefix=/usr/local/ssl
    make && make install

    mv /usr/bin/openssl /usr/bin/openssl.bak
    mv /usr/include/openssl /usr/include/openssl.bak
    ln -s /usr/local/ssl/bin/openssl /usr/bin/openssl
    ln -s /usr/local/ssl/include/openssl /usr/include/openssl
    echo "/usr/local/ssl/lib" > /etc/ld.so.conf.d/libressl-2.8.2.conf 
    ldconfig
    ldconfig -v | fgrep libressl
    openssl version -a
    popd
}

# update-alternatives usage:
#     update-alternatives --list python
#     update-alternatives --config python
#     update-alternatives --remove python /usr/bin/python3.4
function python_relevant() {
    cd ${ROOTPATH}
    pushd ${ROOTPATH}/packages/PythonRelevant
    tar zxf Python-3.7.0.tgz
    cd Python-3.7.0
    export LDFLAGS="-L/usr/local/ssl/lib"
    export CPPFLAGS="-I/usr/local/ssl/include"
    export PKG_CONFIG_PATH="/usr/local/ssl/lib/pkgconfig"
    ./configure --enable-shared CFLAGS=-fPIC
    make && make altinstall
    echo "export PATH=\$PATH:/usr/local/python37/bin" >> ~/.bash_profile
    source ~/.bash_profile

    echo "/usr/local/python37/lib" >> /etc/ld.so.conf.d/python3.conf
    ldconfig
    ldconfig -v | fgrep python
    cd -
    python2.7 ${ROOTPATH}/packages/PythonRelevant/get-pip.py 
    python3.7 ${ROOTPATH}/packages/PythonRelevant/get-pip.py 
    update-alternatives --install /usr/bin/python python /usr/bin/python2.7 10
    update-alternatives --install /usr/bin/python python /usr/local/python37/bin/python3.7 5
}

/usr/bin/openssl version -a | grep 1.0.1 && update_openssl
which python3.7 || (python_relevant && pythonlib_relevant)
