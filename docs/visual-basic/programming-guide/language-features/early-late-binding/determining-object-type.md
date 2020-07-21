---
title: オブジェクトの型の決定
ms.date: 07/20/2015
helpviewer_keywords:
- classes [Visual Basic], discovering which an object belongs to
- types [Visual Basic], determining Visual Basic object types
- object variables [Visual Basic], testing values
- TypeOf...Is expression, object type at run time
- TypeName function
- objects [Visual Basic], type determining
ms.assetid: d95e7ad1-cd63-41d6-9a28-d7a1380d49c1
ms.openlocfilehash: 3b1c4ad0ab4fd8d2897aff6ad9097cdc81272455
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410645"
---
# <a name="determining-object-type-visual-basic"></a>オブジェクトの型の決定 (Visual Basic)
汎用オブジェクト変数 (`Object` として宣言する変数) では、あらゆるクラスのオブジェクトを保持できます。 `Object` 型の変数を使用する場合、オブジェクトのクラスによって異なるアクションを実行しなければならないことがあります。たとえば、オブジェクトによっては、特定のプロパティやメソッドがサポートされません。 Visual Basic では、`TypeName` 関数と `TypeOf...Is` 演算子という 2 つの方法によって、オブジェクト変数に格納されているオブジェクトの型を特定できます。  
  
## <a name="typename-and-typeofis"></a>TypeName と TypeOf…Is  
 `TypeName` 関数の戻り値は文字列であり、次のコードで示すように、オブジェクトのクラス名を格納または表示する必要がある場合に最適です。  
  
 [!code-vb[VbVbalrOOP#92](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#92)]  
  
 `TypeOf...Is` 演算子は、`TypeName` を使用した同等の文字列比較よりもはるかに高速であるため、オブジェクトの型のテストに最も適しています。 次のコードでは、`If...Then...Else` ステートメント内で `TypeOf...Is` を使用しています。  
  
 [!code-vb[VbVbalrOOP#93](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#93)]  
  
 ここで注意が必要です。 オブジェクトが特定の型であるか、または特定の型から派生している場合、`TypeOf...Is` 演算子は `True` を返します。 Visual Basic で行うほとんどすべての操作にはオブジェクトが関係しています。これには、文字列や整数など、オブジェクトとは通常見なされない要素も含まれます。 こうしたオブジェクトは、<xref:System.Object> から派生し、そのメソッドを継承しています。 `TypeOf...Is` 演算子に `Integer` を渡して、`Object` かどうかを評価した場合、`True` が返されます。 次の例では、パラメーター `InParam` は `Object` であり、かつ `Integer` でもあると返されます。  
  
 [!code-vb[VbVbalrOOP#94](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#94)]  
  
 次の例では、`TypeOf...Is` と `TypeName` の両方を使用して、`Ctrl` 引数から渡されたオブジェクトの型を特定します。 `TestObject` プロシージャにより、3 種類のコントロールを使用して `ShowType` を呼び出しています。  
  
#### <a name="to-run-the-example"></a>例を実行するには  
  
1. 新しい Windows アプリケーション プロジェクトを作成して、フォームに <xref:System.Windows.Forms.Button> コントロール、<xref:System.Windows.Forms.CheckBox> コントロール、および <xref:System.Windows.Forms.RadioButton> コントロールを追加します。  
  
2. フォームのボタンで `TestObject` プロシージャを呼び出します。  
  
3. 次のコードをフォームに追加します。  
  
     [!code-vb[VbVbalrOOP#95](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOOP/VB/OOP.vb#95)]  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Information.TypeName%2A>
- [文字列名によるプロパティまたはメソッドの呼び出し](calling-a-property-or-method-using-a-string-name.md)
- [Object 型](../../../language-reference/data-types/object-data-type.md)
- [If...Then...Else ステートメント](../../../language-reference/statements/if-then-else-statement.md)
- [String データ型](../../../language-reference/data-types/string-data-type.md)
- [Integer データ型](../../../language-reference/data-types/integer-data-type.md)
