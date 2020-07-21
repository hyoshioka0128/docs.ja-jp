---
title: 明示的なインターフェイスの実装 - C# プログラミング ガイド
ms.date: 01/24/2020
helpviewer_keywords:
- explicit interfaces [C#]
- interfaces [C#], explicit
ms.assetid: 181c901f-0d4c-4f29-97fc-895079617bf2
ms.openlocfilehash: ea32a279b7c464174a7fada5ef93ccf62ef39884
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "79167674"
---
# <a name="explicit-interface-implementation-c-programming-guide"></a>明示的なインターフェイスの実装 (C# プログラミング ガイド)

シグネチャが同じメンバーが含まれる 2 つのインターフェイスをある[クラス](../../language-reference/keywords/class.md)が実装する場合、そのクラスでそのメンバーを実装することで、実装としてそのメンバーが両方のインターフェイスで使用されます。 次の例では、`Paint` のすべての呼び出しで同じメソッドが呼び出されます。 この最初のサンプルでは、型が定義されます。

[!code-csharp[DefineSimpleTypes](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#DefineTypes)]

次のサンプルでは、メソッドが呼び出されます。

[!code-csharp[DefineSimpleTypes](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#CallMethods)]

2 つのインターフェイス メンバーで同じ関数を実行しない場合、一方または両方のインターフェイスが正しく実装されません。 インターフェイス メンバーは明示的に実装できます。そのインターフェイス経由でのみ呼び出され、そのインターフェイスに固有となるクラス メンバーが作成されます。 インターフェイスの名前とピリオドを利用してクラス メンバーに名前を付けます。 次に例を示します。

[!code-csharp[DefineExplicitImplementation](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#ExplicitImplementation)]

クラス メンバー `IControl.Paint` は `IControl` インターフェイス経由でのみ利用できます。`ISurface.Paint` は `ISurface` 経由でのみ利用できます。 いずれのメソッド実装も個別であり、どちらもクラスで直接利用できません。 次に例を示します。

[!code-csharp[CallExplicitImplementation](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#CallExplicitImplementation)]

2 つのインターフェイスで、それぞれが同じ名前の別のメンバー (プロパティやメソッドなど) を宣言するような場合の解決には、明示的な実装も利用されます。 両方のインターフェイスを実装するには、コンパイラ エラーを回避するために、クラスはプロパティ `P`、メソッド `P`、または両方に明示的な実装を利用する必要があります。 次に例を示します。

[!code-csharp[NameCollisions](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#NameCollision)]

[C# 8.0](../../whats-new/csharp-8.md#default-interface-methods) 以降では、インターフェイスで宣言されたメンバーの実装を定義できます。 クラスでインターフェイスからメソッド実装が継承される場合、そのメソッドにはインターフェイス型の参照を利用する方法でのみアクセスできます。 継承したメンバーは、パブリック インターフェイスの一部として表示されません。 次のサンプルでは、インターフェイス メソッドの既定の実装が定義されます。

[!code-csharp[NameCollisions](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#DefaultImplementation)]

次のサンプルでは、既定の実装が呼び出されます。

[!code-csharp[NameCollisions](~/samples/snippets/csharp/interfaces/ExplicitImplementation.cs#CallDefaultImplementation)]

`IControl` インターフェイスを実装するあらゆるクラスによって、既定の `Paint` メソッドをパブリック メソッドか明示的なインターフェイス実装としてオーバーライドできます。

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [クラスと構造体](../classes-and-structs/index.md)
- [インターフェイス](./index.md)
- [継承](../classes-and-structs/inheritance.md)
