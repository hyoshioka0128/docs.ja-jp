---
title: 部分メソッド
ms.date: 07/20/2015
f1_keywords:
- vb.PartialMethod
- PartialMethod
helpviewer_keywords:
- custom logic into code [Visual Basic]
- partial methods [Visual Basic]
- partial [Visual Basic], methods [Visual Basic]
- methods [Visual Basic], partial methods
- inserting custom logic into code
ms.assetid: 74b3368b-b348-44a0-a326-7d7dc646f4e9
ms.openlocfilehash: 61a1398ba7de8dab005fa1e9efa13dc2ba18cc3c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84364124"
---
# <a name="partial-methods-visual-basic"></a>部分メソッド (Visual Basic)
部分メソッドを使用すると、開発者はカスタム ロジックをコードに挿入できます。 通常、このコードはデザイナーによって生成されるクラスの一部です。 部分メソッドは、コード ジェネレーターによって作成された部分クラスで定義され、何かが変更されたことを通知するためによく使用されます。 部分メソッドにより、開発者は変更に対応するためのカスタム動作を指定できます。  
  
 コード ジェネレーターのデザイナーは、メソッド シグネチャとメソッドの 1 つ以上の呼び出しのみを定義します。 開発者は、生成されたコードの動作をカスタマイズする場合にメソッドの実装を提供できます。 実装が提供されていない場合、メソッドの呼び出しはコンパイラによって削除されるため、パフォーマンスの追加のオーバーヘッドは発生しません。  
  
## <a name="declaration"></a>宣言  
 生成されたコードでは、シグネチャ行の先頭に `Partial` キーワードを配置することによって部分メソッドの定義をマークします。  
  
```vb  
Partial Private Sub QuantityChanged()  
End Sub  
```  
  
 定義は次の条件を満たしている必要があります。  
  
- メソッドは `Function` ではなく、`Sub` である必要があります。  
  
- メソッドの本体は空のままにしておく必要があります。  
  
- アクセス修飾子は `Private` である必要があります。  
  
## <a name="implementation"></a>実装  
 実装は、部分メソッドの本体の入力で主に構成されます。 通常、実装は定義とは別の部分クラスにあり、生成されたコードを拡張する開発者が記述します。  
  
```vb  
Private Sub QuantityChanged()  
'    Code for executing the desired action.  
End Sub  
```  
  
 上記の例では、宣言のシグネチャを正確に複製していますが、バリエーションが可能です。 具体的には、`Overloads` や `Overrides` などの他の修飾子を追加できます。 `Overrides` 修飾子は 1 つだけ許可されます。 メソッド修飾子の詳細については、「[Sub Statement (Sub ステートメント)](../../../language-reference/statements/sub-statement.md)」をご覧ください。  
  
## <a name="use"></a>使用  
 他の `Sub` プロシージャを呼び出す場合と同様に、部分メソッドを呼び出します。 メソッドが実装されている場合、引数が評価され、メソッドの本体が実行されます。 ただし、部分メソッドの実装は省略可能であることに注意してください。 メソッドが実装されていない場合、その呼び出しは無効であり、メソッドに引数として渡された式は評価されません。  
  
## <a name="example"></a>例  
 Product.Designer.vb という名前のファイルで、`Quantity` プロパティを持つ `Product` クラスを定義します。  
  
 [!code-vb[VbVbalrPartialMeths#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrPartialMeths/VB/Class1.vb#4)]  
  
 Product.vb という名前のファイルで、`QuantityChanged` の実装を提供します。  
  
 [!code-vb[VbVbalrPartialMeths#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrPartialMeths/VB/Class1.vb#5)]  
  
 最後に、プロジェクトの Main メソッドで、`Product`インスタンスを宣言し、その `Quantity` プロパティの初期値を指定します。  
  
 [!code-vb[VbVbalrPartialMeths#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrPartialMeths/VB/Class1.vb#6)]  
  
 次のメッセージが示されたメッセージ ボックスが表示されます。  
  
 `Quantity was changed to 100`  
  
## <a name="see-also"></a>関連項目

- [Sub ステートメント](../../../language-reference/statements/sub-statement.md)
- [Sub プロシージャ](./sub-procedures.md)
- [省略可能なパラメーター](./optional-parameters.md)
- [Partial](../../../language-reference/modifiers/partial.md)
- [LINQ to SQL でのコード生成](../../../../framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)
- [部分メソッドによるビジネス ロジックの追加](../../../../framework/data/adonet/sql/linq/adding-business-logic-by-using-partial-methods.md)
