---
title: .NET Core 3.1 を使用した Windows 10 でのデスクトップ アプリ最新化
description: .NET Core 3.1 を使用して既存のデスクトップ アプリを最新化する方法
ms.date: 05/12/2020
ms.openlocfilehash: 5861f806a9158ef761c47bc23e51327d4e2d0480
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83422663"
---
# <a name="modernizing-desktop-apps-on-windows-10-with-net-core-31"></a>.NET Core 3.1 を使用した Windows 10 でのデスクトップ アプリ最新化

![最新デスクトップ アプリに関する電子ブックのカバーを示すスクリーンショット。](./media/modernizing-existing-desktop-apps-ebook-cover.png)

発行者

Microsoft 開発部門、.NET および Visual Studio 製品チーム

A division of Microsoft Corporation

One Microsoft Way

Redmond, Washington 98052-6399

Copyright © 2020 by Microsoft Corporation

All rights reserved. 本書のいかなる部分も、書面による発行者の許可なしに、いかなる形式または方法によっても、複製または伝送することを禁じます。

本書は "現状有姿" で提供され、著者の見解と意見を表しています。 URL および他の参照されているインターネットの Web サイトをはじめ、本書に記載されている見解、意見、および情報は、通知なく変更されることがあります。

ここに記載したいくつかの例は、説明のためだけに提供された架空のものです。 実在のものとの関連性または関係性は一切ありません。

<https://www.microsoft.com> の "商標" Web ページに記載されている Microsoft および商標は、Microsoft グループの商標です。

Mac および macOS は Apple Inc. の商標です。

その他のすべてのマークおよびロゴは、該当する各社が所有しています。

共同作成者:

> **Olia Gavrysh**、Microsoft、.NET チーム、プログラム マネージャー

> **Miguel Angel Castejón Dominguez**、Kabel、イノベーション アーキテクト

参加者とレビュー担当者:

> **Maira Wenzel**、Microsoft、.NET チーム、シニア プログラム マネージャー

> **Andy De Gorge**、Microsoft、.NET Docs チーム、シニア コンテンツ開発者

> **Miguel Ramos**、Microsoft、Windows 開発者プラットフォーム チーム、シニア プログラム マネージャー

> **Adam Braden**、Microsoft、Windows 開発者プラットフォーム チーム、プリンシパル プログラム マネージャー

> **Ricardo Minguez Pablos**、Microsoft、Azure IoT チーム、シニア プログラム マネージャー

> **Nish Anil**、Microsoft、.NET チーム、シニア プログラム マネージャー

> **Beth Massi**、Microsoft、シニア製品マーケティング マネージャー

> **Scott Hunter**、Microsoft、.NET チーム、パートナー ディレクター プログラム マネージャー

> **Marta Fuentes Lara**、Kabel

> **Raúl Fernández de Córdoba**、Kabel

> **Antonio Manuel Fernández Cantos**、Kabel

## <a name="introduction"></a>はじめに

本書では、最新化のパスを使用して既存のデスクトップ アプリケーションを移動させて、最新のランタイム、言語、プラットフォームの機能を組み込むための戦略について説明しています。 アプリケーションがそれぞれ異なり、同様にユーザーの要件や設定もそれぞれ異なるため、独自のレシピが存在しないことはわかるでしょう。 良い点としては、アプリケーションに新しい機能を追加する場合に、一般的なアプローチを適用できることです。 一部のアプローチでは、コードを大幅に変更する必要もありません。 本書では、それらすべての機能のバックグラウンドでの動作を明らかにして、実装のしくみについて説明します。 また、プロジェクトを進化させるためのインスピレーションを得ることができるように、既存のデスクトップ アプリケーションを最新化するための一般的なシナリオをいくつか紹介します。

Microsoft では、既存のアプリケーションを最新化するためのアプローチとして、カスタマイズされた独自のパスを柔軟に作成できるようにしています。 本書で説明されている最新化戦略はすべて、大部分が独立しています。 ご利用のアプリケーションに関連する戦略を選択し、重要ではない他の戦略はスキップすることができます。 つまり、戦略を組み合わせて、最良の方法でアプリケーションのニーズに対応することができます。

## <a name="who-should-use-the-book"></a>対象読者

本書は、既存の Windows フォームと WPF デスクトップ アプリケーションを最新化して .NET Core と Windows 10 のメリットを活用したい開発者やソリューション アーキテクト向けに執筆されました。

また、既存のデスクトップ アプリケーションを最新化することで得られるメリットの概要を知りたいエンタープライズ アーキテクトや開発担当者などの技術的な意思決定者の場合にも、本書は役立つでしょう。

## <a name="how-to-use-the-book"></a>本書の使用方法

本書では、既存のアプリケーションを最新化する必要がある "理由"、および NET Core 3.1 と MSIX を使用してデスクトップ アプリを最新化することで得られる具体的なメリットについて説明します。 本書の内容は、概要は知りたいが、実装や技術的なステップバイステップの詳細は必要のないアーキテクトおよび技術的意思決定者向けに考案されています。

各章には、サンプルの実装コード スニペットとスクリーンショットを記載しています。また、第 5 章では、サンプル アプリケーションの完全な移行プロセスを説明します。

## <a name="what-this-book-doesnt-cover"></a>本書で取り上げないもの

本書では、リフトアンドシフト シナリオに重点を置いたシナリオの特定のサブセットを紹介し、コードを書き直すことなく最新化のメリットを得るための方法の概要を説明します。

本書では、.NET Core を使用して最新のアプリケーションをゼロから開発することについて、および Windows フォームと WPF の概要については説明しません。 ここでは、デスクトップ開発のための最新テクノロジを使用した既存のデスクトップ アプリケーションの更新方法について重点的に説明します。

## <a name="samples-used-in-this-book"></a>本書で使用するサンプル

最新化の実行に必要な手順を強調するために、`eShopModernizing` と呼ばれるサンプル アプリケーションを使用します。 このアプリケーションには、Windows フォームと WPF という 2 種類のフレーバーがあります。これらの両方で .NET Core に対して最新化を実行する方法について、ステップバイステップのプロセスを説明します。

また、本書の GitHub リポジトリには、プロセスの結果が表示されます。ステップバイステップのチュートリアルに従う場合は、こちらを参照してください。

## <a name="send-your-feedback"></a>フィードバックの送信

本書と関連サンプルは継続的に更新されるので、お客様のフィードバックを歓迎しています。 本書を改善する方法についてコメントがある場合、[GitHub の問題](https://github.com/dotnet/docs/issues)に関して作成されたあらゆるページの下部にあるフィードバック セクションをご利用ください。

>[!div class="step-by-step"]
>[次へ](why-modern-applications.md)
