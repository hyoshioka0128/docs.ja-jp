---
title: サテライト アセンブリの読み込みアルゴリズム - .NET Core
description: .NET Core でのサテライト アセンブリ読み込みアルゴリズムの詳細の説明
ms.date: 08/09/2019
author: sdmaclea
ms.author: stmaclea
ms.openlocfilehash: 17f29a9aca79019daa91736e586bf1b6b753a9ec
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82859530"
---
# <a name="satellite-assembly-loading-algorithm"></a>サテライト アセンブリの読み込みアルゴリズム

サテライト アセンブリは、言語およびカルチャ用にカスタマイズされたローカライズされたリソースを格納するために使用されます。

サテライトアセンブリは、一般的なマネージド アセンブリとは異なる読み込みアルゴリズムを使用します。

## <a name="when-are-satellite-assemblies-loaded"></a>サテライト アセンブリが読み込まれるタイミング

サテライト アセンブリは、ローカライズされたリソースを読み込むときに読み込まれます。

ローカライズされたリソースを読み込む基本的な API は <xref:System.Resources.ResourceManager?displayProperty=fullName> クラスです。 最終的に <xref:System.Resources.ResourceManager> クラスは、<xref:System.Globalization.CultureInfo.Name?displayProperty=nameWithType> ごとに <xref:System.Reflection.Assembly.GetSatelliteAssembly%2A> メソッドを呼び出します。

上位レベルの API は、低レベルの API を抽象化する場合があります。

## <a name="algorithm"></a>アルゴリズム

.NET Core リソース フォールバック プロセスには次の手順が含まれます。

1. `active`<xref:System.Runtime.Loader.AssemblyLoadContext> インスタンスを決定します。 いずれの場合も、`active` インスタンスは実行中のアセンブリの <xref:System.Runtime.Loader.AssemblyLoadContext> です。

2. `active` インスタンスは、要求されたカルチャのサテライト アセンブリの読み込みを、以下の優先順位で試行します。
    - キャッシュを調べます。
    - 現在実行中のアセンブリのディレクトリで、要求された <xref:System.Globalization.CultureInfo.Name?displayProperty=nameWithType> (`es-MX` など) と一致するサブディレクトリがないか調べます。

        > [!NOTE]
        > この機能は、3.0 より前の .NET Core では実装されていませんでした。
        >
        > [!NOTE]
        > Linux と macOS では、サブディレクトリは大文字と小文字が区別されるため、次のいずれかでなければなりません。
        >
        > - 大文字と小文字が完全に一致している。
        > - 小文字になっている。

    - `active` が <xref:System.Runtime.Loader.AssemblyLoadContext.Default?displayProperty=nameWithType> インスタンスの場合は、[既定のサテライト (リソース) アセンブリ プローブ](default-probing.md#satellite-resource-assembly-probing) ロジックを実行します。

    - <xref:System.Runtime.Loader.AssemblyLoadContext.Load%2A?displayProperty=nameWithType> 関数を呼び出します。

    - <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving?displayProperty=nameWithType> イベントを発生させます。

    - <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> イベントを発生させます。

3. サテライト アセンブリが読み込まれる場合は、次のようになります。
   - <xref:System.AppDomain.AssemblyLoad?displayProperty=nameWithType> イベントが発生します。
   - アセンブリ内で要求されたリソースが検索されます。 ランタイムによってアセンブリ内でリソースが見つかると、それを使用します。 リソースが見つからない場合は、検索を続けます。

    > [!NOTE]
    > サテライト アセンブリ内のリソースを見つけるために、ランタイムでは現在の <xref:System.Globalization.CultureInfo.Name?displayProperty=nameWithType> の <xref:System.Resources.ResourceManager> によって要求されたリソース ファイルが検索されます。 リソース ファイル内で、要求されたリソース名が検索されます。 いずれかが見つからない場合、リソースは見つからなかったものとして扱われます。

4. 次に、ランタイムは、考えられる多数のレベルについて親カルチャ アセンブリを検索し、それぞれで手順 2 および 3 を繰り返します。

    各カルチャの親は 1 つだけで、<xref:System.Globalization.CultureInfo.Parent%2A?displayProperty=nameWithType> プロパティによって定義されています。

    カルチャの <xref:System.Globalization.CultureInfo.Parent%2A> プロパティが <xref:System.Globalization.CultureInfo.InvariantCulture?displayProperty=nameWithType> のとき、親カルチャの検索は停止します。

    <xref:System.Globalization.CultureInfo.InvariantCulture> については、手順 2 および 3 に戻らず、手順 5 に進みます。

5. リソースがまだ見つからない場合は、既定の (フォールバック) カルチャのリソースが使用されます。

   通常、既定のカルチャのリソースは、メイン アプリケーション アセンブリに格納されています。 ただし、<xref:System.Resources.NeutralResourcesLanguageAttribute.Location?displayProperty=nameWithType> プロパティに <xref:System.Resources.UltimateResourceFallbackLocation.Satellite?displayProperty=nameWithType> を指定することができます。 この値は、リソースの最終的なフォールバックの場所が、メイン アセンブリではなくサテライト アセンブリであることを示します。

    > [!NOTE]
    > 既定のカルチャは、最終的なフォールバックです。 したがって、既定のリソース ファイルにリソースの網羅的なセットを常に含めることをお勧めします。 これは、例外がスローされるのを防ぐのに役立ちます。 網羅的なセットを含めることにより、すべてのリソースに対してフォールバックが提供され、固有のカルチャではなくても、常に少なくとも 1 つのリソースがユーザーに存在することが保証されます。

6. 最後に、
   - ランタイムで既定の (フォールバック) カルチャのリソース ファイルが見つからない場合は、<xref:System.Resources.MissingManifestResourceException> または <xref:System.Resources.MissingSatelliteAssemblyException> 例外がスローされます。
   - リソース ファイルが見つかり、要求されたリソースが存在しない場合は、要求から `null` が返されます。
