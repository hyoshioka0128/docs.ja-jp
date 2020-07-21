---
ms.openlocfilehash: b3cc04d5675ea63a0a6b967e293da8a1bd79830d
ms.sourcegitcommit: d7666f6e49c57a769612602ea7857b927294ce47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/30/2020
ms.locfileid: "82595684"
---
### <a name="uribuilder-properties-no-longer-prepend-leading-characters"></a>UriBuilder では今後、先頭に文字が付加されない

<xref:System.UriBuilder.Fragment?displayProperty=nameWithType> では今後、`#` 文字が先頭に付加されず、<xref:System.UriBuilder.Query?displayProperty=nameWithType> では今後、`?` 文字が先頭に付加されません (既に付いている場合)。

#### <a name="change-description"></a>変更の説明

.NET Framework では、<xref:System.UriBuilder.Fragment?displayProperty=nameWithType> プロパティと <xref:System.UriBuilder.Query?displayProperty=nameWithType> プロパティでは常にそれぞれ、`#` 文字と `?` 文字が保存中の値の先頭に付加されます。 この動作の結果、文字列に既に `#` 文字または `?` 文字が含まれている場合、保存中の値にこれらの先頭文字が複数与えられることになります。 たとえば、<xref:System.UriBuilder.Fragment?displayProperty=nameWithType> の値が `##main` になることがあります。

.NET Core 1.0 以降、これらのプロパティでは今後、文字列の先頭に `#` 文字または `?` 文字が既に存在する場合、これらの文字が先頭に付加されません。

#### <a name="version-introduced"></a>導入されたバージョン

1

#### <a name="recommended-action"></a>推奨アクション

プロパティ値を設定するとき、これらの先頭文字を明示的に削除する必要がなくなりました。 これは特に、値を付加するときに便利です。付加するたびに先頭の `#` または `?` を削除する必要がないためです。

たとえば、次のコード スニペットからは、.NET Framework と .NET Core では動作に違いがあることがわかります。

```csharp
var builder = new UriBuilder();
builder.Query = "one=1";
builder.Query += "&two=2";
builder.Query += "&three=3";
builder.Query += "&four=4";

Console.WriteLine(builder.Query);
```

- .NET Framework の場合、出力は `????one=1&two=2&three=3&four=4` です。
- .NET Core の場合、出力は `?one=1&two=2&three=3&four=4` です。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.UriBuilder.Fragment?displayProperty=fullName>
- <xref:System.UriBuilder.Query?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.UriBuilder.Fragment`
- `T:System.UriBuilder.Query`

-->
