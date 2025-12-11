## この記事のポイント

## はじめに

この記事では「この前リリースされた機能って実際に動かすとどんな感じなんだろう」とか
「もしかしたら内容次第では使えるかも？？」とか「結構前からあるけど、実際どうなんだろう」など
GitHubの中でも特定の機能にフォーカスして検証していく記事です。

今回は[機械学習のための GitHub Codespacesの概要](https://docs.github.com/ja/codespaces/developing-in-a-codespace/getting-started-with-github-codespaces-for-machine-learning)というドキュメントページがあったので

Codespaces上でJupyter環境を構築してみたり、他にJupyter環境を構築する方法がないかを調査してみます。

## 全人類が生成AIを触っているので機械学習にもフォーカスがあたっているようなそんな頃合い

生成AIが注目されている昨今、基礎技術あるいは抱合関係にある機械学習に対しての関心が高まっているかなと感じています。
でも、いざ機械学習を始めようと思っても、環境構築が難しかったり、そもそも何から始めれば良いのか分からなかったりすることも多いです。

とはいえ、手段はたくさん提供されていてたとえば、クラウドエンジニアであれば、クラウドサービスを使って機械学習環境を構築することができます。
具体的には以下のようなサービスがあります。

- Google Cloud
  - Vertex AIとBigQuery MLを使う
- AWS
  - SageMaker Studio Labを使ってJupyter環境を構築する
- Azure
  - Azure Machine Learning Studioを使う

※要件や予算に応じて、他の機能、他のクラウドサービスを使うことも可能です。Databricksや、Google Colabなどもあります。

とはいえ、これらのクラウドサービスを使うにはアカウント登録が必要である点やクラウドサービスの利用に慣れていないと、最初の一歩を踏み出すのが難しいこともあります。
※ひょっとすると、Google Colabの方が手軽かもしれませんが、誰がどんな用途で使うかによっても変わると思います。

とりあえず、機械学習環境としてJupyter環境を手軽に構築できる方法があれば、試してみたいと思う人も多いのではないでしょうか。

## 復習：Jupyter環境あるいはJupyter Notebookとは

何回か、Jupyter NotebookやJupyter環境について説明してきましたが、改めて簡単に説明します。

Jupyter Notebookは、データサイエンスや機械学習の分野で広く使われているオープンソースのウェブアプリケーションです。
Jupyter Notebookを使うとセル単位でコードの作成、実行、共有が簡単に行えます。

[参考：Project Jupyter - Home](https://jupyter.org/)

多くのJupyter環境ではこのJupyter Notebookが利用されており、インターフェイスも継承されています。
ですのでたとえば、Google Colabで作ったJupyter Notebookは、他のJupyter環境（Vertex AI Workbench、Sagemaker、AzureMLなど）でも問題なく動作します。
※各クラウドが独自で提供するサービスを使う場合は、多少の差異があるかもしれません。

なお、今回紹介するJupyterですが、JupyterLab以外にもJupyterHubといったマルチアカウント対応のJupyter環境もあります。
興味のある方は調べてみてください。

## GitHub CodespacesでJupyter環境を構築する場合

GitHub Codespacesは、クラウド上で開発環境を提供するサービスですが、Jupyter環境も構築できます。
具体的には以下の2つの方法があります。

- Jupyter templateを使う
  - https://github.com/github/codespaces-jupyter
- devcontainer.jsonを使って自分で環境を構築する

2つ目の方法はすでに他の環境でJupyterを構築したことがあるいわゆる上級者向けなので、今回は1つ目の方法を紹介します。

### Jupyter templateを使う場合

どのようにしてJupyter環境を構築するかですが、GitHub CodespacesにはJupyter用のテンプレートが用意されており
以下のURLからJupyter Notebookを選択することで簡単に構築できます。

[Codespace templates](https://github.com/codespaces/templates)

あるいはcodespaces-jupyterリポジトリのトップページから`Use this template`ボタンをクリックすることでも同様にJupyter環境を構築できます。

### え？もっと簡単にJupyter環境を構築したいって？

もっと簡単にJupyter環境を構築したい場合は、以下のリンクをクリックするだけでCodespaces上にJupyter環境が構築されます。（凄まじい便利さ）

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/github/codespaces-jupyter)

上記のリンクの作り方については以下のドキュメントを参照してください。

[参考:codespace の迅速な作成と再開を容易にする - GitHub ドキュメント](https://docs.github.com/ja/codespaces/setting-up-your-project-for-codespaces/setting-up-your-repository/facilitating-quick-creation-and-resumption-of-codespaces#github-codespaces-%E3%81%A7%E9%96%8B%E3%81%8F-%E3%83%90%E3%83%83%E3%82%B8%E3%81%AE%E4%BD%9C%E6%88%90)

ちょっとDeepな話をすると上記の機能は開発コンテナと深い関係がありますが、割愛します。
今回はCodespacesはDev Containerの設定を参照しているとだけ覚えておいてください。

## セットアップ

では、凄まじい便利さを体験してみましょう。まずは以下のリンクをクリックしてください。

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/github/codespaces-jupyter)

クリックするとCreate codespaceの画面が表示されるので、`Create new codespace`をクリックします。

![Create codespace](./images/codespace-ml1.png)

なお、ここで左側にある`change options`をクリックすると、Codespacesのスペック（ブランチ、Dev ContainerのConfig、リージョンやCPU）を変更できます。

## Jupyter環境の確認

起動するまで時間がかかりますので、しばらく待ちます。以下のようにターミナルが起動するまで待ちます。
※ターミナルに表示される文字列は環境によって異なります。

![Codespace Terminal](./images/codespace-ml2.png)

## ハンズオン

## 思うところ

実際に触ってみましたが、非常に簡単にJupyter環境を構築できました。
とはいえ、日頃からデータ分析や機械学習を行っている人にとっては、既存のクラウドサービスを使う方が良い場合もあるかもしれません。

というのも多くの企業ではデータがよく使うクラウド上にあって、そして、Vertex AIやSagemakerといったクラウドサービスを使っているはずです。

そうするとCodespacesでJupyterを使うということはどういうことかというと
基本的にはソースコードはGitHubにあり、ソースコードが利用するデータはクラウド上にあるということになるかなと思います。

データはクラウド、ソースはGitHubという状態が良いか悪いかというところはMLでいうところの実験管理の側面もあるので、なんとも難しいところです。また、MLパイプラインがどうなっているかどこにあるかによっても変わると思います。

長々と書きましたが、要は使い分けが重要かなというところですが、デバッグやちょっとした試験的な実験を行うにはCodespaces上のJupyter環境は非常に便利だと思います。

## まとめ

## 余談：Jupyter環境を構築する方法（いくつか紹介）

今回紹介する方法以外でもJupyter環境を構築する方法はたくさんあります。

- ローカルPCにAnaconda/Conda/miniConda/PythonをインストールしてJupyter環境を構築する
  - Dockerを使ってJupyter環境を構築する
- 主要なクラウドサービスを使ってJupyter環境を構築する
  - Google CloudのVertex AI Workbenchを使う
  - Amazon SageMakerを使う
  - Azure Machine Learningを使う
- SaaSを使う
  - Databricksを使う
- Google Colabを使う
