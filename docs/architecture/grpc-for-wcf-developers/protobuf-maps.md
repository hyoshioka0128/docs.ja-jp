---
title: Protobuf maps for dictionary-gRPC for WCF 開発者
description: Protobuf maps を使用してを表す方法について説明します。NET の辞書型。
ms.date: 09/09/2019
ms.openlocfilehash: 8b4f29daa263f329dc533d3ddc596d0f47c1b6e0
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967422"
---
# <a name="protobuf-maps-for-dictionaries"></a>Protobuf のディクショナリのマップ

メッセージ内の名前付きの値の任意のコレクションを表すことができることが重要です。 .NET では、通常、ディクショナリ型を使用して処理されます。 Protobuf は、.NET <xref:System.Collections.Generic.IDictionary%602> 型に相当 `map<key_type, value_type>` 型です。 このセクションでは、Protobuf で `map` を宣言する方法と、生成されたコードを使用する方法について説明します。

```protobuf
message StockPrices {
    map<string, double> prices = 1;
}
```

生成されたコードでは、`map` フィールドは、<xref:System.Collections.Generic.IDictionary%602>を含む標準の .NET コレクションインターフェイスを実装する `Google.Protobuf.Collections.MapField<TKey, TValue>` クラスを使用します。

マップフィールドは、メッセージ定義内で直接繰り返すことはできませんが、次の例のように、マップを含む入れ子になったメッセージを作成し、メッセージの種類で `repeated` を使用することができます。

```protobuf
message Order {
    message Attributes {
        map<string, string> values = 1;
    }
    repeated Attributes attributes = 1;
}
```

## <a name="using-mapfield-properties-in-code"></a>コードでの MapField プロパティの使用

`map` フィールドから生成された `MapField` プロパティは読み取り専用であり、`null`されることはありません。 マッププロパティを設定するには、空の `MapField` プロパティの `Add(IDictionary<TKey,TValue> values)` メソッドを使用して、任意の .NET ディクショナリから値をコピーします。

```csharp
public Order CreateOrder(Dictionary<string, string> attributes)
{
    var order = new Order();
    order.Attributes.Add(attributes);
    return order;
}
```

## <a name="further-reading"></a>関連項目

Protobuf の詳細については、公式の[Protobuf のドキュメント](https://developers.google.com/protocol-buffers/docs/overview)を参照してください。

>[!div class="step-by-step"]
>[前へ](protobuf-enums.md)
>[次へ](wcf-services-to-grpc-comparison.md)
