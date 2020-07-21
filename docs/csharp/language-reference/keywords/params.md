---
title: パラメーター配列の params キーワード - C# リファレンス
ms.date: 07/20/2015
f1_keywords:
- params_CSharpKeyword
- params
helpviewer_keywords:
- parameters [C#], params
- params keyword [C#]
- parameter array
ms.assetid: 1690815e-b52b-4967-8380-5780aff08012
ms.openlocfilehash: 77d7fd19ff57f80f401191027e2fae95026e1966
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81738837"
---
# <a name="params-c-reference"></a>params (C# リファレンス)

`params` キーワードを使用すると、可変数個の引数を受け取る[メソッド パラメーター](method-parameters.md)を指定できます。 パラメーターの型は 1 次元配列でなければなりません。

1 つのメソッド宣言内では、`params` キーワード以後にパラメーターを追加できないため、1 つの `params` キーワードだけを使用できます。

`params` パラメーターの宣言された型が 1 次元配列でない場合は、コンパイラ エラー [CS0225](../../misc/cs0225.md) が発生します。

`params` パラメーターを使用してメソッドを呼び出す場合は、以下を渡すことができます。

- 配列要素の型の引数のコンマ区切りのリスト。
- 指定した型の引数の配列。
- 引数なし。 引数を渡さない場合、`params` リストの長さはゼロになります。

## <a name="example"></a>例

次の例に示すように、さまざまな方法で `params` パラメーターに引数を渡すことができます。

[!code-csharp[csrefKeywordsMethodParams#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsMethodParams/CS/csrefKeywordsMethodParams.cs#5)]

## <a name="c-language-specification"></a>C# 言語仕様

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [C# のキーワード](index.md)
- [メソッド パラメーター](method-parameters.md)
