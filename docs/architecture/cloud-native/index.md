---
title: Azure 向けクラウド ネイティブ .NET アプリケーションの設計
description: Azure のコンテナー、マイクロサービス、サーバーレス機能を活用するクラウドネイティブなアプリケーションを構築するためのガイド。
author: ardalis
ms.date: 05/13/2020
ms.openlocfilehash: 172097b4915deb2d6f0b06441d7c4ca389bbca25
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051507"
---
# <a name="architecting-cloud-native-net-applications-for-azure"></a>Azure 向けクラウド ネイティブ .NET アプリケーションの設計

![カバーの画像](./media/cover.png)

**EDITION v.1.0**

発行者

Microsoft 開発部門、.NET および Visual Studio 製品チーム

A division of Microsoft Corporation

One Microsoft Way

Redmond, Washington 98052-6399

Copyright &copy; 2020 by Microsoft Corporation

All rights reserved. 本書のいかなる部分も、書面による発行者の許可なしに、いかなる形式または方法によっても、複製または伝送することを禁じます。

本書は "現状有姿" で提供され、著者の見解と意見を表しています。 URL および他の参照されているインターネットの Web サイトをはじめ、本書に記載されている見解、意見、および情報は、通知なく変更されることがあります。

ここに記載したいくつかの例は、説明のためだけに提供された架空のものです。 実在のものとの関連性または関係性は一切ありません。

<https://www.microsoft.com> の "商標" Web ページに記載されている Microsoft および商標は、Microsoft グループの商標です。

Mac および macOS は Apple Inc. の商標です。

Docker のクジラのロゴは Docker, Inc. の登録商標です。許可を得て使用しています。

その他のすべてのマークおよびロゴは、該当する各社が所有しています。

作成者:

> **Rob Vettor**、Microsoft、プリンシパル クラウド システム アーキテクト/IP アーキテクト - [thinkingincloudnative.com](https://thinkingincloudnative.com/about/)
>
> **Steve "ardalis" Smith**、ソフトウェア アーキテクトおよびトレーナー - [Ardalis.com](https://ardalis.com)

参加者とレビュー担当者:

> **Cesar De la Torre**、Microsoft、.NET チーム、プリンシパル プログラム マネージャー
>
> **Nish Anil**、Microsoft、.NET チーム、シニア プログラム マネージャー
>
> **Jeremy Likness**、Microsoft、.NET チーム、シニア プログラム マネージャー
>
> **Cecil Phillip**、Microsoft、上級クラウド アドボケイト

編集者:

> **Maira Wenzel**、Microsoft、.NET チーム、シニア プログラム マネージャー

## <a name="version"></a>バージョン

このガイドは、 **.NET Core 3.1** バージョンと、.NET Core 3.1 のリリースと同時期に更新された関連するその他の多数の同じ “相次ぐ” テクノロジ (つまり、Azure やサードパーティ製のテクノロジ) を説明するように記述されています。

## <a name="who-should-use-this-guide"></a>対象読者

本ガイドの対象読者は主に、クラウド向けに設計されたアプリケーションを構築する方法に関心がある開発者、開発リーダー、アーキテクトです。

2 番目の対象読者は、クラウドネイティブな手法でアプリケーションを構築するかどうかを決定する予定の技術部門の意思決定者です。

## <a name="how-you-can-use-this-guide"></a>このガイドを使用する方法

本書ではまず、クラウド ネイティブを定義し、クラウドネイティブなプリンシパルとテクノロジで構築された参照アプリケーションを紹介します。 その最初の 2 章以降、本書の残りの部分は、ほとんどのクラウドネイティブ アプリケーションに共通するトピックに特化した章に分割されています。 任意の章までジャンプし、次に関するクラウドネイティブ手法について知ることができます。

- データとデータ アクセス
- 通信パターン
- スケーリングとスケーラビリティ
- アプリケーションの回復性
- 監視と正常性
- ID とセキュリティ
- DevOps

このガイドは [PDF](https://dotnet.microsoft.com/download/e-book/cloud-native-azure/pdf) 形式とオンラインの両方で利用できます。 本書やそのオンライン版のリンクをチームに転送し、トピックの共通理解に役立ててください。 トピックのほとんどは、基礎的な原則、基礎的なパターン、トピックに関連する意思決定に関係する折り合いが同じように理解されることで効果を発揮します。 本書の目標は、アプリケーションのアーキテクチャ、開発、ホスティングについて、十分に情報が与えられた上で意思決定するために必要な情報をチームとそのリーダーに与えることです。

## <a name="send-your-feedback"></a>フィードバックの送信

本書と関連サンプルは継続的に更新されるので、お客様のフィードバックを歓迎しています。 本書を改善する方法についてコメントがある場合、[GitHub の問題](https://github.com/dotnet/docs/issues)に関して作成されたあらゆるページの下部にあるフィードバック セクションをご利用ください。

>[!div class="step-by-step"]
>[次へ](introduction.md)
