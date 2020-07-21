---
title: << 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.<<
helpviewer_keywords:
- bit shift operators [Visual Basic]
- << operator [Visual Basic]
- operator <<, Visual Basic left shift operator
ms.assetid: fdb93d25-81ba-417f-b808-41207bfb8440
ms.openlocfilehash: 1128b32a739e7dbf3893dcd19b37247cd4643c85
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84370636"
---
# <a name="-operator-visual-basic"></a>\<\< 演算子 (Visual Basic)
ビット パターンに対して算術左シフトを実行します。  
  
## <a name="syntax"></a>構文  
  
```vb  
result = pattern << amount  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 整数数値。 ビット パターンをシフトした結果。 データ型は `pattern` のデータ型と同じです。  
  
 `pattern`  
 必須です。 整数数値式。 シフトするビット パターン。 データ型は、整数型 (`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、または `ULong`) である必要があります。  
  
 `amount`  
 必須です。 数値式。 ビット パターンをシフトするビット数。 データ型は `Integer` であるか、`Integer` に拡大変換する必要があります。  
  
## <a name="remarks"></a>Remarks  
 算術シフトは循環ではありません。つまり、結果の一方の端からシフトされたビットはもう一方の端には再入されません。 算術左シフトでは、結果のデータ型の範囲を超えてシフトされたビットは破棄され、右側に空いたビット位置は 0 に設定されます。  
  
 結果で保持できるよりも多くのビットがシフトされないようにするため、Visual Basic は `pattern` のデータ型に対応するサイズ マスクを使用して `amount` の値をマスクします。 これらの値のバイナリ AND がシフト量に使用されます。 サイズ マスクを次に示します。  
  
|`pattern` のデータ型|サイズ マスク (10 進数)|サイズ マスク (16 進数)|  
|----------------------------|---------------------------|-------------------------------|  
|`SByte`、`Byte`|7|&H00000007|  
|`Short`、`UShort`|15|&H0000000F|  
|`Integer`、`UInteger`|31|&H0000001F|  
|`Long`、`ULong`|63|&H0000003F|  
  
 `amount` が 0 の場合、`result` の値は `pattern` の値と同じになります。 `amount` が負の場合は、符号なしの値として扱われ、適切なサイズ マスクでマスクされます。  
  
 算術シフトではオーバーフロー例外は発生しません。  
  
> [!NOTE]
> `<<` 演算子は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、クラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`<<` 演算子を使用して、整数値に対して算術左シフトを実行しています。 結果のデータ型は、シフトする式のデータ型と常に同じになります。  
  
 [!code-vb[VbVbalrOperators#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#12)]  
  
 前の例の結果は次のようになります。  
  
- `result1` は 192 (0000 0000 1100 0000) です。  
  
- `result2` は 3072 (0000 1100 0000 0000) です。  
  
- `result3` は -32768 (1000 0000 0000 0000) です。  
  
- `result4` は 384 (0000 0001 1000 0000) です。  
  
- `result5` は 0 (左に 15 シフト) です。  
  
 `result4` のシフト量は 17 AND 15 として計算されます。これは 1 と同等です。  
  
## <a name="see-also"></a>関連項目

- [ビット シフト演算子](bit-shift-operators.md)
- [代入演算子](assignment-operators.md)
- [<<= 演算子](left-shift-assignment-operator.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
