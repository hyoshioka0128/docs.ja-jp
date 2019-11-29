---
title: リストと配列の繰り返しフィールド-WCF 開発者向けの gRPC
description: コレクションが Protobuf によってどのように処理され、.NET コレクションにどのように関連しているかを理解します。
ms.date: 09/09/2019
ms.openlocfilehash: 17c579bc98ba62ea74b9452bdb28efd96fc51406
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967364"
---
# <a name="repeated-fields-for-lists-and-arrays"></a>リストと配列の繰り返しフィールド

リストは、`repeated` prefix キーワードを使用して Protobuf で指定されます。 次の例は、リストを作成する方法を示しています。

```protobuf
message Person {
    // Other fields elided
    repeated string aliases = 8;
}
```

生成されたコードでは、`repeated` フィールドは、組み込みの .NET コレクション型ではなく、`Google.Protobuf.Collections.RepeatedField<T>` ジェネリック型によって表されます。 `RepeatedField<T>` 型には、リストをバイナリワイヤ形式にシリアル化および逆シリアル化するために必要なコードが含まれています。 <xref:System.Collections.Generic.IList%601> や <xref:System.Collections.Generic.IEnumerable%601>などの標準的な .NET コレクションインターフェイスがすべて実装されているため、LINQ クエリを使用したり、配列やリストに簡単に変換したりできます。

>[!div class="step-by-step"]
>[前へ](protobuf-nested-types.md)
>[次へ](protobuf-reserved.md)
