---
title: インターフェイスのインデクサー - C# プログラミング ガイド
ms.date: 02/08/2020
helpviewer_keywords:
- indexers [C#], in interfaces
- accessors [C#], indexers
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
ms.openlocfilehash: 9ce6e4f0e0533c2880c6241f44409435248a336a
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287481"
---
# <a name="indexers-in-interfaces-c-programming-guide"></a>インターフェイスのインデクサー (C# プログラミング ガイド)

[interface](../../language-reference/keywords/interface.md) でインデクサーを宣言することができます。 インターフェイスのインデクサーのアクセサーは、[クラス](../../language-reference/keywords/class.md)のインデクサーのアクセサーと次の点で異なります。

- インターフェイスのアクセサーは、修飾子は使用しません。
- インターフェイスのアクセサーには通常、本文がありません。

アクセサーの目的は、インデクサーが読み取り/書き込み、読み取り専用、書き込み専用のどれかを示すことです。 インデクサーの実装をインターフェイスに定義できますが、めったに行われません。 インデクサーでは通常、データ フィールドにアクセスするための API が定義されます。データ フィールドはインターフェイスで定義できません。

インターフェイスのインデクサー アクセサーの例を次に示します。

[!code-csharp[DefineInterface](~/samples/snippets/csharp/interfaces/indexers.cs#DefineIndexer)]

インデクサーのシグネチャは、同じインターフェイスで宣言されている他のすべてのインデクサーの署名とは異なる必要があります。

## <a name="example"></a>例

次の例では、インターフェイスのインデクサーを実装する方法について説明します。

[!code-csharp[Implement](~/samples/snippets/csharp/interfaces/indexers.cs#ImplementInterface)]

[!code-csharp[DefineInterface](~/samples/snippets/csharp/interfaces/indexers.cs#ExampleCode)]

前の例では、インターフェイス メンバーの完全修飾名を使用して明示的なインターフェイス メンバーの実装を使用することができます。 次に例を示します。

```csharp
string IIndexInterface.this[int index]
{
}
```

ただし、完全修飾名は、クラスが同じインデクサーの署名を持つ 2 つ以上のインターフェイスを実装するときにあいまいさを避けるためにのみ必要です。 たとえば、`Employee` クラスが 2 つのインターフェイス `ICitizen` と `IEmployee` を実装し、両方のインターフェイスが同じインデクサーの署名を持っている場合、明示的なインターフェイス メンバーの実装が必要です。 つまり、次のインデクサーの宣言があります。

```csharp
string IEmployee.this[int index]
{
}
```

これは、`IEmployee` インターフェイス上でインデクサーを実装します。次の宣言があります。

```csharp
string ICitizen.this[int index]
{
}
```

これは、`ICitizen` インターフェイスでインデクサーを実装します。

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [インデクサー](./index.md)
- [プロパティ](../classes-and-structs/properties.md)
- [インターフェイス](../interfaces/index.md)
