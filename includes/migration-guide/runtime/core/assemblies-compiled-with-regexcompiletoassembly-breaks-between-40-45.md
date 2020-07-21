---
ms.openlocfilehash: 0bd90b3d479a7e0897aaf78b7718ae156a4a239f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620192"
---
### <a name="assemblies-compiled-with-regexcompiletoassembly-breaks-between-40-and-45"></a>Regex.CompileToAssembly でコンパイルされたアセンブリは 4.0 と 4.5 の間で区別されます

#### <a name="details"></a>説明

コンパイル済みの正規表現のアセンブリが .NET Framework 4.5 でビルドされ、.NET Framework 4 を対象としている場合、.NET Framework 4 がインストールされているシステム上でそのアセンブリの正規表現の 1 つを使用しようとすると、例外をスローします。

#### <a name="suggestion"></a>提案される解決策

この問題を回避するには、次のいずれかの方法を実行します。<ul><li>.NET Framework 4 を使用して正規表現を含むアセンブリをビルドします。</li><li>解釈される正規表現を使用します。</li></ul>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName)?displayProperty=nameWithType></li><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName,System.Reflection.Emit.CustomAttributeBuilder[])?displayProperty=nameWithType></li><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName,System.Reflection.Emit.CustomAttributeBuilder[],System.String)?displayProperty=nameWithType></li></ul>|
