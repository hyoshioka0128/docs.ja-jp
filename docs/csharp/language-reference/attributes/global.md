---
title: C# の予約済み属性:グローバル属性
ms.date: 04/09/2020
description: 属性は、プログラムのセマンティクスをさらに理解するためにコンパイラから使用されるメタデータを提供します
ms.openlocfilehash: f855f32cd7349da34ffbd20fededdf42c3023938
ms.sourcegitcommit: c91110ef6ee3fedb591f3d628dc17739c4a7071e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2020
ms.locfileid: "81389806"
---
# <a name="reserved-attributes-assembly-level-attributes"></a>予約済みの属性:アセンブリ レベルの属性

ほとんどの属性は、クラスやメソッドなど、特定の言語要素に適用されます。ただし、属性の中にはグローバルなものがあり、アセンブリまたはモジュール全体に適用されます。 たとえば、<xref:System.Reflection.AssemblyVersionAttribute> 属性は、次のように、バージョン情報をアセンブリに埋め込むときに使用できます。

```csharp
[assembly: AssemblyVersion("1.0.0.0")]
```

ソース コードでは、グローバル属性は、トップレベルの `using` ディレクティブより後、型、モジュール、または名前空間の宣言より前に指定します。 グローバル属性は複数のソース ファイルに指定できますが、それらのファイルは、1 つのコンパイル パスでコンパイルする必要があります。 Visual Studio によって、.NET Framework プロジェクトの AssemblyInfo.cs ファイルにグローバル属性が追加されます。 これらの属性は、.NET Core プロジェクトには追加されません。

アセンブリの属性は、アセンブリに関する情報を提供する値です。 これらは次のカテゴリに分けられます。

- アセンブリ ID 属性
- 情報属性
- アセンブリ マニフェスト属性

## <a name="assembly-identity-attributes"></a>アセンブリ ID 属性

アセンブリの ID は、名前、バージョン、カルチャの 3 つの属性によって識別されます (適用できる場合は厳密な名前も使用されます)。 アセンブリの完全な名前を形成するこれらの属性は、コード内でアセンブリを参照するときに必要になります。 アセンブリのバージョンとカルチャは、属性を使用して設定できます。 ただし、名前の値は、コンパイラ、[[アセンブリ情報] ダイアログ ボックス](/visualstudio/ide/reference/assembly-information-dialog-box)の Visual Studio IDE、またはアセンブリ リンカー (Al.exe) (アセンブリの作成時) によって設定されます。 アセンブリ名は、アセンブリ マニフェストに基づいています。 <xref:System.Reflection.AssemblyFlagsAttribute> 属性は、アセンブリの複数のコピーが共存できるかどうかを指定します。

次の表に ID 属性を示します。

|属性|目的|
|---------------|-------------|
|<xref:System.Reflection.AssemblyVersionAttribute>|アセンブリのバージョンを指定します。|
|<xref:System.Reflection.AssemblyCultureAttribute>|アセンブリがサポートするカルチャを指定します。|
|<xref:System.Reflection.AssemblyFlagsAttribute>|同じコンピューター、同じプロセス、または同じアプリケーション ドメインでの side-by-side 実行をアセンブリがサポートするかどうかを指定します。|

## <a name="informational-attributes"></a>情報属性

情報属性は、追加の会社情報または製品情報をアセンブリに指定する場合に使用します。 次の表は、<xref:System.Reflection?displayProperty=nameWithType> 名前空間で定義されている情報属性を示しています。

|属性|目的|
|---------------|-------------|
|<xref:System.Reflection.AssemblyProductAttribute>|アセンブリ マニフェストの製品名を指定します。|
|<xref:System.Reflection.AssemblyTrademarkAttribute>|アセンブリ マニフェストの商標を指定します。|
|<xref:System.Reflection.AssemblyInformationalVersionAttribute>|アセンブリ マニフェストの情報バージョンを指定します。|
|<xref:System.Reflection.AssemblyCompanyAttribute>|アセンブリ マニフェストの会社名を指定します。|
|<xref:System.Reflection.AssemblyCopyrightAttribute>|アセンブリ マニフェストの著作権を指定するカスタム属性を定義します。|
|<xref:System.Reflection.AssemblyFileVersionAttribute>|Win32 ファイル バージョン リソースの特定のバージョン番号を設定します。|
|<xref:System.CLSCompliantAttribute>|アセンブリが共通言語仕様 (CLS) に準拠しているかどうかを示します。|

## <a name="assembly-manifest-attributes"></a>アセンブリ マニフェスト属性

アセンブリ マニフェスト属性を使用すると、アセンブリ マニフェストの情報を指定できます。 属性には、タイトル、説明、既定のエイリアス、および構成が含まれます。 次の表は、<xref:System.Reflection?displayProperty=nameWithType> 名前空間で定義されているアセンブリ マニフェスト属性を示しています。

|属性|目的|
|---------------|-------------|
|<xref:System.Reflection.AssemblyTitleAttribute>|アセンブリ マニフェストのアセンブリ タイトルを指定します。|
|<xref:System.Reflection.AssemblyDescriptionAttribute>|アセンブリ マニフェストのアセンブリの説明を指定します。|
|<xref:System.Reflection.AssemblyConfigurationAttribute>|アセンブリ マニフェストのアセンブリ構成 (小売、デバッグなど) を指定します。|
|<xref:System.Reflection.AssemblyDefaultAliasAttribute>|アセンブリ マニフェストのわかりやすい既定の別名を定義します。|
