RG-thesis-template
![](https://github.com/im-neko/RG-Thesis-Template/workflows/build/badge.svg)
=====
RGの卒論TeXテンプレート
chike0905さんが作ったやつをdockerで動くようにして環境構築不要にしました。  
環境部分以外はそのままです。  
SFSにアップロードするくんを追加しました． 
詳細はこちらを見てください  
https://github.com/Im-neko/RG-Thesis-Template/tree/master/sotsuron-push#readme


# Requirement

* Docker

# Usage

## 1. Fork this repository

Fork this repository to your account.
When you push your changes to the forked repository, this repository provides URL to download your thesis PDF file.

## 2. Write your thesis

* Latex files to edit is exists under the "src" directory.
* Use files under the "bib" directory to list citations.

## 3. Execute docker command with shell script file.

`sh ./make.sh`

## 4. Publish and share your thesis

Now, you can publish your thesis on the internet and share it to requiest reviews.
To do this, just commit all changes on your directory and push it to your forked directory.

```bash
$ git add -u
$ git commit -m "Your commit message here."
$ git push origin gh-pages:gh-pages
```

Anyone can download and review your newest thesis on http://your_github_username.github.io/thesis/thesis.pdf now!

## 5.VSCode setting file
VSCodeで自動コンパイルするようのセッティングファイルを追加しました．
LaTex WorkShopを追加後以下の内容でsetting.jsonを上書きするとdockerのlatex環境を利用した自動コンパイルを行ってくれる．
```
{
    "latex-workshop.latex.recipes": [
      {
        "name": "compile",
        "tools": [
          "platex",
          "pbibtex",
          "platex",
          "platex",
          "dvipdfmx"
        ]
      }
    ],
    "latex-workshop.latex.tools": [
      {
        "name": "platex",
        "command": "docker",
        "args": [
          "run",
          "--rm",
          "-v",
          "%DIR%:/workdir",
          "paperist/alpine-texlive-ja",
          "platex",
          "%DOC%"
        ]
      },
      {
        "name": "pbibtex",
        "command": "docker",
        "args": [
          "run",
          "--rm",
          "-v",
          "%DIR%:/workdir",
          "paperist/alpine-texlive-ja",
          "pbibtex",
          "%DOC%"
        ]
      },
      {
        "name": "dvipdfmx",
        "command": "docker",
        "args": [
          "run",
          "--rm",
          "-v",
          "%DIR%:/workdir",
          "paperist/alpine-texlive-ja",
          "dvipdfmx",
          "%DOC%"
        ]
      }
    ],
    "latex-workshop.latex.autoBuild.run": "onFileChange",
    "latex-workshop.docker.enabled": true,
    "latex-workshop.view.pdf.viewer": "browser",
    "window.zoomLevel": 0,
  }
```
