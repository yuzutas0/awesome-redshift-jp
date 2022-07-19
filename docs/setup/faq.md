---
layout: default
title: FAQ
parent: Setup
---

# FAQ
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Redshift Serverless の料金表が「プレビュー」のままに見える（2022年7月19日時点）

日本語だと「プレビュー」の記載がありますが、英語だとPreviewの記載は外れています。
料金表の内容も同じなので、日本語の翻訳が間に合っていないようです。


日本語の料金表:

![日本語の料金表]({{ site.baseurl }}{% link assets/images/cost_preview_1.png %})

英語の料金表:

![英語の料金表]({{ site.baseurl }}{% link assets/images/cost_preview_2.png %})


## Redshift Serverless の名前空間やワークグループの削除ができない（2022年7月19日時点）

日本語表示だとコンソールでエラーになってしまう。

> Amazon Redshift Serverlessで名前空間もワークグループもコンソールのエラーで削除できない
> 
> [https://twitter.com/Korosuke512tr/status/1547783609666265089](https://twitter.com/Korosuke512tr/status/1547783609666265089)

解決策1) 管理コンソールを日本語から英語に変える。

> 管理コンソールの言語を英語に変更して試していただくと、削除できるようになるかもしれません。
> 
> [https://twitter.com/simosako/status/1547790642926870528](https://twitter.com/simosako/status/1547790642926870528)

解決策2) CLI経由で削除する。

> CLI で消せた
> 
> [https://twitter.com/hayaok3/status/1547086353489620992](https://twitter.com/hayaok3/status/1547086353489620992)

## Redshift Serverless の credentials はiamが別

`redshift:GetClusterCredentials` ではなく `redshift-serverless:GetCredentials` が対象となる。

> 一時的な認証情報を使用してサーバーレスワークグループへの認証を行う場合は、ポリシーで redshift-serverless:GetCredentials アクションの使用が許可されていることを確認します。
> [https://docs.aws.amazon.com/ja_jp/redshift/latest/mgmt/data-api.html](https://docs.aws.amazon.com/ja_jp/redshift/latest/mgmt/data-api.html)


非公式ラッパーとして [https://github.com/mashiike/redshift-credentials](https://github.com/mashiike/redshift-credentials) が作られた。

> ServerlessなのかProvisionedなのか意識して、更にAPIの投げわけしないといけないの？
> そう思った人（私）向けにServerlessでもProvisionedでも、どっちのエンドポイントをパラメータに渡してもいい感じに一時認証してDB USERとDB Passwordを返してくれる君を書いてみました。
> 
> [https://datatech-jp.slack.com/archives/C03MHCZS2GG/p1657977637298559](https://datatech-jp.slack.com/archives/C03MHCZS2GG/p1657977637298559)


## Redshift Serverless は時間課金なのでバッチ向き

ストリーミング連携など、高頻度にデータ連携するときは以下の構成だとコスト効率が良い。

- 小さめの常駐インスタンスにデータを流す。
- Redshift ServerlessからData Sharingで常駐インスタンスを参照する

[https://twitter.com/mashiike/status/1547032218140192768](https://twitter.com/mashiike/status/1547032218140192768)

Redshift Serverlessで完結したい場合は、ログをストリーミングでS3に反映しつつ、
Redshiftへのロードは1時間に1回のマイクロバッチで実現するような設計が考えられる。

[https://twitter.com/yuzutas0/status/1547011222998220800](https://twitter.com/yuzutas0/status/1547011222998220800)
