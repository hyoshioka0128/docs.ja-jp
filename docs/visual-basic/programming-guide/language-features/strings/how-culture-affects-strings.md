---
title: カルチャが文字列に与える影響
ms.date: 07/20/2015
helpviewer_keywords:
- locale [Visual Basic], effect on strings
- strings [Visual Basic], locale dependence
ms.assetid: c4664444-ee0d-47bf-bef1-eaa3c54bdd7f
ms.openlocfilehash: 9cbd3a5b8685178259b76d97919ea097ae72f6ae
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401967"
---
# <a name="how-culture-affects-strings-in-visual-basic"></a>Visual Basic においてカルチャが文字列に与える影響
このヘルプ ページでは、Visual Basic でカルチャ情報を使用して、文字列の変換と比較を実行する方法について説明します。  
  
## <a name="when-to-use-culture-specific-strings"></a>カルチャ固有の文字列を使用する場合  
 通常、ユーザーに表示し、ユーザーが読み取るすべてのデータにはカルチャ固有の文字列を使用し、アプリケーションの内部データにはカルチャ不変の文字列を使用する必要があります。  
  
 たとえば、アプリケーションが日付を文字列として入力するようユーザーに要求する場合、アプリケーションでは、ユーザーが各自のカルチャに従って文字列を書式設定することを想定し、文字列を適切に変換する必要があります。 アプリケーションがその日付をユーザー インターフェイスに表示する場合は、ユーザーのカルチャで表示する必要があります。  
  
 ただし、アプリケーションが日付を中央サーバーにアップロードする場合は、異なる可能性がある日付形式間での混乱を防ぐために、1 つの特定のカルチャに従って文字列を書式設定する必要があります。  
  
## <a name="culture-sensitive-functions"></a>カルチャに依存する関数  
 Visual Basic のすべての文字列変換関数 (`Str` および `Val` 関数を除く) は、アプリケーションのカルチャ情報を使用して、変換と比較がアプリケーションのユーザーのカルチャに適していることを確認します。  
  
 カルチャ設定が異なるコンピューターで実行されるアプリケーションで文字列変換関数を正しく使用するには、特定のカルチャ設定を使用する関数と、現在のカルチャ設定を使用する関数を理解することが重要です。 既定では、アプリケーションのカルチャ設定は、オペレーティング システムのカルチャ設定から継承されることに注意してください。 詳細については、<xref:Microsoft.VisualBasic.Strings.Asc%2A>、<xref:Microsoft.VisualBasic.Strings.AscW%2A>、<xref:Microsoft.VisualBasic.Strings.Chr%2A>、<xref:Microsoft.VisualBasic.Strings.ChrW%2A>、<xref:Microsoft.VisualBasic.Strings.Format%2A>、<xref:Microsoft.VisualBasic.Conversion.Hex%2A>、<xref:Microsoft.VisualBasic.Conversion.Oct%2A> に関する記事、および「[データ型変換関数](../../../language-reference/functions/type-conversion-functions.md)」をご覧ください。  
  
 `Str` (数値を文字列に変換) および `Val` (文字列を数値に変換) 関数では、文字列と数値間の変換時にアプリケーションのカルチャ情報を使用しません。 代わりに、ピリオド (.) だけを有効な小数点として認識します。 これらの関数の、カルチャに対応する類似関数は次のとおりです。  
  
- **現在のカルチャを使用した変換:** `CStr` および `Format` 関数は数値を文字列に変換し、`CDbl` および `CInt` 関数は文字列を数値に変換します。  
  
- **特定のカルチャを使用した変換:** 各数値オブジェクトには、数値を文字列に変換する `ToString(IFormatProvider)` メソッドと、文字列を数値に変換する `Parse(String, IFormatProvider)` メソッドがあります。 たとえば、`Double` 型では、<xref:System.Double.ToString%28System.IFormatProvider%29> メソッドと <xref:System.Double.Parse%28System.String%2CSystem.IFormatProvider%29> メソッドが提供されます。  
  
 詳細については、次のトピックを参照してください。 <xref:Microsoft.VisualBasic.Conversion.Str%2A> および <xref:Microsoft.VisualBasic.Conversion.Val%2A>  
  
