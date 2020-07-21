---
title: IsTrue 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.istrue
helpviewer_keywords:
- IsTrue operator [Visual Basic]
- OrElse operator [Visual Basic]
ms.assetid: b6cec0f2-61b1-4331-a7f0-4d07ee3179d6
ms.openlocfilehash: bc129d3a3aec76285d5ea8fb727fc72c3064c9cf
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84370649"
---
# <a name="istrue-operator-visual-basic"></a>IsTrue 演算子 (Visual Basic)
式が `True` かどうかを判別します。  
  
 コード内で `IsTrue` を明示的に呼び出すことはできませんが、Visual Basic コンパイラはそれを使用して `OrElse` 句からコードを生成できます。 クラスまたは構造体を定義し、その型の変数を `OrElse` 句で使用する場合は、そのクラスまたは構造体で `IsTrue` を定義する必要があります。  
  
 コンパイラは、`IsTrue` と `IsFalse` の演算子を "*対応するペア*" と見なします。 つまり、そのいずれかを定義する場合は、もう一方も定義する必要があります。  
  
## <a name="compiler-use-of-istrue"></a>コンパイラでの IsTrue の使用  
 クラスまたは構造体を定義したら、その型の変数を `For`、`If`、`Else If`、`While` ステートメント、または `When` 句で使用できます。 これを行う場合、条件をテストできるように、型を `Boolean` 値に変換する演算子がコンパイラで必要になります。 適切な演算子が次の順序で検索されます。  
  
1. クラスまたは構造体から `Boolean` への拡大変換演算子。  
  
2. クラスまたは構造体から `Boolean?` への拡大変換演算子。  
  
3. クラスまたは構造体の `IsTrue` 演算子。  
  
4. `Boolean` から `Boolean?` への変換を含まない `Boolean?` への縮小変換。  
  
5. クラスまたは構造体から `Boolean` への縮小変換演算子。  
  
 `Boolean` または `IsTrue` 演算子への変換を定義していない場合、コンパイラはエラーを通知します。  
  
> [!NOTE]
> `IsTrue` 演算子は "*オーバーロード*" できます。つまり、オペランドがあるクラスまたは構造体の型を持っているときに、そのクラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を必ず理解してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例では、`IsFalse` および `IsTrue` 演算子の定義を含む構造体のアウトラインを定義しています。  
  
 [!code-vb[VbVbalrOperators#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#28)]  
  
## <a name="see-also"></a>関連項目

- [IsFalse 演算子](isfalse-operator.md)
- [方法: 演算子を定義する](../../programming-guide/language-features/procedures/how-to-define-an-operator.md)
- [OrElse 演算子](orelse-operator.md)
