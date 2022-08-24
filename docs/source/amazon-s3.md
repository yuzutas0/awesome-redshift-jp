---
layout: default
title: Amazon S3
parent: Source
---

# Amazon S3
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## データ取得方法

### Copyコマンド

RedshiftのコマンドでCopyを指示する。

#### メリット

- Redshiftにデータをロードするので挙動が安定しやすい

#### デメリット

- バッチスクリプトの環境構築が必要
- バッチ取得時点のデータがロードされるので、最新データをリアルタイムで確認できない

#### データの流れ

S3 → COPYコマンド → Redshift

#### 実現するテクノロジー

- AWS Lambda等で定期バッチを作成し、コマンドを実行する。
- Amazon RedshiftからLambda UDF経由でAWS Lambdaを実行する。

以下がハンズオン記事。

> [RedshiftでCOPYコマンドを試してみた - Qiita](https://qiita.com/tomokyu/items/89a470b99730f66ac4cf)

直接コマンドを実行する方法と、Redshift Data APIを使う方法がある。
以下が、Redshift Data APIによるCOPYコマンドのハンズオン記事

> [Data API for Redshiftでデータのロード/アンロードを試してみた](https://dev.classmethod.jp/articles/data-api-for-redshift-load-unload-try/)


### Redshift Spectrum

S3に対してクエリを実行できる。

#### メリット

- サーバーレスかつフルマネージドにETL処理を実現できる
- クエリ時点のデータがロードされるので、最新データをリアルタイムで確認できる

#### デメリット

- Redshiftにデータをロードしないので、外部テーブルの制約に引っかかることがある

#### データの流れ

S3 → Redshift Spectrum → Redshift

#### 実現するテクノロジー

以下がハンズオン記事。

[S3データを直接クエリ出来る新機能『Amazon Redshift Spectrum』を実際に試してみました](https://dev.classmethod.jp/articles/amazon-redshift-getting-started-with-spectrum/)

直接クエリ実行する方法と、Redshift Data APIを使う方法がある。
以下が、Redshift Data APIによるRedshift Spectrum実行のハンズオン記事。

> [Amazon Redshift Data APIを使ったETL](https://qiita.com/KimiyukiMuramatsu/items/d301b587f0a8cb7f0553)
