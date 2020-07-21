---
title: .NET Core に移植するためのツール
description: .NET Core への移植に使用できるいくつかのツールに関する詳細情報
author: cartermp
ms.date: 05/03/2020
ms.openlocfilehash: d0cf0abf206950beb34556ca3ba7243d8cad241e
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795587"
---
# <a name="tools-to-help-with-porting-to-net-core"></a>.NET Core への移植で役立つツール

この記事に一覧表示されているツールは、移植するときに役立つ場合があります。

- [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) - .NET Framework と .NET Core の間で、コードを
  - [コマンド ライン ツール](https://github.com/Microsoft/dotnet-apiport/releases)として
  - [Visual Studio 拡張機能](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)として、どの程度移植できるかを示すレポートを生成できるツールチェーン。
- [.NET API アナライザー](../../standard/analyzers/api-analyzer.md): さまざまなプラットフォームでの C# API の互換性リスクの可能性と、非推奨の API の呼び出しを検出する Roslyn アナライザー。
- [try-convert](https://www.nuget.org/packages/try-convert/) - デスクトップ アプリを .NET Core に移動するなど、プロジェクトかソリューション全体を .NET SDK に変換できる .NET Core グローバル ツール。 もっと複雑なビルドを確立し (カスタムのタスク、ターゲット、インポートなど)、.NET Core との間で互換性がない多くのプロジェクト タイプが拒否される場合は推奨されません。
