---
title: 文字列型 (String) (Visual Basic)
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
ms.openlocfilehash: 6d2fd226735622de5cd7197060c05b8ac12b69f1
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71696839"
---
# <a name="string-data-type-visual-basic"></a>文字列型 (String) (Visual Basic)
0 ~ 65535 の範囲の値を範囲とする符号なし16ビット (2 バイト) コードポイントのシーケンスを保持します。 各*コードポイント*(文字コード) は、1つの Unicode 文字を表します。 文字列には、0 ~ 約 20億 (2 ^ 31) の Unicode 文字を含めることができます。  
  
## <a name="remarks"></a>コメント  
 @No__t 0 のデータ型を使用して、`Char` 要素の配列である `Char()` の配列管理オーバーヘッドを発生させずに、複数の文字を保持します。  
  
 @No__t-0 の既定値は `Nothing` (null 参照) です。 これは空の文字列 (値 `""`) と同じではないことに注意してください。  
  
## <a name="unicode-characters"></a>Unicode 文字  
 Unicode の最初の128コードポイント (0 ~ 127) は、標準の U.S. キーボードの文字と記号に対応しています。 これらの最初の128コードポイントは、ASCII 文字セットで定義されているものと同じです。 2番目の128コードポイント (128 ~ 255) は、ラテン語に基づくアルファベット文字、アクセント、通貨記号、分数などの特殊文字を表します。 Unicode では、さまざまなシンボルについて、残りのコードポイント (256-65535) を使用します。 これには、世界中のテキスト文字、分音記号、数学、およびテクニカルシンボルが含まれます。  
  
 @No__t-2 変数の個々の文字に <xref:System.Char.IsDigit%2A> や <xref:System.Char.IsPunctuation%2A> などのメソッドを使用して、Unicode 分類を決定することができます。  
  
## <a name="format-requirements"></a>書式の要件  
 @No__t-0 リテラルは引用符で囲む必要があります (`" "`)。 文字列内のいずれかの文字として引用符を含める必要がある場合は、2つの連続する引用符 (`""`) を使用します。 次に例を示します。  
  
```vb  
Dim j As String = "Joe said ""Hello"" to me."  
Dim h As String = "Hello"  
' The following messages all display the same thing:  
' "Joe said "Hello" to me."  
MsgBox(j)  
MsgBox("Joe said " & """" & h & """" & " to me.")  
MsgBox("Joe said """ & h & """ to me.")  
```  
  
 文字列内の引用符を表す連続した引用符は、@no__t 0 リテラルを開始および終了する引用符とは関係がないことに注意してください。  
  
## <a name="string-manipulations"></a>文字列操作  
 @No__t 0 の変数に文字列を割り当てると、その文字列は*不変*になります。つまり、長さや内容を変更することはできません。 文字列を任意の方法で変更すると、Visual Basic によって新しい文字列が作成され、前の文字列が破棄されます。 @No__t 0 の変数は、新しい文字列を指します。  
  
 @No__t 0 変数の内容を操作するには、さまざまな文字列関数を使用します。 次の例は、<xref:Microsoft.VisualBasic.Strings.Left%2A> 関数を示しています。  
  
```vb  
Dim S As String = "Database"  
' The following statement sets S to a new string containing "Data".  
S = Microsoft.VisualBasic.Left(S, 4)  
```  
  
 別のコンポーネントによって作成された文字列は、先頭または末尾にスペースが埋め込まれている可能性があります。 このような文字列を受け取った場合は、<xref:Microsoft.VisualBasic.Strings.Trim%2A>、<xref:Microsoft.VisualBasic.Strings.LTrim%2A>、<xref:Microsoft.VisualBasic.Strings.RTrim%2A> の各関数を使用して、これらのスペースを削除できます。  
  
 文字列操作の詳細については、「[文字列](../../../visual-basic/programming-guide/language-features/strings/index.md)」を参照してください。  
  
## <a name="programming-tips"></a>プログラミングのヒント  
  
- **負の数値。** @No__t-0 によって保持されている文字は符号なしであり、負の値を表すことはできないことに注意してください。 どのような場合でも、`String` を使用して数値を保持することはできません。  
  
- **相互運用に関する考慮事項。** .NET Framework 用に作成されていないコンポーネント (たとえば、オートメーションや COM オブジェクト) とやり取りする場合は、他の環境で文字列文字のデータ幅が異なる (8 ビット) ことに注意してください。 8ビット文字の文字列引数をこのようなコンポーネントに渡す場合は、新しい Visual Basic コードで `String` ではなく、`Byte` 要素の配列 @no__t 0 として宣言します。  
  
- **文字を入力します。** 識別子の型文字 `$` を任意の識別子に追加すると、強制的に `String` のデータ型になります。 `String` にはリテラルの型文字がありません。 ただし、コンパイラは、引用符で囲まれたリテラル (`" "`) を `String` として扱います。  
  
- **フレームワークの種類。** .NET Framework 内の対応する型は、@no__t 0 のクラスです。  
  
## <a name="see-also"></a>関連項目

- <xref:System.String?displayProperty=nameWithType>
- [データの種類](../../../visual-basic/language-reference/data-types/index.md)
- [Char データ型](../../../visual-basic/language-reference/data-types/char-data-type.md)
- [データ型変換関数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)
- [変換の概要](../../../visual-basic/language-reference/keywords/conversion-summary.md)
- [2 つのオブジェクトが等しいかどうかをテストする方法符号なしの型を使用する Windows の機能を呼び出す](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)
- [データ型の有効な使用方法](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