## <a name="using-a-specific-culture"></a>特定のカルチャの使用  
 (文字列として書式設定された) 日付を Web サービスに送信するアプリケーションを開発しているとします。 この場合、アプリケーションでは、文字列変換に特定のカルチャを使用する必要があります。 その理由を説明するために、日付の <xref:System.DateTime.ToString> メソッドを使用した場合の結果を考えてみましょう。アプリケーションでこのメソッドを使用して、日付 July 4, 2005 を書式設定する場合、米国英語 (en-US) カルチャで実行すると、"7/4/2005 12:00:00 AM" が返されますが、ドイツ語 (de-DE) カルチャで実行すると、"04.07.2005 00:00:00" が返されます。  
  
 特定のカルチャの形式で文字列変換を実行する必要がある場合は、.NET Framework に組み込まれている `CultureInfo` クラスを使用します。 カルチャの名前を <xref:System.Globalization.CultureInfo.%23ctor%2A> コンストラクターに渡して、特定のカルチャの新しい `CultureInfo` オブジェクトを作成できます。 サポートされているカルチャ名は、<xref:System.Globalization.CultureInfo> クラスのヘルプ ページに記載されています。  
  
 別の方法として、<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> プロパティから "*インバリアント カルチャ*" のインスタンスを取得することもできます。 インバリアント カルチャは英語カルチャに基づいていますが、違いがいくつかあります。 たとえば、インバリアント カルチャでは、12 時間形式ではなく、24 時間形式が指定されています。  
  
 日付をこのカルチャの文字列に変換するには、<xref:System.Globalization.CultureInfo> オブジェクトを日付オブジェクトの <xref:System.DateTime.ToString%28System.IFormatProvider%29> メソッドに渡します。 たとえば、次のコードでは、アプリケーションのカルチャ設定に関係なく、"07/04/2005 00:00:00" が表示されます。  
  
 [!code-vb[VbVbalrConcepts#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConcepts/VB/Class1.vb#1)]  
  
> [!NOTE]
> 日付リテラルは、常に英語カルチャに従って解釈されます。  
  
## <a name="comparing-strings"></a>文字列の比較  
 文字列の比較が必要になる 2 つの重要な状況があります。  
  
- **ユーザーに表示するためにデータを並べ替える場合:** 文字列が適切に並べ替えられるように、現在のカルチャに基づいた操作を使用します。  
  
- **(通常はセキュリティの目的で) 2 つのアプリケーション内部文字列が完全に一致するかどうかを確認する場合:** 現在のカルチャを無視する操作を使用します。  
  
 どちらの比較も、Visual Basic の <xref:Microsoft.VisualBasic.Strings.StrComp%2A> 関数を使用して実行できます。 比較の型を制御するには、省略可能な `Compare` 引数を指定します。ほとんどの入力と出力には `Text`を指定し、完全一致の確認には `Binary` を指定します。  
  
 `StrComp` 関数は、並べ替え順序に基づいて、比較対象の 2 つの文字列間の関係を示す整数を返します。 結果の正の値は、最初の文字列が 2 番目の文字列より大きいことを示します。 負の結果は最初の文字列の方が小さいことを示し、ゼロは文字列が等しいことを示します。  
  
 [!code-vb[VbVbalrStrings#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class1.vb#22)]  
  
 `StrComp` 関数の .NET Framework パートナーである <xref:System.String.Compare%2A?displayProperty=nameWithType> メソッドを使用することもできます。 これは、基本文字列クラスのオーバーロードされた静的メソッドです。 次の例は、このメソッドの使用方法を示しています。  
  
 [!code-vb[VbVbalrStrings#48](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#48)]  
  
 比較の実行方法をより細かく制御するには、<xref:System.String.Compare%2A> メソッドの追加のオーバーロードを使用できます。 <xref:System.String.Compare%2A?displayProperty=nameWithType> メソッドでは、`comparisonType` 引数を使用して、使用する比較の型を指定できます。  
  
|`comparisonType` 引数の値|比較の型|使用に適した状況|  
|---|---|---|  
|`Ordinal`|文字列のコンポーネント バイトに基づく比較。|大文字と小文字を区別する識別子、セキュリティ関連の設定、またはバイトが完全に一致する必要があるその他の非言語的識別子を比較するときに、この値を使用します。|  
|`OrdinalIgnoreCase`|文字列のコンポーネント バイトに基づく比較。<br /><br /> `OrdinalIgnoreCase` は、インバリアント カルチャ情報を使用して、2 つの文字の違いが大文字/小文字だけかどうかを判断します。|大文字と小文字を区別しない識別子、セキュリティ関連の設定、Windows に格納されているデータを比較するときに、この値を使用します。|  
|`CurrentCulture` または `CurrentCultureIgnoreCase`|現在のカルチャでの文字列の解釈に基づく比較。|ユーザーに表示されるデータ、ほとんどのユーザー入力、言語的解釈が必要なその他のデータを比較するときに、これらの値を使用します。|  
|`InvariantCulture` または `InvariantCultureIgnoreCase`|インバリアント カルチャでの文字列の解釈に基づく比較。<br /><br /> これは、`Ordinal` および `OrdinalIgnoreCase` とは異なります。インバリアント カルチャでは、許容範囲外の文字を同等の不変文字として扱うためです。|永続データを比較するとき、または固定の並べ替え順序が必要な言語関連のデータを表示するときにのみ、これらの値を使用します。|  
  
### <a name="security-considerations"></a>セキュリティの考慮事項  
 アプリケーションが、比較操作または大文字/小文字の変更操作の結果に基づいてセキュリティ上の決定を行う場合は、操作で <xref:System.String.Compare%2A?displayProperty=nameWithType> メソッドを使用し、`comparisonType` 引数に `Ordinal` または `OrdinalIgnoreCase` を渡す必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Globalization.CultureInfo>
- [Visual Basic の文字列の概要](introduction-to-strings.md)
- [データ型変換関数](../../../language-reference/functions/type-conversion-functions.md)
