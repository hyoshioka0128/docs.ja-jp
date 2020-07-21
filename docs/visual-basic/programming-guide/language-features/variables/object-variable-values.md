---
title: オブジェクト変数の値
ms.date: 07/20/2015
helpviewer_keywords:
- object variables [Visual Basic], values
- values [Visual Basic], of object variables
- data types [Visual Basic], object variable
- variables [Visual Basic], object
ms.assetid: 31555704-58a3-49f1-9a0a-6421f605664f
ms.openlocfilehash: 1dd3e8cd68086fe116daf0678a1a19881f1ae9c3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410349"
---
# <a name="object-variable-values-visual-basic"></a>オブジェクト変数の値 (Visual Basic)
[Object データ型](../../../language-reference/data-types/object-data-type.md)の変数は、任意の型のデータを参照できます。 `Object` 変数に格納した値はメモリ内のどこかに保持されますが、変数自体にはデータへのポインターが保持されます。  
  
## <a name="object-classifier-functions"></a>オブジェクト分類子関数  
 Visual Basic には、次の表に示すように、`Object` 変数の参照先に関する情報を返す関数が用意されています。  
  
|関数|オブジェクト変数が参照している場合に True を返す|  
|--------------|---------------------------------------------------|  
|<xref:Microsoft.VisualBasic.Information.IsArray%2A>|単一の値ではなく、値の配列|  
|<xref:Microsoft.VisualBasic.Information.IsDate%2A>|[Date データ型](../../../language-reference/data-types/date-data-type.md)値、または日付と時刻の値として解釈できる文字列|  
|<xref:Microsoft.VisualBasic.Information.IsDBNull%2A>|欠落しているデータまたは存在しないデータを表す <xref:System.DBNull> 型のオブジェクト|  
|<xref:Microsoft.VisualBasic.Information.IsError%2A>|<xref:System.Exception> から派生する例外オブジェクト|  
|<xref:Microsoft.VisualBasic.Information.IsNothing%2A>|[Nothing](../../../language-reference/nothing.md)、つまり、現在、変数に割り当てられているオブジェクトがない|  
|<xref:Microsoft.VisualBasic.Information.IsNumeric%2A>|数値、または数値として解釈できる文字列|  
|<xref:Microsoft.VisualBasic.Information.IsReference%2A>|参照型 (文字列、配列、デリゲート、またはクラス型など)|  
  
 これらの関数を使用すると、操作やプロシージャに無効な値が送信されるのを回避できます。  
  
## <a name="typeof-operator"></a>TypeOf 演算子  
 また、[TypeOf 演算子](../../../language-reference/operators/typeof-operator.md)を使用すると、オブジェクト変数が現在、特定のデータ型を参照しているかどうかを判断することもできます。 オペランドのランタイム型が指定された型から派生しているか、または指定された型を実装している場合、`TypeOf`...`Is` 式の結果は `True` になります。  
  
 次の例では、値型と参照型を参照するオブジェクト変数に対して `TypeOf` を使用しています。  
  
```vb  
' The following statement puts a value type (Integer) in an Object variable.  
Dim num As Object = 10  
' The following statement puts a reference type (Form) in an Object variable.  
Dim frm As Object = New Form()  
If TypeOf num Is Long Then Debug.WriteLine("num is Long")  
If TypeOf num Is Integer Then Debug.WriteLine("num is Integer")  
If TypeOf num Is Short Then Debug.WriteLine("num is Short")  
If TypeOf num Is Object Then Debug.WriteLine("num is Object")  
If TypeOf frm Is Form Then Debug.WriteLine("frm is Form")  
If TypeOf frm Is Label Then Debug.WriteLine("frm is Label")  
If TypeOf frm Is Object Then Debug.WriteLine("frm is Object")  
```  
  
 上記の例では、次の行が **[デバッグ]** ウィンドウに書き込まれます。  
  
 `num is Integer`  
  
 `num is Object`  
  
 `frm is Form`  
  
 `frm is Object`  
  
 オブジェクト変数 `num` は `Integer` 型のデータを参照し、`frm` はクラス <xref:System.Windows.Forms.Form> のオブジェクトを参照します。  
  
## <a name="object-arrays"></a>オブジェクトの配列  
 `Object` 変数の配列を宣言して使用することができます。 これは、さまざまなデータ型とオブジェクト クラスを処理する必要がある場合に便利です。 配列内のすべての要素が、宣言されたデータ型と同じである必要があります。 このデータ型を `Object` として宣言すると、オブジェクトとクラス インスタンスを配列内の他のデータ型と共に格納できます。  
  
## <a name="see-also"></a>関連項目

- [オブジェクト変数](object-variables.md)
- [オブジェクト変数の宣言](object-variable-declaration.md)
- [オブジェクト変数の代入](object-variable-assignment.md)
- [方法: オブジェクトの現在のインスタンスを参照する](how-to-refer-to-the-current-instance-of-an-object.md)
- [方法: オブジェクト変数で参照している型を確認する](how-to-determine-what-type-an-object-variable-refers-to.md)
- [方法: 2 つのオブジェクトが関連しているかどうかを判別する](how-to-determine-whether-two-objects-are-related.md)
- [方法: 2 つのオブジェクトが同一であるかどうかを判別する](how-to-determine-whether-two-objects-are-identical.md)
- [データの種類](../data-types/index.md)
