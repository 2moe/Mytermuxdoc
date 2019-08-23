### Prepare

文本编辑器可选择Vim或Emacs，或者Emacs+Evil。当然nano,micro也可以。

启用its-pointless仓库。

```shell
pkg install coreutils gnupg wget -y
mkdir -p $PREFIX/etc/apt/sources.list.d
# Write the needed source file
echo "deb https://its-pointless.github.io/files/ termux extras" >  ${PREFIX}/etc/apt/sources.list.d/pointless.list
wget https://its-pointless.github.io/pointless.gpg -O $PREFIX/tmp/pointless.gpg
apt-key add $PREFIX/tmp/pointless.gpg
apt update
```
