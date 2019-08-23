### 贴吧打印机

将贴吧的帖子打印成epub电子书。当年在贴吧追过的小说看过的漫画可以保留下来慢慢看了……


利用tieba-to-epub项目:https://github.com/lexdene/tieba-post-to-epub

目前只有两个star，用户不知道有几个……

**Install**

```shell
pkg install libxml2 libxml2-dev libxslt libxslt-dev openssl libffi libffi-dev openssl-tool openssl-dev fftw fftw-dev libzmq libzmq-dev freetype freetype-dev pkg-config scrypt libcrypt libcrypt-dev ccrypt libgcrypt libgcrypt-dev libpng libpng-dev clang python-dev python libiconv-dev -y
pip install lxml
pip install -U tieba-to-epub
```

**Use**

获取一个帖子的id

例子：

https://tieba.baidu.com/p/4949361390?lp=5027&mo_device=1&is_jingpost=1&pn=0&

id:4949361390

```shell
tieba-to-epub 4949361390 dark.epub
```





