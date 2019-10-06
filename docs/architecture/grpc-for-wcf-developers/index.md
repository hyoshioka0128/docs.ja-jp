---
title: WCF 開発者向け ASP.NET Core gRPC - WCF 開発者向け gRPC
description: 記述予定
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: dc39fc96e7154fb50acd0b65a58586b3fa12ab50
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696917"
---
# <a name="aspnet-core-grpc-for-wcf-developers"></a>WCF 開発者向け ASP.NET Core gRPC

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

![カバーの画像](./media/cover.png)

発行者

Microsoft 開発部門、.NET および Visual Studio 製品チーム

A division of Microsoft Corporation

One Microsoft Way

Redmond, Washington 98052-6399

Copyright © 2019 by Microsoft Corporation

All rights reserved. 本書のいかなる部分も、書面による発行者の許可なしに、いかなる形式または方法によっても、複製または伝送することを禁じます。

本書は "現状有姿" で提供され、著者の見解と意見を表しています。 URL および他の参照されているインターネットの Web サイトをはじめ、本書に記載されている見解、意見、および情報は、通知なく変更されることがあります。

ここに記載したいくつかの例は、説明のためだけに提供された架空のものです。 実在のものとの関連性または関係性は一切ありません。

[https://www.microsoft.com](https://www.microsoft.com ) の "商標" Web ページに記載されている Microsoft および商標は、Microsoft グループの商標です。

Docker のクジラのロゴは Docker, Inc. の登録商標です。許可を得て使用しています。

その他のすべてのマークおよびロゴは、該当する各社が所有しています。

作成者:

> **Mark Rendle** - 技術部門最高責任者 - [Visual ReCode](https://visualrecode.com)
>
> **Miranda Steiner** - 技術文書作成者

編集者:

> **Maira Wenzel** - シニア コンテンツ開発者 - Microsoft

## <a name="introduction"></a>はじめに

TODO

## <a name="purpose"></a>目的

TODO

## <a name="who-should-use-this-guide"></a>対象読者

**これを更新する**

本ガイドの対象読者は、gRPC サービスを利用して .NET 4 以前の WCF ソリューションを ASP.NET Core 3.0 に移行することに関心がある WCF 開発者、開発リーダー、アーキテクトです。

## <a name="how-you-can-use-this-guide"></a>このガイドを使用する方法

**これを更新する**

本書では ASP.NET Core 3.0 で gRPC サービスを構築する方法を簡単に説明しています。特に、同類のプラットフォームとして WCF を参照しています。 gRPC の原則について説明しており、各概念をそれに相当する WCF の機能に関連付けています。また、既存の WCF アプリケーションを gRPC に移行する方法を紹介しています。 WCF の経験があり、新しいサービスを構築する目的で gRPC の知識を求めている開発者にとっても役立ちます。 サンプル アプリケーションは独自のプロジェクトのためのテンプレートまたは参照として利用できます。本書やそのサンプルのコードは自由にコピーしたり、再利用したりしてかまいません。

これらの考慮事項と営業案件の共通理解を確保するために、チームにこのガイドを自由に転送してください。 用語の共通セットと基本原則を理解して全員が作業すると、アーキテクチャのパターンと実践方法を一貫して適用できるようになります。

## <a name="references"></a>関連項目

- **gRPC Web サイト**  
  <https://grpc.io>
- **サーバー アプリ用 .NET Core と .NET Framework の選択**  
  <https://docs.microsoft.com/dotnet/standard/choosing-core-framework-server>

>[!div class="step-by-step"]
>[次へ](introduction.md)
