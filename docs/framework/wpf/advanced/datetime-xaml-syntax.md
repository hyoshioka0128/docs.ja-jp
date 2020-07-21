---
title: DateTime XAML 構文
ms.date: 03/30/2017
helpviewer_keywords:
- DateTime XAML syntax [WPF], strings for
- DateTime XAML syntax [WPF], where used
- short date format [WPF], DateTime
- DateTime XAML syntax [WPF]
- DateTime XAML text [WPF]
- DateTime XAML syntax [WPF], format strings for
ms.assetid: 5901710a-609b-40c8-9d65-f0016cd9090b
ms.openlocfilehash: 57b73d3b80f0392b99aacfbfac4d8709f72d52e9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186327"
---
# <a name="datetime-xaml-syntax"></a>DateTime XAML 構文
<xref:System.Windows.Controls.Calendar> や <xref:System.Windows.Controls.DatePicker> などの一部のコントロールには、<xref:System.DateTime> 型を使用するプロパティが存在します。 これらのコントロールに対する日付または時刻の初期値は、分離コードで実行時に指定するのが一般的です。ただし、日付または時刻の初期値を XAML で指定することもできます。 WPF XAML パーサーでは、組み込みの XAML テキスト構文を使用して、<xref:System.DateTime> の値が解析されます。 このトピックでは、<xref:System.DateTime> の XAML テキスト構文の詳細について説明します。  

<a name="where_datetime_xaml_syntax_is_used"></a>
## <a name="when-to-use-datetime-xaml-syntax"></a>DateTime XAML 構文が使用される状況  
 日付は必ずしも XAML で設定する必要はありません。また、XAML で設定することが適切とは言えない場合もあります。 たとえば、<xref:System.DateTime.Now%2A?displayProperty=nameWithType> プロパティを使用すると、実行時に日付を初期化できます。また、カレンダーに対する日付の調整も、ユーザーの入力に基づいてコードビハインドですべて行うことができます。 ただし、コントロール テンプレートの <xref:System.Windows.Controls.Calendar> や <xref:System.Windows.Controls.DatePicker> に日付をハードコーディングすることが必要になる場合もあります。 このようなシナリオでは、<xref:System.DateTime> XAML 構文を使用する必要があります。  
  
### <a name="datetime-xaml-syntax-is-a-native-behavior"></a>DateTime XAML 構文はネイティブの動作  
 <xref:System.DateTime> は、CLR の基底クラス ライブラリで定義されているクラスです。 基底クラス ライブラリと CLR の他のライブラリとの関連性のため、<xref:System.ComponentModel.TypeConverterAttribute> をクラスに適用し、型コンバーターを使用して XAML 文字列を処理し、ランタイム オブジェクト モデルの <xref:System.DateTime> に変換することはできません。 変換動作を提供する `DateTimeConverter` クラスは存在しません。このトピックで説明する変換動作は、WPF XAML パーサーのネイティブな動作です。  
  
<a name="format_strings_for_datetime_xaml_syntax"></a>
## <a name="format-strings-for-datetime-xaml-syntax"></a>DateTime XAML 構文の書式指定文字列  
 <xref:System.DateTime> の形式は、書式指定文字列で指定できます。 書式指定文字列は、値を作成するときに使用できるテキスト構文を形式化します。 既存の WPF コントロールの <xref:System.DateTime> 値では、一般に、<xref:System.DateTime> の日付要素のみが使用され、時刻要素は使用されません。  
  
 <xref:System.DateTime> を XAML で指定する場合、どの書式指定文字列でも代用できます。  
  
 また、このトピックで特に示されていない形式および書式指定文字列も使用できます。 技術的には、<xref:System.DateTime> 値を XAML で指定すると、WPF XAML パーサーによって解析されるときに、<xref:System.DateTime.Parse%2A?displayProperty=nameWithType> が内部的に呼び出されます。したがって、XAML の入力では、<xref:System.DateTime.Parse%2A?displayProperty=nameWithType> によって受け付けられる任意の文字列を使用できます。 詳細については、「<xref:System.DateTime.Parse%2A?displayProperty=nameWithType>」を参照してください。  
  
> [!IMPORTANT]
> DateTime XAML 構文でネイティブ変換を行う場合は常に、<xref:System.Globalization.CultureInfo> として `en-us` を使用します。 これは、XAML 内の <xref:System.Windows.FrameworkElement.Language%2A> 値または `xml:lang` 値による影響を受けません。XAML の属性レベルでの型変換は、コンテキストなしで動作するためです。 日や月を表示する順序などにはカルチャによる違いがあるため、ここで示した書式指定文字列は補完しないでください。 ここで示した書式指定文字列は、その他のカルチャ設定に関係なく、XAML を解析する場合に適しています。  
  
 以降のセクションでは、<xref:System.DateTime> の一般的な書式指定文字列について説明します。  
  
### <a name="short-date-pattern-d"></a>短い形式の日付パターン ("d")  
 XAML における <xref:System.DateTime> の短い日付形式は次のとおりです。  
  
 `M/d/YYYY`  
  
 これは、WPF コントロールでの一般的な使用法で、必要なすべての情報を指定するための最も簡単な形式です。タイム ゾーン オフセットと時刻要素を誤って指定した場合でも影響を受けないため、他の形式ではなく、この形式の使用をお勧めします。  
  
 たとえば、2010 年 6 月 1 日を指定するには、次の文字列を使用します。  
  
 `3/1/2010`  
  
 詳細については、「<xref:System.Globalization.DateTimeFormatInfo.ShortDatePattern%2A?displayProperty=nameWithType>」を参照してください。  
  
### <a name="sortable-datetime-pattern-s"></a>並べ替えできる DateTime のパターン ("s")  
 XAML における並べ替え可能な <xref:System.DateTime> のパターンを次に示します。  
  
 `yyyy'-'MM'-'dd'T'HH':'mm':'ss`  
  
 たとえば、2010 年 6 月 1 日を指定するには、次の文字列を使用します (時刻要素はすべて 0 として入力されます)。  
  
 `2010-06-01T000:00:00`  
  
### <a name="rfc1123-pattern-r"></a>RFC1123 パターン ("r")  
 RFC1123 パターンの利点は、カルチャに依存しないために、RFC1123 パターンが使用されている他の日付ジェネレーターから入力された文字列を使用できることです。 XAML における RFC1123 の <xref:System.DateTime> パターンを次に示します。  
  
 `ddd, dd MMM yyyy HH':'mm':'ss 'UTC'`  
  
 たとえば、2010 年 6 月 1 日を指定するには、次の文字列を使用します (時刻要素はすべて 0 として入力されます)。  
  
 `Mon, 01 Jun 2010 00:00:00 UTC`  
  
### <a name="other-formats-and-patterns"></a>その他の形式とパターン  
 既に説明したように、XAML における <xref:System.DateTime> では、<xref:System.DateTime.Parse%2A?displayProperty=nameWithType> に対する入力として受け付けられる任意の文字列を指定できます。 これには、その他の形式化された形式 (例: <xref:System.Globalization.DateTimeFormatInfo.UniversalSortableDateTimePattern%2A>) および特定の <xref:System.Globalization.DateTimeFormatInfo> フォームとして形式化されていない形式が含まれます。 たとえば、`YYYY/mm/dd` という形式は、<xref:System.DateTime.Parse%2A?displayProperty=nameWithType> に対する入力として受け付けられます。 このトピックでは、使用可能な形式の一部を説明します。標準的な使用手順としては、短い形式の日付パターンをお勧めします。  
  
## <a name="see-also"></a>関連項目

- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
