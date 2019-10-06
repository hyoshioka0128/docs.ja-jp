---
title: '>> 演算子 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.>>
helpviewer_keywords:
- operator>>
- '>> operator [Visual Basic]'
- bit shift operators [Visual Basic]
- operator >>
- right shift operators [Visual Basic]
ms.assetid: 054dc6a6-47d9-47ef-82da-cfa2b59fbf8f
ms.openlocfilehash: 337d651e831dc2ab132056f6e9a1f2b5300bf7f8
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701323"
---
# <a name="-operator-visual-basic"></a>> > 演算子 (Visual Basic)
ビットパターンに対して算術右シフトを実行します。  
  
## <a name="syntax"></a>構文  
  
```vb  
result = pattern >> amount  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須。 整数の数値。 ビットパターンをシフトした結果。 データ型は、の`pattern`データ型と同じです。  
  
 `pattern`  
 必須。 整数の数値式。 シフトされるビットパターン。 データ`SByte`型は、整数型 ( `UShort` `Short`、 `Byte`、、 `Integer` `UInteger` `ULong`、、、、または) である必要があります。 `Long`  
  
 `amount`  
 必須。 数値式。 ビットパターンをシフトするビット数。 データ型は、 `Integer`またはに`Integer`拡大変換する必要があります。  
  
## <a name="remarks"></a>コメント  
 算術シフトは循環していません。つまり、結果の一方の端からシフトされたビットはもう一方の端には再入されません。 算術右シフトでは、右端のビット位置を超えてシフトされたビットは破棄され、左端 (符号) ビットは左側に空いているビット位置に反映されます。 これは、`pattern` に負の値がある場合、空いた位置が1に設定されることを意味します。それ以外の場合は0に設定されます。  
  
 @No__t-0、`UShort`、`UInteger`、および `ULong` のデータ型は符号なしであるため、伝達する符号ビットはありません。 @No__t-0 が符号なしの型である場合、空いている位置は常に0に設定されます。  
  
 結果よりも多くのビットがシフトされないようにするため、Visual Basic は `pattern` のデータ型に対応するサイズマスクを使用して `amount` の値をマスクします。 これらの値のバイナリとは、シフトの量に使用されます。 サイズマスクは次のとおりです。  
  
|@No__t のデータ型-0|サイズマスク (10 進数)|サイズマスク (16 進数)|  
|----------------------------|---------------------------|-------------------------------|  
|`SByte`, `Byte`|7|& H00000007|  
|`Short`, `UShort`|15|& H0000000F|  
|`Integer`, `UInteger`|31|& H0000001F|  
|`Long`, `ULong`|63|& H0000003F|  
  
 @No__t-0 が0の場合、`result` の値は `pattern` の値と同じになります。 @No__t-0 が負の場合は、符号なしの値として取得され、適切なサイズマスクでマスクされます。  
  
 算術シフトではオーバーフロー例外は生成されません。  
  
## <a name="overloading"></a>オーバーロード  
 @No__t-0 演算子は*オーバーロード*できます。つまり、クラスまたは構造体がそのクラスまたは構造体の型を持つ場合に、クラスまたは構造体がその動作を再定義できます。 コードでこのようなクラスまたは構造体に対してこの演算子を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`>>` 演算子を使用して、整数値に対して算術右シフトを実行します。 結果は、シフトする式と同じデータ型になります。  
  
 [!code-vb[VbVbalrOperators#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#14)]  
  
 前の例の結果は次のようになります。  
  
- `result1` は 2560 (0000 1010 0000 0000) です。  
  
- `result2` は 160 (0000 0000 1010 0000) です。  
  
- `result3` は 2 (0000 0000 0000 0010) です。  
  
- `result4` は 640 (0000 0010 1000 0000) です。  
  
- `result5` は 0 (右に15桁に移動) です。  
  
 @No__t 0 のシフト量は18と15として計算されます。この値は2になります。  
  
 次の例は、負の値での算術シフトを示しています。  
  
 [!code-vb[VbVbalrOperators#55](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#55)]  
  
 前の例の結果は次のようになります。  
  
- `negresult1` は-512 (1111 1110 0000 0000) です。  
  
- `negresult2` は-1 (符号ビットが伝達されます) です。  
  
## <a name="see-also"></a>関連項目

- [ビット シフト演算子](../../../visual-basic/language-reference/operators/bit-shift-operators.md)
- [代入演算子](../../../visual-basic/language-reference/operators/assignment-operators.md)
- [>>= 演算子](../../../visual-basic/language-reference/operators/right-shift-assignment-operator.md)
- [Visual Basic における演算子の優先順位](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [機能別の演算子一覧](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic の算術演算子](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
