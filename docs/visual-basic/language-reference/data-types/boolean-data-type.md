---
title: Boolean データ型
ms.date: 07/20/2015
f1_keywords:
- vb.FALSE
- vb.TRUE
- vb.Boolean
helpviewer_keywords:
- Boolean data type
- Boolean values [Visual Basic], False keyword
- False keyword [Visual Basic]
- True keyword [Visual Basic]
- Boolean values [Visual Basic], True keyword
ms.assetid: 4858e630-4813-4216-a55e-f4d0feb884e4
ms.openlocfilehash: 851c524a83c5f24b77a151634a96798249c5905e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84374422"
---
# <a name="boolean-data-type-visual-basic"></a>ブール型 (Boolean) (Visual Basic)

`True` または `False` のみ可能な値を保持します。 キーワード `True` と `False` は `Boolean` 変数の 2 つの状態に対応しています。  
  
## <a name="remarks"></a>Remarks  

 [ブール データ型 (Visual Basic)](boolean-data-type.md) を使用して、true/false、yes/no、on/off などの 2 つの状態の値を格納します。  
  
 `Boolean` の既定値は `False`です。  
  
 `Boolean` 値は数値として格納されず、格納された値は数値と等価であると見なされません。 `True` と `False` に対して等価の数値に依存するコードを記述することは避けてください。 可能な限り、`Boolean` 変数には、仕様で定められている論理値以外の値を使用しないようにしてください。  
  
## <a name="type-conversions"></a>型変換  

 Visual Basic で数値データ型の値を `Boolean` に変換すると、0 は `False` になり、その他のすべての値は `True` になります。 Visual Basic で `Boolean` 値を数値型に変換すると、`False` は 0 になり、`True` は -1 になります。  
  
 `Boolean` 値と数値データ型の間で変換を行う場合、.NET Framework の変換メソッドでは、必ずしも Visual Basic の変換キーワードと同じ結果が生成されないことに注意してください。 これは、Visual Basic の変換では、以前のバージョンと互換性のある動作が保持されているためです。 詳細については、「[データ型のトラブルシューティング](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)」の「Boolean Type Does Not Convert to Numeric Type Accurately」(ブール型で数値型に正確に変換されない) を参照してください。  
  
## <a name="programming-tips"></a>プログラミングのヒント  
  
- **負の数値。** `Boolean` は数値型ではなく、負の値を表すことはできません。 いかなる場合でも、`Boolean` を使用して数値を保持しないでください。  
  
- **型文字。** `Boolean` には、リテラルの型文字も識別子の型文字も含まれません。  
  
- **Framework の型。** .NET Framework において対応する型は、<xref:System.Boolean?displayProperty=nameWithType> 構造体です。  
  
## <a name="example"></a>例  

 次の例で、`runningVB` は、シンプルな yes/no 設定を格納する `Boolean` 変数です。  
  
```vb  
Dim runningVB As Boolean  
' Check to see if program is running on Visual Basic engine.  
If scriptEngine = "VB" Then  
    runningVB = True  
End If  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Boolean?displayProperty=nameWithType>
- [データの種類](index.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
- [トラブルシューティング (データ型)](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [CType 関数](../functions/ctype-function.md)
