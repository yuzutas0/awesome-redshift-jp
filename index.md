---
layout: default
title: Home
nav_order: 1
description: "Awesome Redshift JP"
permalink: /
---

# Awesome Redshift JP
{: .fs-9 }

Amazon Redshift によるデータ活用を実現するためのノウハウや参考資料をまとめています。
{: .fs-6 .fw-300 }

[GitHubで開く](https://github.com/yuzutas0/awesome-redshift-jp){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 }

---

## ドキュメント構成

- [セットアップ＆ハンズオン]({{ site.baseurl }}{% link docs/setup/setup.md %})
- [ユースケース]({{ site.baseurl }}{% link docs/usecase/usecase.md %})：データ活用によるビジネス価値の創出（ROAS計測、ダイナミックプライシング、1to1マーケティング、Sales Ops、CS Ops、HR Opsなど）
- [データアクティベーション]({{ site.baseurl }}{% link docs/activation/activation.md %})：Redshiftのデータを用いてユースケースを実現する方法（ReverseETL、Embed BIなど）
- [データモデリング]({{ site.baseurl }}{% link docs/modeling/modeling.md %})：DWHのデータを使いやすく整備する方法（Data Vault 2.0、ディメンショナルモデリングなど）
- [データ統合]({{ site.baseurl }}{% link docs/integration/integration.md %})：各データソースのデータをRedshiftに収集する方法（ETLツールなど）
- [データソース]({{ site.baseurl }}{% link docs/source/source.md %})：データの生成箇所・取得元（RDBMSやアクセス解析ツールなど）
- [ワークフロー]({{ site.baseurl }}{% link docs/workflow/workflow.md %})：データ統合からデータアクティベーションまでの全体の流れを管理する方法（マネージドELTツール、データリネージ管理など）
- [データガバナンス]({{ site.baseurl }}{% link docs/governance/governance.md %})：データを安心・安全に使えるように内部統制する方法（個人情報保護法、セキュリティ、メタデータ整備など）
- [機械学習]({{ site.baseurl }}{% link docs/machine-learning/machine-learning.md %})：Redshiftのデータを用いて機械学習を実現する方法（MLOps/SysML、AutoMLツールなど）

## 用語について

書籍『実践的データ基盤への処方箋』ならびに『データマネジメントが30分でわかる本』に準拠します。

## コミュニティについて

- 主な活動場所： Slackコミュニティ「[datatech-jp](https://datatech-jp.github.io/)」の「[#redshift](https://datatech-jp.slack.com/archives/C03MHCZS2GG)」チャンネル
- コントリビューター： [@yuzutas0](https://twitter.com/yuzutas0), [@mashiike](https://twitter.com/mashiike), [@yummydum](https://twitter.com/yummydum)
- インタビューのお願い： Redshiftを利用中または検討中の方に、30分のオンライン1on1で「こういうノウハウを開拓した」「この記事が参考になった」「こういうことに困っている」「こういう情報を掲載してほしい」といったお話を伺っています。「話しても良いよ」という方がいたらSlackで相談させてください。

## Contributionについて

- ぜひ気軽にIssue、Discussion、P.R.に投稿していただけると嬉しいです。
- 完成度が上がったら個人リポジトリからOrganization（例：[datatech-jp](https://github.com/datatech-jp/) ）への移行を検討します。
