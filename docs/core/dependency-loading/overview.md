---
title: 依存関係の読み込み - .NET Core
description: .NET Core でのマネージドおよびアンマネージドの依存関係の読み込みの概要
ms.date: 08/09/2019
author: sdmaclea
ms.author: stmaclea
ms.topic: overview
ms.openlocfilehash: 34deb802183f20cc92449c21eb7e149cc002850f
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84284223"
---
# <a name="dependency-loading-in-net-core"></a>.NET Core での依存関係の読み込み

すべての .NET Core アプリケーションには依存関係があります。 単純な `hello world` アプリでも、.NET Core クラス ライブラリの一部に依存関係があります。

.NET Core の既定のアセンブリ読み込みロジックについて理解すると、デプロイに関する一般的な問題を理解し、デバッグするのに役立ちます。

アプリケーションによっては、依存関係が実行時に動的に決定されます。 このような状況では、マネージド アセンブリおよびアンマネージドの依存関係がどのように読み込まれるかを理解することが重要です。

## <a name="understanding-assemblyloadcontext"></a>AssemblyLoadContext について

<xref:System.Runtime.Loader.AssemblyLoadContext> API は、.NET Core 読み込みデザインの中核となるものです。 [AssemblyLoadContext について](understanding-assemblyloadcontext.md)の記事では、設計の概念についての概要を示します。

## <a name="loading-details"></a>読み込みの詳細

読み込みアルゴリズムの詳細については、次のいくつかの記事で簡単に説明されています。

- [マネージド アセンブリの読み込みアルゴリズム](loading-managed.md)
- [サテライト アセンブリの読み込みアルゴリズム](loading-resources.md)
- [アンマネージド (ネイティブ) ライブラリの読み込みアルゴリズム](loading-unmanaged.md)
- [既定のプローブ](default-probing.md)

## <a name="create-a-net-core-application-with-plugins"></a>プラグインがある .NET Core アプリケーションを作成する

チュートリアル「[プラグインがある .NET Core アプリケーションを作成する](../tutorials/creating-app-with-plugin-support.md)」では、カスタムの AssemblyLoadContext の作成方法について説明します。 ここでは <xref:System.Runtime.Loader.AssemblyDependencyResolver> を使用して、プラグインの依存関係を解決します。 このチュートリアルでは、ホスト アプリケーションからプラグインの依存関係を正しく分離します。

## <a name="how-to-use-and-debug-assembly-unloadability-in-net-core"></a>.NET Core でアセンブリのアンローダビリティを使用およびデバッグする方法

「[.NET Core でアセンブリのアンローダビリティを使用およびデバッグする方法](../../standard/assembly/unloadability.md)」の記事は、ステップ バイ ステップのチュートリアルです。 ここでは、.NET Core アプリケーションを読み込んで実行し、アンロードする方法を示します。 この記事ではデバッグのヒントも示します。
