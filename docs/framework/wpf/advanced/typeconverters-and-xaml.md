---
title: TypeConverters および XAML
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [WPF], TypeConverter class
ms.assetid: f6313e4d-e89d-497d-ac87-b43511a1ae4b
ms.openlocfilehash: 94cfce44d5702e0550310723ec56184096165436
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187291"
---
# <a name="typeconverters-and-xaml"></a>TypeConverters および XAML
このトピックでは、XAML の一般的な言語機能としての文字列からの型変換の目的について説明します。 .NET Framework では、<xref:System.ComponentModel.TypeConverter> クラスは、XAML 属性を使用するときにプロパティ値として使用できるマネージド カスタム クラスの実装の一部として、特定の目的を果たします。 カスタム クラスを作成するときに、クラスのインスタンスを XAML で設定可能な属性値として使用できるようにする場合は、クラスに <xref:System.ComponentModel.TypeConverterAttribute> を適用するか、カスタム <xref:System.ComponentModel.TypeConverter> クラスを記述するか、またはその両方を行うことが必要になる場合があります。  

## <a name="type-conversion-concepts"></a>型変換の概念  
  
### <a name="xaml-and-string-values"></a>XAML と文字列値  
 XAML ファイルで属性値を設定する場合、その値の最初の型は純粋なテキストの文字列です。 <xref:System.Double> など、その他のプリミティブも、XAML プロセッサに対して最初はテキスト文字列です。  
  
 XAML プロセッサでは、属性値を処理するために 2 つの情報が必要です。 第 1 の情報は、設定しようとしているプロパティの値の型です。 属性値を定義するすべての文字列は、XAML で処理され、最終的にはその型の値に変換 (解決) される必要があります。 値が、XAML パーサーで認識できるプリミティブ (数値など) である場合は、文字列の直接的な変換が試みられます。 値が列挙型である場合、文字列は、その列挙型の名前付き定数と名前が一致するかどうかを確認するために使用されます。 値がパーサーで認識されるプリミティブでも列挙型でもない場合、問題の型は、変換される文字列に基づく型または値のインスタンスを提供できるものである必要があります。 これを行うには、型コンバーター クラスを指定します。 型コンバーターは、実際には、XAML のシナリオと、場合によっては .NET コードでのコード呼び出しのシナリオの両方で、別のクラスの値を提供するためのヘルパー クラスです。  
  
### <a name="using-existing-type-conversion-behavior-in-xaml"></a>XAML での既存の型変換動作の使用  
 基になる XAML の概念に関する知識によっては、基本的なアプリケーションの XAML で型変換動作を既に意識せず使用している場合があります。 たとえば、WPF では、<xref:System.Windows.Point> 型の値を受け取る文字どおり数百のプロパティが定義されています。 <xref:System.Windows.Point> は、2 次元座標空間内の座標を表す値であり、実際に重要なプロパティは <xref:System.Windows.Point.X%2A> と <xref:System.Windows.Point.Y%2A> の 2 つだけです。 XAML でポイントを指定するときは、<xref:System.Windows.Point.X%2A> と <xref:System.Windows.Point.Y%2A> の値とそれらの間の区切り記号 (通常はコンマ) という文字列として指定します。 たとえば、`<LinearGradientBrush StartPoint="0,0" EndPoint="1,1"/>` のように指定します。  
  
 このような単純型の <xref:System.Windows.Point> と XAML でのその簡単な使用でも、型コンバーターが必要です。 この場合のそれは <xref:System.Windows.PointConverter> クラスです。  
  
 クラス レベルで定義されている <xref:System.Windows.Point> の型コンバーターにより、<xref:System.Windows.Point> を受け取るすべてのプロパティをマークアップで簡単に使用できるようになります。 この場合に型コンバーターがないと、前に示したのと同じ例に対し、次のようなはるかに冗長なマークアップが必要になります。  

