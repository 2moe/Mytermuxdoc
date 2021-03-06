# Prepare

首先安装CPython包。

```shell
pkg i python -y
```

Python2的生命周期已经接近结束了，建议不再使用Python2。

CPython是使用最广的Python解释器，但是它默认的repl不太友好。建议在`ipython`, `ptpython`,`bpython`中选择一个。`xonsh`是一个兼容BASH和Python语法的shell，功能较少但更轻量方便，也可以做为选择之一。要为xonsh加入语法高亮支持，只需执行：

```shell
pip install xonsh prompt-toolkit
```

如果一定要使用默认的repl，那么

>记好了，默认的python repl不会自动缩进，在需要缩进时，得手动输4个空格。而且每行都要...

**免费书籍**

`<Think Python>`

`<interpy>`

**lxml**

```shell
#python-lxml
function pylxml_install
{
pkg install libxml2 libxml2-dev libxslt libxslt-dev openssl libffi libffi-dev openssl-tool openssl-dev fftw fftw-dev libzmq libzmq-dev freetype freetype-dev pkg-config scrypt libcrypt libcrypt-dev ccrypt libgcrypt libgcrypt-dev libpng libpng-dev clang python-dev libiconv-dev -y
pip install lxml
}
```

**科学计算**

包括Numpy,pandas,matplotlib，SciPy等包。

```shell
#See also: https://github.com/termux/termux-packages/issues/136
#issue include install numpy matplotlib and pandas

function its-pointless-repo_install
{
cat <<EOF
This repo Generated by its-pointless@github
EOF
pkg install coreutils gnupg wget -y
mkdir -p $PREFIX/etc/apt/sources.list.d
# Write the needed source file
echo "deb https://its-pointless.github.io/files/ termux extras" > \
		$PREFIX/etc/apt/sources.list.d/pointless.list
wget https://its-pointless.github.io/pointless.gpg -O $PREFIX/tmp/pointless.gpg
apt-key add $PREFIX/tmp/pointless.gpg
apt update
}



#matplotlib
function matplotlib_install
{
pkg install libpng libpng-dev freetype freetype-dev pkg-config make -y
LDFLAGS="-lm -lcompiler_rt" pip install matplotlib
}


#numpy
function numpy_install
{
pkg install clang python python-dev make -y
ln -s ${PREFIX}/include/freetype2/freetype ${PREFIX}/include/freetype
#解决找不到freetype.h
LDFLAGS="-lm -lcompiler_rt" pip install numpy
}

#pandas
function pandas_install
{
numpy_install
LDFLAGS="-lm -lcompiler_rt" pip install pandas
}

#scipy
function scipy_install
{
its-pointless-repo_install
pkg install scipy
}
```

**opencv**

```shell

#python opencv
function opencv_install
{
its-pointless-repo_install
pkg install opencv -y
}
```

**零散Python包**

```shell
function pygevent_install
{
pkg install clang python2 python2-dev libevent libcrypt-dev libcrypt -y
pip2 install gevent
}





#Python-scrapy
#install
function scrapy_install
{
#scrapy依赖于lxml
pylxml_install
#installation
#事实上，是cryptography引发了麻烦
pkg install python python-dev clang libffi-dev libxml2-dev libxslt-dev openssl openssl-dev openssl-tool -y
ln -s $PREFIX/include/libxml2/libxml $PREFIX/include/libxml
pip install cryptography --no-binary cryptography
pip3 install scrapy
}

#cryptography

function cryptography_install
{
pkg install python python-dev clang libffi-dev openssl openssl-dev openssl-tool -y
ln -s $PREFIX/include/libxml2/libxml $PREFIX/include/libxml
pip install cryptography --no-binary cryptography
}

Python-pynacl
#install
function pynacl_install
{
pkg install clang python python-dev libsodium libsodium-dev -y
export SODIUM_INSTALL=system
pip install pynacl
}




#Python-pillow
#install
#You do not need to install all supported external libraries to use Pillow’s basic features. Zlib and libjpeg are required by default.
#Pillow有很多可选的库，详情见doc
function pillow_install
{
pkg install python python-dev ndk-sysroot clang make libjpeg-turbo-dev zilb-dev -y
pip install pillow
}



#Python-jupyter
#Jupyter notebook（http://jupyter.org/） 是一种 Web 应用，能让用户将说明文本、数学方程、代码和可视化内容全部组合到一个易于共享的文档中。
#install
function jupyter_install
{
pkg install clang python python-dev fftw libzmq libzmq-dev -y
LDFLAGS="-lm -lcompiler_rt" pip install jupyter
}

#pyuv
function pyuv_install
{
#感谢pupy
pkg install python python-dev curl clang libcrypt-dev libffi-dev openssl-dev automake autoconf libtool make pkg-config libuv-dev -y
pip install --global-option 'build_ext' --global-option '--use-system-libuv' pyuv
}
 
#gmpy2
function gmpy2_install
{
pkg install libgmp-dev libmpc-dev libmpfr-dev -y
pip install gmpy2
}

```
