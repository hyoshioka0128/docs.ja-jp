---
title: 文字列型 (String)
ms.date: 07/20/2015
f1_keywords:
- vb.String
helpviewer_keywords:
- strings [Visual Basic], character
- strings [Visual Basic], fixed-length
- string keyword [Visual Basic]
- fixed-length strings [Visual Basic], string data type
- literals [Visual Basic], string
- text [Visual Basic], String data type
- $ identifier type character
- String data type
- fixed-length strings
- string literals [Visual Basic]
- data types [Visual Basic], assigning
- String literals [Visual Basic]
- identifier type characters [Visual Basic], $
ms.assetid: 15ac03f5-cabd-42cc-a754-1df3893c25d9
ms.openlocfilehash: cd4b64c101ae56928e84a04649e49c17b6f4023c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415506"
---
# <a name="string-data-type-visual-basic"></a>文字列型 (String) (Visual Basic)

0 から 65535 までの値の範囲の符号なし 16 ビット (2 バイト) のコード ポイントにシーケンスを保持します。 各*コード ポイント* (文字コード) は、1 つの Unicode 文字を表します。 文字列には、0 ～ 約 20 億 (2 ^ 31) の Unicode 文字を含めることができます。  
  
## <a name="remarks"></a>Remarks  

 `String` データ型を使用して、`Char` 要素の配列である `Char()` の配列管理のオーバーヘッドを発生させることなく、複数の文字を保持します。  
  
 `String` の既定値は `Nothing` (null 参照) です。 これは空の文字列 (値 `""`) と同じではありません。  
  
## <a name="unicode-characters"></a>Unicode 文字  

 Unicode の最初の 128 コード ポイント (0 ～ 127) は、標準の米国キーボードの文字と記号に対応しています。 これらの最初の 128 コード ポイントは、ASCII 文字セットで定義されているものと同じです。 2 番目の 128 コード ポイント (128 ～ 255) は、ラテン語に基づくアルファベット文字、アクセント、通貨記号、分数などの特殊文字を表します。 Unicode では、さまざまな記号に残りのコード ポイント (256-65535) を使用します。 これには、世界中のテキスト文字、分音記号、算術記号、および技術用記号が含まれます。  
  
 `String` 変数内の個々の文字に対して <xref:System.Char.IsDigit%2A> や <xref:System.Char.IsPunctuation%2A> などのメソッドを使用して、その Unicode の分類を判断できます。  
  
## <a name="format-requirements"></a>書式の要件  

 `String` リテラルは、引用符 (`" "`) で囲む必要があります。 文字列内の文字のいずれかとして引用符を含める必要がある場合は、2 つの連続する引用符 (`""`) を使用します。 次に例を示します。  
  
```vb  
Dim j As String = "Joe said ""Hello"" to me."  
Dim h As String = "Hello"  
' The following messages all display the same thing:  
' "Joe said "Hello" to me."  
MsgBox(j)  
MsgBox("Joe said " & """" & h & """" & " to me.")  
MsgBox("Joe said """ & h & """ to me.")  
```  
  
 文字列内の引用符を表す連続する引用符は、`String` リテラルを開始および終了する引用符とは独立しています。  
  
## <a name="string-manipulations"></a>文字列の処理  

 文字列を `String` 変数に割り当てた後、その文字列は*不変*になります。つまり、長さや内容を変更できなくなります。 文字列を何らかの方法で変更すると、Visual Basic によって新しい文字列が作成され、前の文字列が破棄されます。 その後、`String` 変数は新しい文字列を指します。  
  
 さまざまな文字列関数を使用することで、`String` 変数の内容を操作できます。 <xref:Microsoft.VisualBasic.Strings.Left%2A> 関数の例を次に示します  
  
```vb  
Dim S As String = "Database"  
' The following statement sets S to a new string containing "Data".  
S = Microsoft.VisualBasic.Left(S, 4)  
```  
  
 別のコンポーネントによって作成された文字列は、先頭または末尾にスペースが埋め込まれている可能性があります。 このような文字列を受け取った場合は、<xref:Microsoft.VisualBasic.Strings.Trim%2A>、<xref:Microsoft.VisualBasic.Strings.LTrim%2A>、および <xref:Microsoft.VisualBasic.Strings.RTrim%2A> の各関数を使用して、これらのスペースを削除できます。  
  
 文字列操作の詳細については、「[文字列](../../programming-guide/language-features/strings/index.md)」を参照してください。  
  
## <a name="programming-tips"></a>プログラミングのヒント  
  
- **負の数値。** `String` によって保持されている文字は符号なしであり、負の値を表すことはできないことに注意してください。 いかなる場合でも、`String` を使用して数値を保持しないでください。  
  
- **相互運用の考慮事項。** オートメーション オブジェクトや COM オブジェクトなど、.NET Framework 用に作成されていないコンポーネントとやり取りする場合、他の環境では文字列の文字のデータ幅 (8 ビット) が異なることに注意してください。 そのようなコンポーネントに 8 ビット文字の文字列引数を渡す場合は、新しい Visual Basic のコードで、`String` ではなく、`Byte` 要素の配列である `Byte()` として宣言します。  
  
- **型文字。** ある識別子に識別子の型文字 `$` を付けると、その識別子は `String` データ型に変換されます。 `String` にはリテラルの型文字は含まれません。 ただし、コンパイラでは、引用符 (`" "`) で囲まれたリテラルは、`String` として処理されます。  
  
- **Framework の型。** .NET Framework において対応する型は、<xref:System.String?displayProperty=nameWithType> クラスです。  
  
## <a name="see-also"></a>関連項目

- <xref:System.String?displayProperty=nameWithType>
- [データの種類](index.md)
- [Char データ型](char-data-type.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [方法: 符号なしの型を使用する Windows の機能を呼び出す](../../programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