```xaml
<LinearGradientBrush>
  <LinearGradientBrush.StartPoint>
    <Point X="0" Y="0"/>
  </LinearGradientBrush.StartPoint>
  <LinearGradientBrush.EndPoint>
    <Point X="1" Y="1"/>
  </LinearGradientBrush.EndPoint>
</LinearGradientBrush>
 ```
  
 型変換文字列を使用するか、より冗長な同等の構文を使用するかは、通常、コーディング スタイルとして選択することです。 XAML ツールのワークフローも、値の設定方法に影響を与える可能性があります。 一部の XAML ツールでは、デザイナー ビューへのラウンドトリップや、独自のシリアル化メカニズムが簡単になるため、最も冗長な形式のマークアップが生成される傾向があります。  
  
 WPF および .NET Framework の型に対する既存の型コンバーターは、通常、<xref:System.ComponentModel.TypeConverterAttribute> が適用されているクラス (またはプロパティ) が存在するかどうかを調べることによって検出できます。 この属性では、XAML や他の目的で、その型の値をサポートする型コンバーターであるクラスに名前が付けられます。  
  
### <a name="type-converters-and-markup-extensions"></a>型コンバーターとマークアップ拡張機能  
 マークアップ拡張機能と型コンバーターは、XAML プロセッサの動作と、それらが適用されるシナリオに関して、果たす役割が異なります。 マークアップ拡張機能の使用時にはコンテキストを利用できますが、マークアップ拡張機能が値を提供するプロパティの型変換動作は一般にマークアップ拡張機能の実装ではチェックされません。 つまり、マークアップ拡張機能で `ProvideValue` の出力としてテキスト文字列が返される場合でも、特定のプロパティまたはプロパティ値型に適用される、その文字列に対する型変換動作は呼び出されません。一般に、マークアップ拡張機能の目的は、型コンバーターを呼び出さずに文字列を処理してオブジェクトを返すことです。  
  
 型コンバーターではなくマークアップ拡張機能が必要になる一般的な状況の 1 つは、既に存在するオブジェクトを参照する場合です。 ステートレスな型コンバーターではせいぜい新しいインスタンスを生成することしかできないため、望ましくありません。 マークアップ拡張機能の詳細については、「[マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)」を参照してください。  
  
### <a name="native-type-converters"></a>ネイティブな型コンバーター  
 XAML パーサーの WPF および .NET Framework による実装では、ネイティブな型変換処理が行われる特定の型がありますが、慣例としてプリミティブと考えられる可能性のある型はありません。 このような型の例として、 <xref:System.DateTime>が挙げられます。 これの理由は、.NET Framework のアーキテクチャがどのように機能するかに基づきます。<xref:System.DateTime> 型は、.NET の最も基本的なライブラリである mscorlib で定義されています。 <xref:System.DateTime> の属性を設定する時は、別のアセンブリから来る属性を使用して従属関係を持ち込むことができません (<xref:System.ComponentModel.TypeConverterAttribute> は System から)。したがって、属性による通常の型コンバーターの検出機構はサポートできません。 代わりに、XAML パーサーでは、ネイティブな処理が必要な型の一覧が保持され、それらの型は通常のプリミティブの処理と類似した方法で処理されます。 (<xref:System.DateTime> の場合、これには <xref:System.DateTime.Parse%2A> の呼び出しが含まれます)。  
  
<a name="Implementing_a_Type_Converter"></a>
## <a name="implementing-a-type-converter"></a>型コンバーターの実装  
  
### <a name="typeconverter"></a>TypeConverter  
 前に示した <xref:System.Windows.Point> の例では、<xref:System.Windows.PointConverter> クラスについて説明しました。 XAML の .NET による実装では、XAML の目的で使用されるすべての型コンバーターは、基底クラス <xref:System.ComponentModel.TypeConverter> から派生したクラスです。 <xref:System.ComponentModel.TypeConverter> クラスは、XAML が登場するより前のバージョンの .NET Framework に存在しました。その本来の用途の 1 つは、ビジュアル デザイナーのプロパティ ダイアログに文字列の変換を提供することでした。 XAML では、<xref:System.ComponentModel.TypeConverter> の役割が拡張され、文字列属性値の解析を有効にし、場合によっては特定のオブジェクト プロパティの実行時の値を属性としてシリアル化するために文字列に戻す処理を可能にする、文字列への変換および文字列からの変換のための基底クラスとして含まれるようになっています。  
  
 <xref:System.ComponentModel.TypeConverter> には、XAML を処理する目的で、文字列への変換と文字列からの変換に関連する次の 4 つのメンバーが定義されています。  
  
