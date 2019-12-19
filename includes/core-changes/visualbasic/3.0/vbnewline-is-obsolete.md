---
ms.openlocfilehash: 86cdb845c436f424bbcc70e0736568031143b204
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74567463"
---
### <a name="microsoftvisualbasicconstantsvbnewline-is-obsolete"></a>Microsoft.VisualBasic.Constants.vbNewLine は古い

<xref:Microsoft.VisualBasic.Constants.vbNewLine?displayProperty=fullName> 定数は、.NET Core 3.0 Preview 8 以降では[廃止](xref:System.ObsoleteAttribute)としてマークされています。

#### <a name="version-introduced"></a>導入されたバージョン

3.0 Preview 8

#### <a name="change-description"></a>変更の説明

.NET Core 3.0 Preview 8 以降では、[廃止](xref:System.ObsoleteAttribute)属性が <xref:Microsoft.VisualBasic.Constants.vbNewLine?displayProperty=fullName> 定数に適用されています。 その定数を使用すると、コンパイラの警告が発生します。 .NET Core と .NET Framework の両方の以前のリリースでは、廃止としてマークされていませんでした。

この変更は、Visual Basic をマルチプラットフォーム開発用の言語としてサポートするために行われました。 `vbNewLine` 定数は、Windows での改行文字シーケンスである `\r\n` と同等です。 Unix ベースのシステムでは、改行文字は `\n` です。

#### <a name="recommended-action"></a>推奨される操作

`vbNewLine` に対する[廃止](xref:System.ObsoleteAttribute)属性メッセージには、次の推奨事項が含まれています。

> キャリッジ リターンとライン フィードの場合は、[vbCrLf](xref:Microsoft.VisualBasic.Constants.vbCrLf) を使用します。 現在のプラットフォームの改行の場合は、<xref:System.Environment.NewLine?displayProperty=nameWithType> を使用します。

#### <a name="category"></a>カテゴリ

Visual Basic

#### <a name="affected-apis"></a>影響を受ける API

- <xref:Microsoft.VisualBasic.Constants.vbNewLine?displayProperty=fullName>

<!--

### Affected APIs

- `F:Microsoft.VisualBasic.Constants.vbNewLine`

-->
