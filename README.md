# 1. Quarto CLI（`.deb` パッケージ）

## 1.1. アーキテクチャ確認（amd64 か arm64）
```bash
dpkg --print-architecture
```

## 1.1. Install for amd64 
```bash
VER=$(curl -s https://api.github.com/repos/quarto-dev/quarto-cli/releases/latest | grep -Po '"tag_name": "v\K[^"]*')
wget "https://github.com/quarto-dev/quarto-cli/releases/download/v${VER}/quarto-${VER}-linux-amd64.deb"
sudo dpkg -i "quarto-${VER}-linux-amd64.deb"
```

## 1.2. Install for amd64 
```bash
VER=$(curl -s https://api.github.com/repos/quarto-dev/quarto-cli/releases/latest | grep -Po '"tag_name": "v\K[^"]*')
wget "https://github.com/quarto-dev/quarto-cli/releases/download/v${VER}/quarto-${VER}-linux-arm64.deb"
sudo dpkg -i "quarto-${VER}-linux-arm64.deb"
```

## 1.3. Check
```bash
quarto --version
quarto check
```

# 2. PDF 出力用の TeX 環境（任意）
HTML のみなら不要です。PDF を出す場合:

```bash
quarto install tinytex
```

**日本語 PDF** には LuaLaTeX 系が必要です。確実なのは TeX Live の導入です:

```bash
sudo apt update
sudo apt install -y texlive-luatex texlive-lang-japanese texlive-latex-extra fonts-noto-cjk
```

# 3. コード実行用エンジン（201, 205 を動かす場合・任意）
##　3.1 Python（jupyter エンジン）
```bash
python3 -m venv .venv
source .venv/bin/activate
(venv) pip install jupyter matplotlib pandas
```

##　3.2 # R（knitr エンジン）
```bash
sudo apt install -y r-base
R
> install.packages("rmarkdown")
```

# VSCode Extension
## Quarto
```
quarto.quarto
```

## .vscode/settings.json
```
{
  "python.defaultInterpreterPath": "${workspaceFolder}/.venv/bin/python"
}
```