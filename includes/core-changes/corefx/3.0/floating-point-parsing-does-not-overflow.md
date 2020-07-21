---
ms.openlocfilehash: 935d9b2368ea4a0eeca7943dcbd584d24d2a6633
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721167"
---
### <a name="floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception"></a>浮動小数点の解析操作が失敗したり OverflowException がスローされたりすることがなくなった

浮動小数点の解析メソッドが、<xref:System.Single> または <xref:System.Double> 浮動小数点の型の範囲外の数値を持つ文字列を解析する場合に、<xref:System.OverflowException> をスローしたり、`false` を返したりすることがなくなりました。

#### <a name="change-description"></a>変更の説明

.NET Core 2.2 以前のバージョンでは、<xref:System.Double.Parse%2A?displayProperty=nameWithType> および <xref:System.Single.Parse%2A?displayProperty=nameWithType> メソッドは、それぞれの型の範囲外の値に対して、<xref:System.OverflowException> をスローします。 <xref:System.Double.TryParse%2A?displayProperty=nameWithType> および <xref:System.Single.TryParse%2A?displayProperty=nameWithType> メソッドは、範囲外の数値を持つ文字列表現に対して `false` を返します。

.NET Core 3.0 以降、範囲外の数値文字列を解析するときに、<xref:System.Double.Parse%2A?displayProperty=nameWithType>、<xref:System.Double.TryParse%2A?displayProperty=nameWithType>、<xref:System.Single.Parse%2A?displayProperty=nameWithType>、および <xref:System.Single.TryParse%2A?displayProperty=nameWithType> の各メソッドが失敗しなくなりました。 代わりに、<xref:System.Double> の解析メソッドが、<xref:System.Double.MaxValue?displayProperty=nameWithType> を超過する値に対して <xref:System.Double.PositiveInfinity?displayProperty=nameWithType> を返し、また <xref:System.Double.MinValue?displayProperty=nameWithType> 未満の値に対して <xref:System.Double.NegativeInfinity?displayProperty=nameWithType> を返すようになりました。 同様に、<xref:System.Single> の解析メソッドが、<xref:System.Single.MaxValue?displayProperty=nameWithType> を超過する値に対して <xref:System.Single.PositiveInfinity?displayProperty=nameWithType> を返し、また <xref:System.Single.MinValue?displayProperty=nameWithType> 未満の値に対して <xref:System.Single.NegativeInfinity?displayProperty=nameWithType> を返すようになりました。

この変更は、IEEE 754:2008 に対する準拠の改善のために行われました。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="recommended-action"></a>推奨アクション

この変更は、次の 2 つのいずれかの方法でコードに影響を与える可能性があります。

- コードは、オーバーフローが発生したときに実行される <xref:System.OverflowException> のハンドラーに依存します。 この場合、`catch` ステートメントを削除し、<xref:System.Double.IsInfinity%2A?displayProperty=nameWithType> または <xref:System.Single.IsInfinity%2A?displayProperty=nameWithType> が `true` であるかをテストする任意のコードを `If` ステートメントに含める必要があります。

- コードは、浮動小数点値が `Infinity` ではないことを前提としています。 この場合は、必要な `PositiveInfinity` および `NegativeInfinity` の浮動小数点値を確認するコードを追加する必要があります。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Double.Parse%2A?displayProperty=nameWithType>
- <xref:System.Double.TryParse%2A?displayProperty=nameWithType>
- <xref:System.Single.Parse%2A?displayProperty=nameWithType>
- <xref:System.Single.TryParse%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:System.Double.Parse`
- `Overload:System.Double.TryParse`
- `Overload:System.Single.Parse`
- `Overload:System.Single.TryParse`

-->
