# How to use LaTeX in Termux with custom fonts

1. Install TeX Live and dependences
```bash
# install texlive
apt install texlive

# install fontconfig-utils which includes `fc-list`
apt install fontconfig-utils

# change the remote repository to the mirror close to you 
tlmgr option repository https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet

# update tlmgr
tlmgr update --all
```

2. Install custom fonts
```bash
# make a new directory to store your custom fonts
CUSTOM_FONT_PATH="/data/data/com.termux/files/usr/share/fonts/YOUR_DIR_NAME"
mkdir -p "${CUSTOM_FONT_PATH}"

# copy fonts from somewhere else to the path of your custom fonts
cp [YOUR_FONTS_PATH/*] "${CUSTOM_FONT_PATH}"
chmod 744 "${CUSTOM_FONT_PATH}"/*
fc-cache -f -v

# better to export the path in ~/.bashrc
export OSFONTDIR="/data/data/com.termux/files/usr/share/fonts"

# add the font Fandol
tlmgr install fandol
```

3. Install LaTeX packages
```bash
# reinstall  l3packages
tlmgr install --reinstall --with-doc --with-src l3packages

# install ctex to parse Chinese if you need
tlmgr install --with-doc --with-src ctex
```

4. Write a LaTeX demo in file `demo.tex`
```bash
# goto a temporary directory
cd $(mktemp -d); pwd

DEMO_FILE=$demo.tex$
echo "\document{article}" > "${DEMO_FILE}"

# "font=windows" if you copied Chinese fonts from Windows
echo "\usepackage[fontset=windows]{ctex}" >> "${DEMO_FILE}"

echo "\begin{document}" >> "${DEMO_FILE}"

echo 'Hello $\LaTeX$' >> "${DEMO_FILE}"
echo "测试" >> "${DEMO_FILE}" # or in other languages 

echo "\end{document}" >> "${DEMO_FILE}"
```

5. compile the LaTeX file `demo.tex`
```bash
xelatex -synctex=1 -interaction=nonstopmode demo.tex

# install lost packages if needed
tlmgr install --with-doc --with-src LOST_PACKAGE

xelatex -synctex=1 -interaction=nonstopmode demo.tex
tlmgr install --with-doc --with-src LOST_PACKAGE

xelatex -synctex=1 -interaction=nonstopmode demo.tex
tlmgr install --with-doc --with-src LOST_PACKAGE
# ...
```

6. Open the PDF file by your Android PDF reader
```bash
termux-open demo.pdf
```
