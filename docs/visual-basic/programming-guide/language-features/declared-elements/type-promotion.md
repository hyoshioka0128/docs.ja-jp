---
title: 型の上位変換
ms.date: 07/20/2015
helpviewer_keywords:
- declared elements [Visual Basic], scope
- visibility [Visual Basic], declared elements
- Partial keyword [Visual Basic], unexpected results with type promotion
- scope [Visual Basic], declared elements
- scope [Visual Basic], Visual Basic
- type promotion
- declared elements [Visual Basic], visibility
ms.assetid: 035eeb15-e4c5-4288-ab3c-6bd5d22f7051
ms.openlocfilehash: 1e284b99a36cdf0f62aee2c45fd9f3bf544d1d81
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410709"
---
# <a name="type-promotion-visual-basic"></a>型の上位変換 (Visual Basic)
モジュールでプログラミング要素を宣言すると、Visual Basic によって、そのスコープがモジュールを含む名前空間に昇格されます。 これは*型の上位変換*と呼ばれます。  
  
 次の例では、モジュールのスケルトン定義とそのモジュールの 2 つのメンバーを示しています。  
  
 [!code-vb[VbVbalrDeclaredElements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#1)]  
  
 `projModule` 内で、モジュール レベルで宣言されたプログラミング要素が `projNamespace` に昇格されます。 前の例では、`basicEnum` と `innerClass` は昇格されますが、`numberSub` は、モジュール レベルで宣言されていないため、昇格されません。  
  
## <a name="effect-of-type-promotion"></a>型の上位変換の効果  
 型の上位変換の効果は、修飾文字列にモジュール名を含める必要がないことです。 次の例では、前の例のプロシージャを 2 回呼び出しています。  
  
 [!code-vb[VbVbalrDeclaredElements#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#2)]  
  
 前の例では、最初の呼び出しで完全修飾文字列を使用しています。 ただし、型の上位変換のため、これは必要ありません。 2 番目の呼び出しでは、修飾文字列に `projModule` を含めずに、モジュールのメンバーにアクセスしています。  
  
## <a name="defeat-of-type-promotion"></a>型の上位変換の無効化  
 名前空間にモジュール メンバーと同じ名前のメンバーが既に存在する場合、そのモジュール メンバーに対して型の上位変換は無効になります。 次の例では、同じ名前空間内の列挙とモジュールのスケルトン定義を示しています。  
  
 [!code-vb[VbVbalrDeclaredElements#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#3)]  
  
 前の例では、名前空間レベルで同じ名前を持つ列挙が既に存在するため、Visual Basic がクラス `abc` を `thisNameSpace` に昇格できません。 `abcSub` にアクセスするには、完全修飾文字列 `thisNamespace.thisModule.abc.abcSub` を使用する必要があります。 ただし、クラス `xyz` は引き続き昇格され、短い修飾文字列 `thisNamespace.xyz.xyzSub` で、`xyzSub` にアクセスできます。  
  
### <a name="defeat-of-type-promotion-for-partial-types"></a>部分型の型の上位変換の無効化  
 モジュール内のクラスまたは構造体で [Partial](../../../language-reference/modifiers/partial.md) キーワードを使用している場合は、名前空間に同じ名前のメンバーが含まれているかどうかに関係なく、そのクラスまたは構造体に対する型の上位変換が自動的に無効になります。 モジュール内の他の要素は、引き続き型の上位変換の対象になります。  
  
 **結果。** 部分定義の型の上位変換の無効化によって、予期しない結果が発生したり、コンパイラ エラーが発生したりすることもあります。 次の例では、クラスのスケルトンの部分定義を示しており、そのうちの 1 つがモジュール内にあります。  
  
 [!code-vb[VbVbalrDeclaredElements#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrDeclaredElements/VB/Class1.vb#4)]  
  
 前の例で、開発者は、コンパイラに `sampleClass` の 2 つの部分定義をマージすることを期待するかもしれません。 しかし、コンパイラでは `sampleModule` 内の部分定義の上位変換が考慮されません。 そのため、どちらも `sampleClass` という名前が付けられていますが、修飾パスが異なる 2 つの個別のクラスのコンパイルが試みられます。  
  
 コンパイラは、完全修飾されたパスがまったく同じ場合にのみ、部分定義をマージします。  
  
## <a name="recommendations"></a>推奨事項  
 次の推奨事項は、優れたプログラミング方法を示しています。  
  
- **一意の名前。** プログラミング要素の名前付けを完全に制御できる場合は、どこでも一意の名前を使用することをお勧めします。 同一の名前は追加の修飾が必要であり、コードが読みにくくなる可能性があります。 それらは、軽度のエラーや予期しない結果につながる可能性もあります。  
  
- **完全修飾。** 同じ名前空間内のモジュールやその他の要素を操作する場合、最も安全な方法は、すべてのプログラミング要素に対して常に完全修飾を使用することです。 モジュール メンバーの型の上位変換が無効になっていて、そのメンバーを完全に修飾していない場合、誤って別のプログラミング要素にアクセスする可能性があります。  
  
## <a name="see-also"></a>関連項目

- [Module ステートメント](../../../language-reference/statements/module-statement.md)
- [Namespace ステートメント](../../../language-reference/statements/namespace-statement.md)
- [Partial](../../../language-reference/modifiers/partial.md)
- [Visual Basic におけるスコープ](scope.md)
- [方法: 変数のスコープを制御する](how-to-control-the-scope-of-a-variable.md)
- [宣言された要素の参照](references-to-declared-elements.md)
