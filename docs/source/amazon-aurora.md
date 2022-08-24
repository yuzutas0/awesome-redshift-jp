---
layout: default
title: Amazon Aurora
parent: Source
---

# Amazon Aurora
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## データ取得方法

### Federated Queryで取得

RedshiftでSQLを実行すると、Amazon Auroraにアクセスしてデータを取得できる。

#### メリット

- ETL処理をサーバーレスかつフルマネージドに実現できる
- クエリ実行時に参照するので常に最新の結果を取得できる

#### デメリット

- アクセス先に負荷がかかる

#### データの流れ

Amazon Aurora → （DNS or RDS proxy →） Amazon Redshift

> クラスターエンドポイントを直で指定するのではなくCNAMEレコード等をRoute53とかで作って、そのアドレスを指定しておくことをオススメします。
> (中略)
> クラスターが作り直しになるので、Federated Queryの外部テーブルの定義でクラスターエンドポイントを直接指定してたら、その外部テーブルも作り直しになります。そうなると、依存するView等も作り直しになります。
> 
> https://datatech-jp.slack.com/archives/C03MHCZS2GG/p1656734780821049

#### 実現するテクノロジー

以下がハンズオン記事
[#DevelopersIO [新機能] Amazon Redshift Federated QueryがGAになったので試してみました](https://dev.classmethod.jp/articles/amazon-redshift-20200417-federated-query-ga/)