- <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>  
  
- <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>  
  
- <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>  
  
- <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>  
  
 それらの中で、最も重要なメソッドは <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> です。 このメソッドでは、入力文字列が必要なオブジェクト型に変換されます。 厳密には、<xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> メソッドを実装して、コンバーターで意図されている変換後の型に、より広範な型を変換することができます。これにより、実行時の変換のサポートなど、XAML の範囲を超えた目的まで拡張できます。XAML の目的は、対象の <xref:System.String> 入力を処理できるコード パスだけです。  
  
 次に重要なメソッドは <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> です。 アプリケーションがマークアップ表現に変換される場合 (たとえば、ファイルとして XAML に保存される場合)、<xref:System.ComponentModel.TypeConverter.ConvertTo%2A> でマークアップ表現を生成する必要があります。 この場合、XAML にとって重要なコード パスは、<xref:System.String> の `destinationType` を渡すときです。  
  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> と <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> は、サービスが <xref:System.ComponentModel.TypeConverter> の実装の機能を照会する時に使用されるサポート メソッドです。 これらのメソッドは、その型について、相当する変換メソッドをコンバーターがサポートしている場合に `true` を返すように実装する必要があります。 XAML の目的では、通常、 <xref:System.String> 型であることを意味します。  
  
### <a name="culture-information-and-type-converters-for-xaml"></a>カルチャ情報と XAML の型コンバーター  

 <xref:System.ComponentModel.TypeConverter> の各実装では、変換に対して有効な文字列の構成内容を独自に解釈でき、パラメーターとして渡される型の説明を使用することも無視することもできます。 カルチャと XAML の型変換に関しては、重要な考慮事項があります。 属性値としてローカライズ可能な文字列を使用することは、XAML で完全にサポートされています。 ただし、そのローカライズ可能な文字列を特定のカルチャの要件で型コンバーターの入力として使用することはサポートされていません。これは、XAML 属性値の型コンバーターには、`en-US` カルチャを使用する固定言語の解析動作が含まれるためです。 この制限に関する設計上の理由の詳細については、XAML 言語の仕様 ([\[MS-XAML\]](https://download.microsoft.com/download/0/A/6/0A6F7755-9AF5-448B-907D-13985ACCF53E/[MS-XAML].pdf)) を参照してください。  
  
 カルチャが問題になる場合がある例として、一部のカルチャでは数値の小数点記号としてコンマが使用されます。 これは、多くの WPF XAML 型コンバーターでのコンマを区切り記号として使用する動作と競合します (一般的な X,Y 形式やコンマ区切りリストなどの歴史的前例に基づきます)。 周囲の XAML でカルチャを渡しても (小数点にコンマを使用するカルチャの例である `sl-SI` を `Language` または `xml:lang` に設定)、問題は解決されません。  
  
### <a name="implementing-convertfrom"></a>ConvertFrom の実装  
 XAML をサポートする <xref:System.ComponentModel.TypeConverter> の実装としてコンバーターを使用できるようにするためには、そのコンバーターの <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> メソッドが `value` パラメーターとして文字列を受け入れる必要があります。 文字列が有効な形式であり、<xref:System.ComponentModel.TypeConverter> の実装で変換できる場合、実装から返されるオブジェクトで、プロパティで想定される型へのキャストがサポートされている必要があります。 それ以外の場合、 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 実装は `null`を返す必要があります。  
  
 <xref:System.ComponentModel.TypeConverter> の各実装では、変換に対して有効な文字列の構成内容を独自に解釈でき、パラメーターとして渡される型の説明またはカルチャのコンテキストを使用することも無視することもできます。 ただし、WPF による XAML の処理では、型の説明のコンテキストに値が渡されない場合があり、`xml:lang` に基づくカルチャが渡されない場合もあります。  
  
> [!NOTE]
> 文字列形式の可能な要素として、中かっこ文字 { を使用しないでください。 これらの文字は、マークアップ拡張シーケンスの開始および終了を示す文字として予約されています。  
  
### <a name="implementing-convertto"></a>ConvertTo の実装  
 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> は、シリアル化のサポートで使用される可能性があります。 カスタム型およびその型コンバーターに対して <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> によるシリアル化をサポートすることは、絶対要件ではありません。 ただし、コントロールを実装する場合、またはクラスの機能または設計の一部としてシリアル化を使用する場合は、 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>を実装する必要があります。  
  
 XAML をサポートする <xref:System.ComponentModel.TypeConverter> の実装として使用できるようにするには、そのコンバーターの <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> メソッドで、サポートされる型 (または値) のインスタンスを `value` パラメーターとして受け入れる必要があります。 `destinationType` パラメーターが <xref:System.String> 型の場合、返されるオブジェクトは <xref:System.String> にキャストできる必要があります。 返される文字列は、 `value`のシリアル化された値を表している必要があります。 理想としては、採用するシリアル化の形式は、その文字列を同じコンバーターの <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> の実装に渡した場合と比べて情報の大きな損失が発生することなく、同じ値を生成できる必要があります。  
  
 値をシリアル化できない場合、またはコンバーターでシリアル化がサポートされていない場合、<xref:System.ComponentModel.TypeConverter.ConvertTo%2A> の実装では、`null` を返す必要があり、その場合は例外をスローすることが許可されます。 ただし、例外をスローする場合は、最初に <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> を確認することによって例外を回避するというベスト プラクティスがサポートされるよう、<xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> の実装の一部として、その変換を使用できないことを通知する必要があります。  
  
 `destinationType` パラメーターが <xref:System.String> 型でない場合は、独自のコンバーター処理を選択できます。 通常は、基底の実装の処理に戻り、基底の <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> で特定の例外を発生させます。  
  
### <a name="implementing-canconvertto"></a>CanConvertTo の実装  
 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> の実装は、 `true` が `destinationType` 型の場合は <xref:System.String>を返し、それ以外の場合は基底の実装に任せる必要があります。  
  
### <a name="implementing-canconvertfrom"></a>CanConvertFrom の実装  
 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> の実装は、 `true` が `sourceType` 型の場合は <xref:System.String>を返し、それ以外の場合は基底の実装に任せる必要があります。  
  
<a name="Applying_the_TypeConverterAttribute"></a>
## <a name="applying-the-typeconverterattribute"></a>TypeConverterAttribute の適用  
 XAML プロセッサでカスタム型コンバーターがカスタム クラス用の型コンバーターとして実際に使用されるようにするには、<xref:System.ComponentModel.TypeConverterAttribute> をクラスの定義に適用する必要があります。 属性を通して指定する <xref:System.ComponentModel.TypeConverterAttribute.ConverterTypeName%2A> は、カスタム型コンバーターの型名である必要があります。 この属性を適用すると、プロパティの型としてカスタム クラスの型が使用されている値を XAML プロセッサが処理するときに、入力文字列を処理して、オブジェクトのインスタンスを返すことができます。  
  
 また、プロパティごとに型コンバーターを提供することもできます。 クラスの定義に <xref:System.ComponentModel.TypeConverterAttribute> を適用する代わりに、プロパティの定義 (メイン定義内の `get`/`set` の実装ではなくメイン定義自体) に適用します。 プロパティの型は、カスタム型コンバーターによって処理される型と一致する必要があります。 この属性を適用すると、プロパティの値を XAML プロセッサが処理する際に、入力文字列を処理して、オブジェクトのインスタンスを返すことができます。 プロパティごとに型コンバーターを提供する手法は、Microsoft .NET Framework や他のライブラリなど、クラス定義を制御することができず、<xref:System.ComponentModel.TypeConverterAttribute> を適用できないライブラリからプロパティの型を使用する場合に特に便利です。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ComponentModel.TypeConverter>
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)
- [XAML 構文の詳細](xaml-syntax-in-detail.md)
