---
title: "Githubの実践的な使い方"
weight: 15
---

さて、git についてある程度理解し、contribute できたところで、より実践的な手法について学んでいきましょう。

まずは、Github についてです。

## Github Actions

この説明のためには、まず **CI/CD**について理解しておく必要があります。Circle Ci とか聞いたことがある方もいらっしゃるかもしれません。同じようなものです。

- **CI** は、Continuous Integration の略で、継続的インテグレーションと訳されます。
  チーム開発の際に複数のブランチで並行作業が行われるとします。その際、それぞれで「build が正常に行くこと」や「意図した挙動を正常に示すこと（テストが通ること）」を検証しながら進めていく必要があります。

  例えば「PR を発行した時」や「リモートリポジトリに push した時」に自動で CI を検証することで、コードの安全性を担保したり、開発効率化をすることができます。

- **CD** は、Continuous Deployment の略で、継続的デプロイメントと訳されます。
  これは、CI を自動で行うだけでなく、その後のリリースまでも自動化する、ということです。

Github Actions というのは、PR や commit をトリガーとして、CI/CD を自動で行ってくれるサービスになります。主にリポジトリごとに設定します。例えば以下のような感じです。

`.github/workflows/deploy.yml`

```

name: CI

on:
  push:
    branches: [ main ] // mainブランチにpushされた時（マージされた時）

jobs:
  deploy:
    name: Deploy to Firebase
    runs-on: ubuntu-latest // 最新のubuntuコンテナで実行させます
    steps:
    - name: Checkout Repo
      uses: actions/checkout@v1
    - name: setup Node
      uses: actions/setup-node@v1 // nodeの設定をしてくれる
      with:
        node-version: 16.x
    - name: Create .env file
      run: echo "${{ secrets.ENV_PROD }}" > .env // 環境変数の設定をしたり
    - name: Install Dependencies
      run: yarn // ライブラリをインストールしたり
    - name: Install firebase tools
      run: yarn global add firebase-tools
    - name: build
      run: yarn build // buildする
    - name: deploy to Firebase Hosting
      run: yarn deploy --token=${{ secrets.FIREBASE_TOKEN }} // デプロイする
```

このような設定をリポジトリに書いておくことで、より快適な開発を行うことができます。

## Issue や PR のテンプレートを作る

Issue や PR のテンプレートを設定することも可能です。`.github/`ディレクトリないに設定します。

`.github/PULL_REQUEST_TEMPLATE.yml`

```
## 対応したIssue
- URL

## 変更内容
- 簡潔に箇条書きで

## スクリーンショット(オプション)
必要であればスクリーンショットを添付

## 動作確認方法
- 修正内容にしてどのような動作確認をしたか（テスト）
```
