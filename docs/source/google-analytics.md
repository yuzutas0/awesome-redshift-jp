---
layout: default
title: Google Analytics
parent: Source
---

# Google Analytics
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

{:toc}

---

## データ取得方法

1. WebAPI
    - エンドポイント
        - [Reporting API v4](https://developers.google.com/analytics/devguides/reporting/core/v4) ：Universal Analyticsのレポートが対象。
        - [Google Analytics Data API v1](https://developers.google.com/analytics/devguides/reporting/data/v1) ：Google Analytics 4のレポートが対象。
    - メリット
        - GoogleAnalyticsのコンソール画面と同じデータなので、数字のズレを気にしなくて済む。
        - ツールの選択肢が幅広いので自社に適したアーキテクチャを選定できる。
    - デメリット
        - ローデータをそのまま使えるわけではないので、他データソースとの統合や集計に限界がある。 
    - データの流れ
        - WebAPI → 任意のIntegrationソリューション (→ Amazon S3) → Amazon Redshift
    - 実現するテクノロジー（関連：[Integration](../integration/integration.md)）
        - AWS Lambda等で定期バッチを作成し、上記エンドポイントにリクエストを送る。
        - Amazon RedshiftからLambda UDF経由でAWS Lambdaを実行して、上記エンドポイントにリクエストを送る。
        - [Amazon AppFlow](https://aws.amazon.com/jp/appflow/) を利用する。
        - [CData AWS Glue Connector for Google Analytics](https://aws.amazon.com/marketplace/pp/prodview-s65fmshg6qcvw) を利用する。
1. エクスポート
    - 出力先
        - [BigQuery](https://support.google.com/analytics/topic/9359001) のみ出力可能。
    - メリット
        - ローデータをそのまま使えるので、他データソースとの統合や集計が可能となる。
    - デメリット
        - GoogleAnalyticsのコンソール画面を使い慣れている場合、数字を一致させるのは難しいため、混乱を招く恐れがある。
        - ツールの選択肢が1つだけなのでマルチクラウドを管理しなければならない。
        - 無料版かつ日次エクスポート設定だと1日の上限は100万イベントまでに制限される。
        - 日次エクスポートの完了時間が約束されていないため、テスト＆リトライの自動化を実装する必要がある。
    - データの流れ
        - Google Analytics → エクスポート設定 → BigQuery (→ Cloud Storage) → 任意のIntegrationソリューション （→ Amazon S3） → Amazon Redshift
        - BigQuery や Cloud Storage はデータ基盤ではなく、外部データソースという位置付けになる。
    - 実現するテクノロジー
        - TODO：記載
