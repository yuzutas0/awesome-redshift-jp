---
layout: default
title: BigQuery
parent: Source
---

# BigQuery
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## データ取得方法

### WebAPI 経由で取得

[BigQuery REST Resource: jobs](https://cloud.google.com/bigquery/docs/reference/rest/v2/jobs#configuration.extract)

#### メリット

- ツールの選択肢が幅広いので自社に適したアーキテクチャを選定できる。

#### デメリット

- 外部テーブルのデータ抽出に対応していない。
- 直接APIにリクエストを送る場合、大規模データの受け渡しはSQL実行ではなくジョブの発行・受け取りが必要となる。

#### データの流れ

- BigQuery → WebAPI → 任意のIntegrationソリューション (→ Amazon S3) → Amazon Redshift。
- BigQueryはデータ基盤ではなく、外部データソースという位置付けになる。

#### 実現するテクノロジー

- [Embulkのplugiin](https://github.com/jo8937/embulk-input-bigquery_extract_files) にて上記エンドポイントにリクエストを送る。
- [AirflowのOperator](https://airflow.apache.org/docs/apache-airflow-providers-google/stable/operators/cloud/bigquery.html) にて上記エンドポイントにリクエストを送る。
- AWS Lambda等で定期バッチを作成し、上記エンドポイントにリクエストを送る。
- Amazon RedshiftからLambda UDF経由でAWS Lambdaを実行して、上記エンドポイントにリクエストを送る。
- trocco等のETL SaaSにて[転送元：BigQuery](https://documents.trocco.io/docs/data-source-bigquery) 、[転送先：Redshift](https://documents.trocco.io/docs/data-destination-redshift) を設定する。
- [CData Syncによるレプリケーション](https://www.cdata.com/jp/kb/tech/bigquery-sync-redshift.rst) を実施する。

関連：[Integration](../integration/integration.md)

### エクスポート

[Google Cloud Storage へのエクスポート機能](https://cloud.google.com/bigquery/docs/exporting-data) を用いる。

#### メリット

- 安定したパフォーマンスで大規模データを受け渡せる。
- エクスポートはWebAPI、各プログラミング言語のライブラリ、SQLで指示できる。

#### デメリット

- 1GBを超えるデータは複数ファイルに分割される。
- ネストや繰り返しのあるデータはAvro、JSON、Parquet形式のみ対応している。
- JSON形式ではINT64（整数）型は文字列としてエンコードされ、一部の記号はUnicode表記に変換される。

#### データの流れ

- BigQuery → Cloud Storage → 任意のIntegrationソリューション （→ Amazon S3） → Amazon Redshift
- BigQuery や Cloud Storage はデータ基盤ではなく、外部データソースという位置付けになる。

#### 実現するテクノロジー

- AWS Lambda等で定期バッチを作成し、エクスポート指示を出すように上記エンドポイントにリクエストを送る。
- Amazon RedshiftからLambda UDF経由でAWS Lambdaを実行して、上記エンドポイントにリクエストを送る。

- Cloud Storage からのデータ連携方法は[別ページ](./google-cloud-storage.md)を参照。
