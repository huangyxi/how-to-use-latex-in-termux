# How to use LaTeX in Termux (Android's Linux Terminal)

```shell_session
#install texlive
apt install texlive

#change remote repository to TUNA
tlmgr option repository https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet

#update tlmgr
tlmgr update --all

#install fontconfig-utils to use fc-list
apt install fontconfig-utils

#make new directory to store fonts from Windows
mkdir -p /data/data/com.termux/files/usr/share/fonts/WinFonts

#copy fonts from Windows to termux directory
cp [YOUR_WIN_FONTS_PATH/*] /data/data/com.termux/files/usr/share/fonts/WinFonts

cd /data/data/com.termux/files/usr/share/fonts/WinFonts

#add Windows fonts to termux
fc-cache -f -v

cd

tlmgr install --reinstall --with-doc --with-src l3packages
tlmgr install --with-doc --with-src ctex

mkdir test\

cd test\



```
