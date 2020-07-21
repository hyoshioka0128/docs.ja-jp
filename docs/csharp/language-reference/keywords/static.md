---
title: static 修飾子 - C# リファレンス
ms.date: 04/22/2020
f1_keywords:
- static
- static_CSharpKeyword
helpviewer_keywords:
- static keyword [C#]
ms.assetid: 5509e215-2183-4da3-bab4-6b7e607a4fdf
ms.openlocfilehash: 771bcfdac4c4bf27c15da4bc374d804405317a78
ms.sourcegitcommit: 73aa9653547a1cd70ee6586221f79cc29b588ebd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82102061"
---
# <a name="static-c-reference"></a>static (C# リファレンス)

このページでは、`static` 修飾子キーワードについて説明します。 `static` キーワードも [`using static`](using-static.md) ディレクティブに含まれます。

`static` 修飾子は、静的メンバーの宣言に使用します。静的メンバーは、特定のオブジェクトではなく、型自体に属するメンバーです。 `static` 修飾子は `static` クラスの宣言に使用できます。 クラス、インターフェイス、構造体では、`static` 修飾子をフィールド、メソッド、プロパティ、演算子、イベント、コンストラクターに追加できます。 `static` 修飾子はインデクサーおよびファイナライザーと併用できません。 詳細については、「[静的クラスと静的クラス メンバー](../../programming-guide/classes-and-structs/static-classes-and-static-class-members.md)」を参照してください。

## <a name="example---static-class"></a>例 - 静的クラス

次のクラスは `static` として宣言され、`static` メソッドのみが含まれます。

[!code-csharp[csrefKeywordsModifiers#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#18)]

定数宣言や型宣言は暗黙的な `static` メンバーです。 `static` メンバーはインスタンスを使って参照できません。 代わりに、型の名前を使って参照します。 たとえば、次のクラスを考えてみます。

[!code-csharp[csrefKeywordsModifiers#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#19)]

`static` メンバー `x` を参照するには、同じスコープからその静的メンバーにアクセス可能でない限り、完全修飾名 (`MyBaseC.MyStruct.x`) を使用します。

```csharp
Console.WriteLine(MyBaseC.MyStruct.x);
```

クラスのインスタンスには、そのクラスのインスタンス フィールドすべてにそれぞれのコピーが含まれていますが、各 `static` フィールドのコピーは 1 つだけです。

`static` メソッドまたはプロパティ アクセサーへの参照には、[`this`](this.md) は使用できません。

`static` キーワードをクラスに適用する場合、そのクラスのすべてのメンバーが `static` でなければなりません。

クラス、インターフェイス、`static` クラスには、`static` コンストラクターを含めることができます。 `static` コンストラクターは、プログラムが開始されてからクラスがインスタンス化されるまでの間に呼び出されます。

> [!NOTE]
> `static` キーワードの用法は、C++ の場合よりも制限されています。 C++ キーワードと比較するには、「[ストレージ クラス (C++)](/cpp/cpp/storage-classes-cpp#static)」をご覧ください。

`static` メンバーの例を示すために、ある企業の従業員を表すクラスを考えてみます。 このクラスには、従業員数を数えるメソッドと、従業員数を格納するフィールドがあります。 メソッドとフィールドはどちらも、従業員のインスタンスに属しておらず、 全体として従業員のクラスに属しています。 クラスの `static` メンバーとして宣言する必要があります。

## <a name="example---static-field-and-method"></a>例 - 静的フィールドとメソッド

この例では、新しい従業員の名前と ID を読み取り、従業員数のカウンターを 1 つインクリメントして、新しい従業員の情報と従業員数を表示します。 このプログラムでは、現在の従業員数がキーボードから読み取られます。

[!code-csharp[csrefKeywordsModifiers#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#20)]  

## <a name="example---static-initialization"></a>例 - 静的な初期化

この例では、まだ宣言されていない別の `static` フィールドを使用することで `static` フィールドを初期化できます。 `static` フィールドに値を明示的に割り当てるまで、結果は未定義になります。

[!code-csharp[csrefKeywordsModifiers#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#21)]  

## <a name="c-language-specification"></a>C# 言語仕様

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [C# のキーワード](index.md)
- [修飾子](index.md)
- [using static ディレクティブ](using-static.md)
- [静的クラスと静的クラス メンバー](../../programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
