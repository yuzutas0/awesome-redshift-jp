---
layout: default
title: Data Vault 2.0
parent: Modeling
---

# Data Vault 2.0
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## Data Vault 2.0 とは何か

TODO：分かりやすいページがそのうち公開されるはずなのでリンクを張ります

## dbtによる実現

現時点ではdbtvaultがRedshiftに対応していないため、自前でマクロやクエリを書く必要がある。
dbtのロードマップには記載済み。

> Releases Roadmap¶
> 
> v0.8.x¶
> - We will be incrementally back-filling support for Google BigQuery and MSSQL Server v0.8.x versions
> 
> Future releases¶
> 
> In future releases, we hope to include the following:
> 
> Platform support¶
> - Databricks
> - Postgres
> - Amazon Redshift
>
> https://dbtvault.readthedocs.io/en/latest/roadmap/

さらに、dbtvaultではカラム名を強制的にUpperにしているが、RedshiftのSUPER型の仕様にハマりポイントがあるので注意。

> JSON フィールドで、大文字、または大文字と小文字が混在している場合は、enable_case_sensitive_identifier を TRUE に設定し、大文字、または大文字と小文字が混在しているフィールドを二重引用符で囲む必要があります。
> 
> https://docs.aws.amazon.com/ja_jp/redshift/latest/dg/super-configurations.html

以下の議論より抜粋。

> https://datatech-jp.slack.com/archives/C03MHCZS2GG/p1657680767159609
