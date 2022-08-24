---
layout: default
title: Reverse ETL
parent: Activation
---

# Reverse ELT
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## Reverse ELT とは何か

Redshiftで集計した結果をもとに、メール配信といったデータ活用に繋げていくこと。
ETLソリューションの多くがデータソースからRedshiftへの連携を得意とするため、
Redshiftから外へのデータ連携をReverseETLと呼ぶことがある。

### Lambda UDFによる実現

RedshiftのSQL実行時にUDFでLambdaを実行できる。

> 仮にDBTによるSNSを使ってレポート送ったりするサンプル的なのを出すと、こんな感じになるとは思います。
> 
> https://datatech-jp.slack.com/archives/C03MHCZS2GG/p1657676866715489

```sql
{{
    config(
        materialized='incremental',
    )
}}

SELECT
    getdate() as send_at,
    publish_message_to_sns_udf('sample-topic', data) as publish_result
FROM
    {{ ref('report_data') }}
```

- メリット
    - 全てSQLで完結できる
- デメリット
    - 本来はSQLで出来ないことを実現するので、プログラムを別に作るケースに比べて、設計、テスト、CI/CD、監視といった一連の活動が順調に進むとは限らない
    
### S3 Notification の利用

1. Redshiftで集計結果や抽出リストをS3にUNLOADする。
1. S3にObjectがPutされたらS3 Notificationを使って通知を送る。
1. 他のAWSサービスと連携して別の場所に転送する。例えばLambdaでメール配信ツールのAPIにリクエストを送る。

> https://datatech-jp.slack.com/archives/C03MHCZS2GG/p1657677126126539

- メリット
  - 各サービスが適切に役割分担されており、安定したシステム構成となる。
- デメリット
  - SQLで完結しないので各サービスごとに設計、テスト、CI/CD、監視といった仕組みを作る必要がある。
