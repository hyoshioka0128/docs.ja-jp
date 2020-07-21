---
title: 文字列とその他の型との変換
ms.date: 07/20/2015
helpviewer_keywords:
- data type conversion [Visual Basic], string
- conversions [Visual Basic], type
- string conversion [Visual Basic]
- conversions [Visual Basic], data type
- type conversion [Visual Basic], string
- regional options
ms.assetid: c3a99596-f09a-44a5-81dd-1b89a094f1df
ms.openlocfilehash: ae8f7c2159191536013fafd8bfd10fb9a93fb785
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84394222"
---
# <a name="conversions-between-strings-and-other-types-visual-basic"></a>文字列とその他の型との変換 (Visual Basic)
数値、`Boolean`、または日付/時刻値を `String` に変換できます。 文字列の内容が変換先データ型の有効な値と解釈される場合は、逆方向 (文字列値を数値、`Boolean`、または `Date`) に変換することもできます。 そうでない場合は、実行時エラーが発生します。  
  
 これらのすべての代入での変換は、どちらの方向でも縮小変換です。 型変換キーワード (`CBool`、`CByte`、`CDate`、`CDbl`、`CDec`、`CInt`、`CLng`、`CSByte`、`CShort`、`CSng`、`CStr`、`CUInt`、`CULng`、`CUShort`、および `CType`) を使用する必要があります。 <xref:Microsoft.VisualBasic.Strings.Format%2A> 関数や <xref:Microsoft.VisualBasic.Conversion.Val%2A> 関数を使用すると、文字列と数値の間の変換をさらに制御できます。  
  
 クラスまたは構造体を定義している場合は、`String` とクラスまたは構造体の型との間に型変換演算子を定義できます。 詳細については、「[方法:変換演算子を定義する](../procedures/how-to-define-a-conversion-operator.md)」を参照してください。  
  
## <a name="conversion-of-numbers-to-strings"></a>数値から文字列への変換  
 `Format` 関数を使用して、数値を書式設定された文字列に変換できます。これは、該当する数字だけでなく、通貨記号 (`$` など)、3 桁ごとの区切りつまり "*桁区切り記号*" (`,` など)、小数点 (`.` など) のような書式設定記号を含むことができます。 `Format` は、Windows の **[コントロール パネル]** に指定された **[地域のオプション]** 設定に従って適切な記号を自動的に使用します。  
  
 次の例のように、連結 (`&`) 演算子を使用して、数値を文字列に暗黙に変換できることに注意してください。  
  
```vb  
' The following statement converts count to a String value.  
Str = "The total count is " & count  
```  
  
## <a name="conversion-of-strings-to-numbers"></a>文字列から数値への変換  
 `Val` 関数を使用すると、明示的に文字列の数字を数値に変換できます。 `Val` は、数字、スペース、タブ、改行、またはピリオド以外の文字が見つかるまで文字列を読み取ります。 シーケンス "&O" と "&H" によって記数法の基数が変更され、これでスキャンが終了します。 読み取りを終了するまで、`Val` は該当するすべての文字を数値に変換します。 たとえば、次のステートメントでは値 `141.825` が返されます。  
  
 `Val("   14   1.825 miles")`  
  
 Visual Basic が文字列を数値に変換するとき、Windows の **[コントロール パネル]** の **[地域のオプション]** 設定を使用して、桁区切り記号、小数点、および通貨記号を解釈します。 つまり、変換は 1 つの設定では成功しますが、別の設定では成功しない可能性があります。 たとえば、`"$14.20"` は英語 (米国) のロケールでは許容されますが、フランス語のロケールでは許容されません。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における型変換](type-conversions.md)
- [拡大変換と縮小変換](widening-and-narrowing-conversions.md)
- [暗黙の型変換と明示的な型変換](implicit-and-explicit-conversions.md)
- [方法: Visual Basic でオブジェクトを別の型に変換する](how-to-convert-an-object-to-another-type.md)
- [配列変換](array-conversions.md)
- [データの種類](../../../language-reference/data-types/index.md)
- [データ型変換関数](../../../language-reference/functions/type-conversion-functions.md)
- [グローバル化およびローカライズされたアプリの開発](/visualstudio/ide/globalizing-and-localizing-applications)
