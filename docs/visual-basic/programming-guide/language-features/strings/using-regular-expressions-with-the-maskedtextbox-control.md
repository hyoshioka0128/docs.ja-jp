---
title: MaskedTextBox コントロールによる正規表現を使用する
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], regular expressions
- strings [Visual Basic], masked edit
ms.assetid: 2a048fb0-7053-487d-b2c5-ffa5e22ed6f9
ms.openlocfilehash: efda70be0ccdbc1f4b59d548e50f743f6c493b19
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363715"
---
# <a name="using-regular-expressions-with-the-maskedtextbox-control-in-visual-basic"></a>Visual Basic の MaskedTextBox コントロールによる正規表現を使用する
この例では、単純な正規表現を変換して、<xref:System.Windows.Forms.MaskedTextBox> コントロールで使用する方法を示します。  
  
## <a name="description-of-the-masking-language"></a>マスク言語の説明  
 標準の <xref:System.Windows.Forms.MaskedTextBox> マスク言語は、Visual Basic 6.0 の `Masked Edit` コントロールで使用されているものに基づいているので、そのプラットフォームから移行するユーザーにはよく知られています。  
  
 <xref:System.Windows.Forms.MaskedTextBox> コントロールの <xref:System.Windows.Forms.MaskedTextBox.Mask%2A> プロパティでは、使用する入力マスクを指定します。 マスクは、次の表の 1 つ以上のマスク要素で構成される文字列である必要があります。  
  
|マスク要素|説明|正規表現要素|  
|---------------------|-----------------|--------------------------------|  
|0|0 から 9 までの任意の 1 桁の数字。 必須のエントリ。|\d|  
|9|数字またはスペース。 省略可能なエントリ。|[ \d]?|  
|#|数字またはスペース。 省略可能なエントリ。 マスク内でこの位置を空白のままにすると、スペースとしてレンダリングされます。 プラス (+) 記号とマイナス (-) 記号を使用できます。|[ \d+-]?|  
|L|ASCII 文字。 必須のエントリ。|[a-zA-Z]|  
|?|ASCII 文字。 省略可能なエントリ。|[a-zA-Z]?|  
|&|文字です。 必須のエントリ。|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]|  
|C|文字です。 省略可能なエントリ。|[\p{Ll}\p{Lu}\p{Lt}\p{Lm}\p{Lo}]?|  
|A|英数字。 省略可能なエントリ。|\W|  
|.|カルチャに応じた小数点のプレースホルダー。|使用できません。|  
|,|カルチャに応じた桁区切りのプレースホルダー。|使用できません。|  
|:|カルチャに応じた時刻の区切り文字。|使用できません。|  
|/|カルチャに応じた日付の区切り文字。|使用できません。|  
|$|カルチャに応じた通貨記号。|使用できません。|  
|\<|後続のすべての文字を小文字に変換します。|使用できません。|  
|>|後続のすべての文字を大文字に変換します。|使用できません。|  
|&#124;|以前の上へのシフトまたは下へのシフトを元に戻します。|使用できません。|  
|&#92;|マスク文字をエスケープしてリテラルに変換します。 "\\\\" は、円記号のエスケープ シーケンスです。|&#92;|  
|他のすべての文字。|リテラル。 マスク要素以外のすべての要素は、<xref:System.Windows.Forms.MaskedTextBox> 内にそのまま表示されます。|他のすべての文字。|  
  
 小数点 (.)、桁区切り (,)、時刻 (:)、日付 (/)、通貨 ($) の各記号は、アプリケーションのカルチャで定義されている記号が既定で表示されます。 <xref:System.Windows.Forms.MaskedTextBox.FormatProvider%2A> プロパティを使用すると、別のカルチャの記号を強制的に表示できます。  
  
## <a name="regular-expressions-and-masks"></a>正規表現とマスク  
 正規表現とマスクを使用してユーザー入力を検証できますが、これらは完全に同等であるわけではありません。 正規表現ではマスクよりも複雑なパターンを表現できますが、マスクでは同じ情報をカルチャに関連する形式でより簡潔に表現できます。  
  
 次の表では、4 つの正規表現とそれぞれに対応するマスクを比較しています。  
  
|正規表現|マスク|メモ|  
|------------------------|----------|-----------|  
|`\d{2}/\d{2}/\d{4}`|`00/00/0000`|マスク内の `/` 文字は論理的な日付区切り文字であり、アプリケーションの現在のカルチャに適した日付区切り文字としてユーザーに表示されます。|  
|`\d{2}-[A-Z][a-z]{2}-\d{4}`|`00->L<LL-0000`|米国形式の日付 (日、月の省略形、年)。3 文字の月の省略形は、先頭の大文字の後に 2 つの小文字が続く形で表示されます。|  
|`(\(\d{3}\)-)?\d{3}-d{4}`|`(999)-000-0000`|米国の電話番号。市外局番は省略可能です。 ユーザーは、省略可能な文字を入力しない場合には、スペースを入力するか、マスク内の最初の 0 で表される位置にマウス ポインターを直接置くことができます。|  
|`$\d{6}.00`|`$999,999.00`|0 から 999999 の範囲の通貨値。 通貨、桁区切り、小数点の各文字は、実行時にカルチャ固有の同等の文字に置き換えられます。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.MaskedTextBox.Mask%2A>
- <xref:System.Windows.Forms.MaskedTextBox>
- [Visual Basic における文字列の検証](validating-strings.md)
- [MaskedTextBox コントロール](../../../../framework/winforms/controls/maskedtextbox-control-windows-forms.md)
