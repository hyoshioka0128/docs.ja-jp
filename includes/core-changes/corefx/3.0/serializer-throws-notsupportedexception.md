---
ms.openlocfilehash: cc3251e3b31143bd95793b407e50cf76e0e30142
ms.sourcegitcommit: 348bb052d5cef109a61a3d5253faa5d7167d55ac
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82021660"
---
### <a name="json-serializer-exception-type-changed-from-jsonexception-to-notsupportedexception"></a>`JsonException` から `NotSupportedException` に変更された Json シリアライザーの例外の型

.NET Core 3.0 Preview 6 から 8 では、サポート対象外の派生コレクション型が検出されると、<xref:System.Text.Json.JsonException> がスローされます。 .NET Core 3.0 Preview 9 以降では、シリアライザーによって <xref:System.NotSupportedException> が代わりにスローされます。

#### <a name="change-description"></a>変更の説明

.NET Core 3.0 Preview 6 から Preview 8 では、サポート対象外の派生コレクション型が検出されると、<xref:System.Text.Json.JsonException> がスローされます。 "*サポート対象外の派生コレクション型*" とは、次のいずれかの型に割り当てることができない任意のコレクション型です。

- <xref:System.Collections.IList>
- <xref:System.Collections.Generic.ICollection%601>
- <xref:System.Collections.Generic.Stack%601>
- <xref:System.Collections.Generic.Queue%601>
- <xref:System.Collections.IDictionary>
- [IDictionary\<String,T>](xref:System.Collections.Generic.IDictionary%602)

.NET Core 3.0 Preview 9 以降では、シリアライザーでサポート対象外のコレクション型が検出されると、<xref:System.NotSupportedException> がスローされます。 新しい例外の型の方が、逆シリアル化操作が失敗する理由がよくわかります。

#### <a name="version-introduced"></a>導入されたバージョン

3.0 Preview 9

#### <a name="recommended-action"></a>推奨アクション

逆シリアル化時に <xref:System.Text.Json.JsonException> をキャッチする場合は、<xref:System.NotSupportedException> もキャッチすることを検討してください。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType>
- <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Deserialize`
- `Overload:System.Text.Json.JsonSerializer.DeserializeAsync`

-->
