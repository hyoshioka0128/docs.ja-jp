---
title: .NET Framework および特別なリリース
description: .NET およびアウトオブバンドのリリースについて説明します。 クロスプラットフォームでの開発の強化や新機能の導入を目的として、新しい機能をアウトオブバンド (OOB) でリリースしています。
ms.date: 10/10/2018
ms.assetid: 721f10fa-3189-4124-a00d-56ddabd889b3
ms.openlocfilehash: 9653696f46279e0c23418f92030d64839cc20518
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618767"
---
# <a name="net-framework-and-out-of-band-releases"></a>.NET Framework および特別なリリース

.NET Framework は、UWP アプリや従来のデスクトップ アプリや Web アプリなどのさまざまなプラットフォームに対応し、コードの再利用を最大化するために進化しました。 通常の .NET Framework のリリースに加えて、クロスプラットフォームでの開発の強化や新機能の導入を目的として、新しい機能をアウトオブバンド (OOB) リリースによって提供しています。

## <a name="advantages-of-oob-releases"></a>OOB リリースの長所

新しいコンポーネントやコンポーネントに対する更新プログラムをアウトオブバンドで提供することにより、Microsoft では .NET Framework の更新プログラムをより頻繁に提供できます。 また、カスタマーからのフィードバックにすばやく収集して対応できます。

独自のアプリで OOB 機能を使用する場合、OOB アセンブリはアプリのパッケージで配置されるため、ユーザーはアプリを実行するために最新バージョンの .NET Framework をインストールする必要はありません。

## <a name="how-oob-packages-are-distributed"></a>OOB パッケージの配布方法

共通言語ランタイム (CLR) のコア コンポーネントの OOB リリースは、.NET 用パッケージ マネージャーである [NuGet](https://www.nuget.org/) を通じて配布されます。 NuGet を使用すると、Visual Studio 内からライブラリを簡単に参照して .NET Framework プロジェクトに追加できます。 NuGet パッケージ マネージャーは、Visual Studio 2012 以降の Visual Studio のすべてのエディションに含まれています。 Visual Studio の **[ツール]** メニューで **NuGet パッケージ マネージャー**を探します。 インストールされていない場合は、[NuGet のインストール](/nuget/install-nuget-client-tools)の手順に従います。 NuGet の詳細については、[NuGet のドキュメント](/nuget)を参照してください。

## <a name="use-a-nuget-oob-package"></a>NuGet OOB パッケージを使用する

NuGet パッケージ マネージャーがインストールされている場合、Visual Studio のソリューション エクスプローラーを使用して、NuGet パッケージへの参照を確認し、追加できます。

1. Visual Studio でプロジェクトのショートカット メニューを開き、 **[NuGet パッケージの管理]** を選択します。 (このオプションは、 **[プロジェクト]** メニューからも使用できます。)

2. 左ペインで、 **[オンライン]** を選択します。

3. プレリリースのパッケージを使用する場合は、中央のペインのドロップダウン リスト ボックスで **[安定版パッケージのみ]** の代わりに **[リリース前のパッケージを含める]** を選択します。

4. 右ペインで、 **[検索]** ボックスを使用して使用するパッケージを検索します。 Microsoft の一部のパッケージは、Microsoft .NET Framework のロゴで識別され、すべて発行者は Microsoft となっています。

![NuGet パッケージ マネージャー。](./media/the-net-framework-and-out-of-band-releases/nuget-package-manager-dialog.png)

OOB パッケージを使用するアプリケーションを配置する場合は、前述のとおり、OOB のアセンブリは、アプリのパッケージに付属しています。

## <a name="types-of-oob-releases"></a>OOB のリリースの種類

通常、OOB パッケージには、1 つ以上のプレリリース バージョンと 1 つの安定したバージョンがあります。 プレリリースに含まれるライセンスでは通常、再配布は許可されませんが、パッケージを試用して、フィードバックを提供することができます。 フィードバックはパッケージに対する更新プログラムに組み込まれます。 最終リリースは NuGet を使って安定したパッケージとして配布され、アプリと共に NuGet パッケージを再配布できるライセンスが含まれます。 安定したパッケージは Microsoft によってサポートされています。 Microsoft では、IntelliSense のサポートや、ブログの投稿、フォーラムでの回答などの別の種類のドキュメントを、すべてのパッケージについて提供します。 また、すべてのパッケージではありませんが、一部のパッケージについてはソース コードも利用できる場合があります。 新しいパッケージや更新パッケージに関するお知らせについては、「[.NET Framework ブログ](https://devblogs.microsoft.com/dotnet/)」を受信登録できます。

リリース前のパッケージと安定版パッケージの両方を検索するには、NuGet パッケージ マネージャーで **[リリース前のパッケージを含める]** を選択してください。

## <a name="see-also"></a>関連項目

- [はじめに](index.md)
