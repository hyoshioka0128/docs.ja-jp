---
ms.openlocfilehash: 3300a74b81fc9eeba670ee0ceb2c2615fd3925bd
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617220"
---
### <a name="listlttgtforeach-can-throw-exception-when-modifying-list-item"></a>List&lt;T&gt;.ForEach は、リスト項目を変更すると、例外をスローすることがあります。

#### <a name="details"></a>説明

.NET Framework 4.5 から、<xref:System.Collections.Generic.List%601.ForEach(System.Action{%600})> 列挙子は、呼び出し元のコレクション内の要素が変更された場合、<xref:System.InvalidOperationException?displayProperty=fullName> 例外をスローします。 以前は、この様な場合、例外はスローされませんでしたが、競合状態になることがありました。

#### <a name="suggestion"></a>提案される解決策

理想的には、安全な操作ではないため、要素の列挙中にリストを変更しないようにコードを修正する必要があります。 ただし、以前の動作に戻すには、アプリを .NET Framework 4.0 向けにできます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Collections.Generic.List%601.ForEach(System.Action{%600})?displayProperty=nameWithType>
