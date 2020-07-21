---
ms.openlocfilehash: 26a001ec2009a1a66dd9038b9bd3a42d7bcefb73
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620255"
---
### <a name="missing-target-framework-moniker-results-in-40-behavior"></a>ターゲット フレームワーク モニカーがないと、4.0 の動作になる

#### <a name="details"></a>説明

アセンブリ レベルで <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=fullName> が適用されていないアプリケーションは、自動的に .NET Framework 4.0 のセマンティクス (quirks) を使用して実行します。 高い品質を確保するには、すべてのバイナリを、ビルドされた .NET Framework のバージョンを示す <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=fullName> で明示的に属性指定することをお勧めします。 プロジェクト ファイルでターゲット フレームワーク モニカーを使用すると、MSBuid は <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=fullName> を自動的に適用します。

#### <a name="suggestion"></a>提案される解決策

<xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=fullName> は、属性をアセンブリに直接追加するか、[プロジェクト ファイルで、または Visual Studio のプロジェクト プロパティ GUI](https://devblogs.microsoft.com/visualstudio/visual-studio-managed-multi-targeting-part-1-concepts-target-framework-moniker-target-framework/) でターゲット フレームワークを指定することによって指定する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |Major|
|バージョン|4.5|
|種類|ランタイム|
