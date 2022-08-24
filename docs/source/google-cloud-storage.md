---
layout: default
title: Google Cloud Storage
parent: Source
---

# Google Cloud Storage
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## データ取得方法

### WebAPI 経由で取得

[API reference](https://cloud.google.com/storage/docs/json_api/v1)

#### メリット

- ツールの選択肢が幅広いので自社に適したアーキテクチャを選定できる。

#### デメリット

- 特になし

#### データの流れ

- Cloud Storage → WebAPI → 任意のIntegrationソリューション (→ Amazon S3) → Amazon Redshift。
- Cloud Storage はデータレイクではなく、外部データソースという位置付けになる。

#### 実現するテクノロジー

- [Embulkのplugiin](https://github.com/embulk/embulk-input-gcs) にて上記エンドポイントにリクエストを送る。
- [AirflowのOperator](https://airflow.apache.org/docs/apache-airflow-providers-google/stable/_api/airflow/providers/google/cloud/operators/gcs/index.html) にて上記エンドポイントにリクエストを送る。
- AWS Lambda等で定期バッチを作成し、上記エンドポイントにリクエストを送る。
- Amazon RedshiftからLambda UDF経由でAWS Lambdaを実行して、上記エンドポイントにリクエストを送る。
- trocco等のETL SaaSにて[転送元：Google Cloud Storage](https://documents.trocco.io/docs/data-destination-google-cloud-storage) 、[転送先：Redshift](https://documents.trocco.io/docs/data-destination-redshift) を設定する。

関連：[Integration](../integration/integration.md)

### AWS DataSync

[AWS DataSync](https://aws.amazon.com/jp/datasync/)

#### メリット

- 安定したパフォーマンスで大規模データを受け渡せる。

#### デメリット

- 他にもデータソースがある場合、GCS→S3だけ独立した経路を作ることになる。CI/CD、SLO監視等もAWS DataSync用に構築することになる。

#### データの流れ

- Cloud Storage → S3 → Redshift
- Cloud Storage はデータレイクではなく、外部データソースという位置付けになる。

#### 実現するテクノロジー

手順は [AWS DataSync を使用して Google Cloud Storage から Amazon S3 にデータを移行する方法 - Amazon Web Services ブログ](AWS DataSync を使用して Google Cloud Storage から Amazon S3 にデータを移行する方法) に記載。
