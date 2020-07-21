---
title: '>> 演算子'
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
ms.openlocfilehash: 10b07da22b8b43d6a966fa7c334ac6a0ef4b430d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406367"
---
# <a name="-operator-visual-basic"></a>>> 演算子 (Visual Basic)
ビット パターンに対して算術右シフトを実行します。  
  
## <a name="syntax"></a>構文  
  
```vb  
result = pattern >> amount  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 整数数値。 ビット パターンをシフトした結果。 データ型は `pattern` のデータ型と同じです。  
  
 `pattern`  
 必須です。 整数数値式。 シフトするビット パターン。 データ型は、整数型 (`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、または `ULong`) である必要があります。  
  
 `amount`  
 必須です。 数値式。 ビット パターンをシフトするビット数。 データ型は `Integer` であるか、`Integer` に拡大変換する必要があります。  
  
## <a name="remarks"></a>Remarks  
 算術シフトは循環ではありません。つまり、結果の一方の端からシフトされたビットはもう一方の端に再入されません。 算術右シフトでは、右端のビット位置を超えてシフトされたビットは破棄され、左端 (符号) ビットは左側の空いたビット位置に伝搬されます。 したがって、`pattern` に負の値がある場合、空いている位置は 1 に設定されます。それ以外の場合は 0 に設定されます。  
  
 `Byte`、`UShort`、`UInteger`、および `ULong` データ型は符号なしであるため、伝搬する符号ビットはありません。 `pattern` が符号なしの型の場合、空いている位置は常に 0 に設定されます。  
  
 結果で保持できるよりも多くのビットがシフトされないようにするため、Visual Basic は `pattern` のデータ型に対応するサイズ マスクを使用して `amount` の値をマスクします。 これらの値のバイナリ AND がシフト量に使用されます。 サイズ マスクを次に示します。  
  
|`pattern` のデータ型|サイズ マスク (10 進数)|サイズ マスク (16 進数)|  
|----------------------------|---------------------------|-------------------------------|  
|`SByte`、`Byte`|7|&H00000007|  
|`Short`、`UShort`|15|&H0000000F|  
|`Integer`、`UInteger`|31|&H0000001F|  
|`Long`、`ULong`|63|&H0000003F|  
  
 `amount` が 0 の場合、`result` の値は `pattern` の値と同じになります。 `amount` が負の場合は、符号なしの値として扱われ、適切なサイズ マスクでマスクされます。  
  
 算術シフトではオーバーフロー例外は生成されません。  
  
## <a name="overloading"></a>オーバーロード  
 `>>` 演算子は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、クラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`>>` 演算子を使用して、整数値に対して算術右シフトを実行しています。 結果のデータ型は、シフトする式のデータ型と常に同じになります。  
  
 [!code-vb[VbVbalrOperators#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#14)]  
  
 前の例の結果は次のようになります。  
  
- `result1` は 2560 (0000 1010 0000 0000) です。  
  
- `result2` は 160 (0000 0000 1010 0000) です。  
  
- `result3` は 2 (0000 0000 0000 0010) です。  
  
- `result4` は 640 (0000 0010 1000 0000) です。  
  
- `result5` は 0 (右に 15 桁シフト)。  
  
 `result4` のシフト量は 18 AND 15 として計算されます。これは 2 と同等です。  
  
 次の例は、負の値に対する算術シフトを示しています。  
  
 [!code-vb[VbVbalrOperators#55](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#55)]  
  
 前の例の結果は次のようになります。  
  
- `negresult1` は -512 (1111 1110 0000 0000) です。  
  
- `negresult2` は -1 です (符号ビットが伝播されます)。  
  
## <a name="see-also"></a>関連項目

- [ビット シフト演算子](bit-shift-operators.md)
- [代入演算子](assignment-operators.md)
- [>>= 演算子](right-shift-assignment-operator.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
