---
layout: default
title: microsoft Excel
parent: Activation
---

# microsoft Excel
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
   {:toc}

---

## microsoft Excel

データの集計、表示、可視化まで実現できる多機能な表計算ソフト。

## データ連携方法

ExcelからODBC接続でRedshiftにアクセスできる。
RedshiftのODBCドライバは以下で公開されている。

> https://github.com/aws/amazon-redshift-odbc-driver

PC端末やExcelアプリケーションに過剰な負荷がかからないように、Excel接続に適したビューをRedshift側で用意しておく。

## データ活用方法

ピボットテーブルでBIツールのようにRedshiftのデータを分析できる。

## 参考記事

> ExcelでRedshift
> 
> ExcelってODBC扱えるよね、ということを思い出したのでExcelからRedshiftに接続してみたメモ。
> あんまり難しいこと考えずにDWHをカジュアルに使おうぜ、という気持ち。
>
> https://imai-factory.hatenablog.com/entry/2013/11/04/105207 
