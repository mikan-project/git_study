---
title: "リポジトリを作ってみよう"
weight: 7
---

ここまできたら、あとはコマンドを使えるようになるだけです。そんな難しくないですよ！

Git を使えるようになるにあたって、**リポジトリィ**というのはとても重要な概念です。

リポジトリとは、以下のようにバージョンを管理するプロジェクトごとに作られ、その中の各ファイルの変更履歴の他、issue やブランチの情報が入っています。

<img src="/repository.png" width="450px"/>

下のように、各エンジニアは Github 上にある（自分で作った）リポジトリを自分の PC に取り込み（**clone**と言います）、リポジトリの中のファイルを変更してそれを Github に送ります（**push**といいます）。

## さあ、やってみよう！

Github 上に repository を作ってみましょう。以下のメニューにある`New repository`をクリックします。

<img src="/new_repository.png" width="600px" />

以下にリポジトリ名や、世の中に公開するか許可した人じゃないとみれないようにするか（`plivate`か`public`か）などを選択します。

<img src="/settings_repository.png" width="500px" />

できた！

<img src="/created_repository.png" width="500px" />

### ローカルにリポジトリを作る

何らかのファイルが入っているディレクトリを用意します。例えば、

```
> ls
hoge.txt huga.png
```

みたいな感じ。その状態で、以下のコマンドを打ちます。（上記画像に指定されているのと同じです）

```
> git init
> git add .
> git commit -m "initial commit"
> git branch -M main
// [自分の作ったリポジトリのURL].git です。
> git remote add origin https://github.com/hogehoge/hugahuga.git
> git push -u origin main
```

できたら、先ほど作ったリポジトリのページにアクセスしてください。ファイルが公開されていますか。
