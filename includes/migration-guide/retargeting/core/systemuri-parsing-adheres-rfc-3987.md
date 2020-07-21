---
ms.openlocfilehash: 9c3c0bf7fbd8d45eba84eaa8634fd2d834195702
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617207"
---
### <a name="systemuri-parsing-adheres-to-rfc-3987"></a>System.Uri 解析が RFC 3987 に準拠

#### <a name="details"></a>説明

.NET Framework 4.5 では、URI 解析がいくつかの点で変更されました。 ただし、これらの変更は .NET Framework 4.5 を対象としたコードのみに影響することに注意してください。 バイナリが .NET Framework 4.0 を対象としている場合、以前の動作が実行されます。 .NET Framework 4.5 での URI 解析の変更は次のとおりです。

- URI 解析は、RFC 3987 の最新の IRI 規則に従って、正規化と文字チェックを実行します。
- Unicode 正規化フォーム C は、URI のホスト部分でのみ実行されます。
- 無効な mailto:URI は、例外の原因になります。
- パス セグメントの最後の末尾のドットが保存されるようになりました。
- `file://` URI は `?` 文字をエスケープしません。
- Unicode 制御文字の `U+0080` から `U+009F` まではサポートされません。
- コンマ文字 `,` または `%2c` は自動的にエスケープ解除されません。

#### <a name="suggestion"></a>提案される解決策

古い .NET Framework 4.0 URI 解析セマンティクスが必要な場合 (めったにありません)、.NET Framework 4.0 を対象とすることによって使用できます。 これは、アセンブリで <xref:System.Runtime.Versioning.TargetFrameworkAttribute?displayProperty=fullName> を使用することによって、または、[プロジェクトのプロパティ] ページの Visual Studio のプロジェクト システム UI によって実現できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Uri.%23ctor(System.String)>
- <xref:System.Uri.%23ctor(System.String,System.Boolean)>
- <xref:System.Uri.%23ctor(System.String,System.UriKind)>
- <xref:System.Uri.%23ctor(System.Uri,System.String)>
- <xref:System.Uri.TryCreate(System.String,System.UriKind,System.Uri@)?displayProperty=nameWithType>
- <xref:System.Uri.TryCreate(System.Uri,System.String,System.Uri@)?displayProperty=nameWithType>
- <xref:System.Uri.TryCreate(System.Uri,System.Uri,System.Uri@)?displayProperty=nameWithType>
