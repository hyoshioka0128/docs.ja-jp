---
title: XAML の型コンバーターの概要
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], type converters
- XAML [XAML Services], TypeConverter
- type conversion for XAML [XAML Services]
ms.assetid: 51a65860-efcb-4fe0-95a0-1c679cde66b7
ms.openlocfilehash: c3c69aebacd140a14e74545d601c0207cb8de681
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432870"
---
# <a name="overview-of-type-converters-for-xaml"></a>XAML 用の型コンバーターの概要

型コンバーターは、XAML マークアップの文字列をオブジェクト グラフの特定のオブジェクトに変換するオブジェクト ライターのロジックを提供します。 NET XAML サービスでは、型コンバーターは<xref:System.ComponentModel.TypeConverter>から派生するクラスである必要があります。 一部のコンバーターは XAML 保存パスもサポートしており、オブジェクトをシリアル化マークアップの文字列形式にシリアル化するために使用されます。 このトピックでは、XAML の型コンバーターがいつ、どのように起動されるかについて説明し、 <xref:System.ComponentModel.TypeConverter>のメソッドのオーバーライドの実装についてアドバイスします。

## <a name="type-conversion-concepts"></a>型変換の概念

次のセクションでは、XAML で文字列を使用する方法と、.NET XAML サービスのオブジェクト ライターが型コンバーターを使用して、XAML ソースで検出される文字列値の一部を処理する方法についての基本的な概念について説明します。

### <a name="xaml-and-string-values"></a>XAML と文字列値

XAML ファイルで属性値を設定する場合、その値の最初の型は一般的な意味での文字列であり、XML の意味としては文字列の属性値です。 <xref:System.Double> など、その他のプリミティブも、XAML プロセッサに対して最初は文字列です。

ほとんどの場合、XAML プロセッサは、属性値を処理するために 2 つの情報を必要とします。 第 1 の情報は、設定しようとしているプロパティの値の型です。 属性値を定義するすべての文字列は、XAML で処理され、最終的にはその型の値に変換 (解決) される必要があります。 値が、XAML パーサーで認識できるプリミティブ (数値など) である場合は、文字列の直接的な変換が試みられます。 属性の値が列挙体を参照している場合は、指定された文字列がその列挙体の名前付き定数に一致するかどうか確認されます。 値がパーサーが理解できるプリミティブまたは列挙型の定数名でない場合、該当する型は、変換された文字列に基づく値または参照を提供できる必要があります。

> [!NOTE]
> XAML 言語ディレクティブでは、型コンバーターは使用されません。

### <a name="type-converters-and-markup-extensions"></a>型コンバーターとマークアップ拡張機能

マークアップ拡張機能の使用は、プロパティの型やその他の考慮事項を確認する前に、XAML プロセッサで処理される必要があります。 たとえば、属性として設定されるプロパティが、通常は型変換を行うものの、特定のケースではマークアップ拡張機能を使用して設定するという場合は、マークアップ拡張機能の動作が最初に処理されます。 マークアップ拡張機能が必要になる 1 つの一般的な状況は、既に存在するオブジェクトを参照する場合です。 このシナリオでは、ステートレスな型コンバーターは新しいインスタンスを生成することしかできないため、望ましくありません。 マークアップ拡張機能について詳しくは、「 [Markup Extensions for XAML Overview](markup-extensions-overview.md)」をご覧ください。

### <a name="native-type-converters"></a>ネイティブな型コンバーター

Windows プレゼンテーション ファンデーション (WPF) および .NET XAML サービスの実装では、ネイティブ型変換処理を持つ特定の CLR 型があります。 ただし、これらの CLR 型は、従来はプリミティブとは考え方が異なります。 このような型の例として、 <xref:System.DateTime>が挙げられます。 この理由の 1 つは、.NET Framework のアーキテクチャがどのように機能するかにあります。 <xref:System.DateTime> 型は、.NET の最も基本的なライブラリである mscorlib で定義されています。 <xref:System.DateTime>は、依存関係を導入する別のアセンブリから取得された属性を持つ属性を持つ許可<xref:System.ComponentModel.TypeConverterAttribute>されていません ( System から取得します 。 したがって、帰属による通常の型コンバーター検出メカニズムはサポートされません。 代わりに、XAML パーサーは、ネイティブな処理が必要な型の一覧を保持し、それらの型を通常のプリミティブの処理と類似した方法で処理します。 <xref:System.DateTime>の場合、その処理には <xref:System.DateTime.Parse%2A>の呼び出しが含まれます。

## <a name="implementing-a-type-converter"></a>型コンバーターの実装

以下のセクションで、 <xref:System.ComponentModel.TypeConverter> クラスの API について説明します。

### <a name="typeconverter"></a>TypeConverter

NET XAML サービスでは、XAML 目的で使用されるすべての型コンバーターは、基本クラスから派生するクラス<xref:System.ComponentModel.TypeConverter>です。 <xref:System.ComponentModel.TypeConverter> クラスは、XAML が登場するより前のバージョンの .NET Framework にも含まれていました。 <xref:System.ComponentModel.TypeConverter> を使用する元々のシナリオの 1 つは、ビジュアル デザイナーのプロパティ エディターに文字列の変換を提供することでした。

XAML では、 <xref:System.ComponentModel.TypeConverter> の役割が拡張されました。 XAML の目的では、 <xref:System.ComponentModel.TypeConverter> は、特定の文字列への変換と特定の文字列からの変換をサポートする基底クラスです。 文字列からの変換は、XAML から文字列属性値への解析に利用されます。 文字列への変換は、特定のオブジェクト プロパティの実行時の値をシリアル化のために XAML の属性に戻す処理に利用されます。

<xref:System.ComponentModel.TypeConverter> には、XAML を処理する目的で、文字列への変換と文字列からの変換に関連する次の 4 つのメンバーが定義されています。

- <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A>

- <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A>

- <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>

- <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>

これらのメンバーの中で最も重要なメソッドは <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>であり、入力文字列を必要なオブジェクトの型に変換します。 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> メソッドの実装では、さまざまな型をコンバーターの目的とする型に変換する処理を実現できます。 したがって、実行時の変換をサポートするなど、XAML 以外の目的でも使用できます。 ただし、XAML の用途では、 <xref:System.String> 入力を処理できるコード パスのみが重要です。

2 番目に重要な方法<xref:System.ComponentModel.TypeConverter.ConvertTo%2A>は です。 アプリケーションがマークアップ表現に変換される場合 (たとえば、XAML にファイルとして保存される場合)、<xref:System.ComponentModel.TypeConverter.ConvertTo%2A>マークアップ表現を生成する XAML テキスト ライターの大規模なシナリオに関与します。 この場合、XAML にとって重要なコード パスは、呼び出し元が `destinationType` の <xref:System.String>を渡す時です。

<xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> と <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> は、サービスが <xref:System.ComponentModel.TypeConverter> の実装の機能を照会する時に使用されるサポート メソッドです。 これらのメソッドは、その型について、相当する変換メソッドをコンバーターがサポートしている場合に `true` を返すように実装する必要があります。 XAML の目的では、通常、 <xref:System.String> 型であることを意味します。

### <a name="culture-information-and-type-converters-for-xaml"></a>カルチャ情報と XAML の型コンバーター

各 <xref:System.ComponentModel.TypeConverter> 実装では、変換に対して有効な文字列を独自に解釈できます。また、パラメーターとして渡される型の説明を使用することも無視することもできます。 カルチャと XAML の型変換については、重要な考慮事項があります。ローカライズ可能な文字列を属性値として使用することは XAML でサポートされていますが、それらのローカライズ可能な文字列を、特定のカルチャ要件を指定して型コンバーターの入力として使用することはできません。 この制限の理由は、XAML 属性値の型コンバーターには、特定の言語に固定して ( `en-US` カルチャを使用して) 実行しなければならない XAML 処理の動作がどうしても含まれるためです。 この制限の設計上の理由の詳細については、「XAML 言語仕様 ([\[MS-XAML\]](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))) 」または「 [WPF のグローバリゼーションとローカリゼーションの概要](../../framework/wpf/advanced/wpf-globalization-and-localization-overview.md)」を参照してください。

カルチャが問題となる例として、一部のカルチャで文字列形式の数値の小数点記号にピリオドではなくコンマが使用されることが挙げられます。 そのように使用した場合、区切り記号としてコンマを使用する多くの既存の型コンバーターで、動作が競合します。 周囲の XAML で `xml:lang` を使用してカルチャを指定しても、この問題は解決しません。

### <a name="implementing-convertfrom"></a>ConvertFrom の実装

XAML をサポートする <xref:System.ComponentModel.TypeConverter> の実装としてコンバーターを使用できるようにするためには、そのコンバーターの <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> メソッドが `value` パラメーターとして文字列を受け入れる必要があります。 文字列が有効な形式であり、 <xref:System.ComponentModel.TypeConverter> 実装で変換できる場合、実装から返すオブジェクトは、プロパティで想定される型へのキャストをサポートしている必要があります。 それ以外の場合、 <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 実装は `null`を返す必要があります。

各 <xref:System.ComponentModel.TypeConverter> 実装では、変換に対して有効な文字列の構成内容を独自に解釈できます。また、パラメーターとして渡される型の説明やカルチャ コンテキストを使用することも無視することもできます。 ただし、WPF による XAML 処理では、型の説明コンテキストに値を渡さない場合があり、 `xml:lang`に基づくカルチャを渡さない場合もあります。

> [!NOTE]
> かっこ (){}を使用しない場合は、文字列形式の要素として、特に左中かっこ ({) を使用しないでください。 これらの文字は、マークアップ拡張シーケンスの開始および終了を示す文字として予約されています。

型コンバーターが .NET XAML Services オブジェクト ライターから XAML サービスにアクセスする必要があるが、コンテキストに<xref:System.IServiceProvider.GetService%2A>対して行われた呼び出しがそのサービスを返さない場合は、例外をスローするのが適切です。

### <a name="implementing-convertto"></a>ConvertTo の実装

<xref:System.ComponentModel.TypeConverter.ConvertTo%2A> は、シリアル化のサポートで使用される可能性があります。 カスタム型およびその型コンバーターに対して <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> によるシリアル化をサポートすることは、絶対要件ではありません。 ただし、コントロールを実装する場合、またはクラスの機能または設計の一部としてシリアル化を使用する場合は、 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A>を実装する必要があります。

XAML をサポートする <xref:System.ComponentModel.TypeConverter> の実装としてコンバーターを使用できるようにするためには、そのコンバーターの <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> メソッドが、サポートされる型のインスタンス (または値) を `value` パラメーターとして受け入れる必要があります。 `destinationType` パラメーターが <xref:System.String>型の場合、返されるオブジェクトは <xref:System.String>にキャストできる必要があります。 返される文字列は、 `value`のシリアル化された値を表している必要があります。 理想としては、採用するシリアル化の形式は、その文字列を同じコンバーターの <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> の実装に渡した場合と比べて情報の大きな損失が発生することなく、同じ値を生成できる必要があります。

値をシリアル化できない場合、またはコンバーターがシリアル化をサポートしていない場合は、 <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> の実装は `null` を返す必要があり、例外をスローできます。 ただし、例外をスローする場合は、 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> 実装の一部として、その変換を使用できないことを通知するようにしてください。そうすれば、まず <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> を確認することによって例外を回避するというベスト プラクティスをサポートできます。

`destinationType` パラメーターが <xref:System.String>型でない場合は、独自のコンバーター処理を実装できます。 通常は、基底の実装の処理に戻り、基底の <xref:System.ComponentModel.TypeConverter.ConvertTo%2A> で特定の例外を発生させます。

型コンバーターが .NET XAML Services オブジェクト ライターから XAML サービスにアクセスする必要があるが、コンテキストに<xref:System.IServiceProvider.GetService%2A>対して行われた呼び出しがそのサービスを返さない場合は、例外をスローするのが適切です。

### <a name="implementing-canconvertfrom"></a>CanConvertFrom の実装

<xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> の実装は、 `true` が `sourceType` 型の場合は <xref:System.String> を返し、それ以外の場合は基底の実装に任せる必要があります。 <xref:System.ComponentModel.TypeConverter.CanConvertFrom%2A> から例外をスローしないでください。

### <a name="implementing-canconvertto"></a>CanConvertTo の実装

<xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> の実装は、 `true` が `destinationType` 型の場合は <xref:System.String>を返し、それ以外の場合は基底の実装に任せる必要があります。 <xref:System.ComponentModel.TypeConverter.CanConvertTo%2A> から例外をスローしないでください。

## <a name="applying-the-typeconverterattribute"></a>TypeConverterAttribute の適用

カスタム型コンバーターを .NET XAML サービスによるカスタム クラスの代理型コンバーターとして使用するには、 を<xref:System.ComponentModel.TypeConverterAttribute>クラス定義に適用する必要があります。 属性を通して指定する <xref:System.ComponentModel.TypeConverterAttribute.ConverterTypeName%2A> は、カスタム型コンバーターの型名である必要があります。 この属性を適用すると、プロパティの型としてカスタム クラスの型が使用されている値を XAML プロセッサが処理する際に、入力文字列を処理して、オブジェクトのインスタンスを返すことができます。

また、プロパティごとに型コンバーターを提供することもできます。 を<xref:System.ComponentModel.TypeConverterAttribute>クラス定義に適用するのではなく、プロパティ定義 (その中の`get`/`set`実装ではなく、メイン定義) に適用します。 プロパティの型は、カスタム型コンバーターによって処理される型と一致する必要があります。 この属性を適用すると、プロパティの値を XAML プロセッサが処理する際に、入力文字列を処理して、オブジェクトのインスタンスを返すことができます。 プロパティごとの型コンバーターの手法は、Microsoft .NET Framework またはクラス定義を制御できず、そのライブラリからプロパティ型を使用する場合に便利です<xref:System.ComponentModel.TypeConverterAttribute>。

アタッチされたカスタム メンバーの型変換動作を割り当てるには、アタッチされたメンバーの実装パターンの <xref:System.ComponentModel.TypeConverterAttribute> アクセサー メソッドに `Get` を適用します。

## <a name="accessing-service-provider-context-from-a-markup-extension-implementation"></a>マークアップ拡張機能の実装からサービス プロバイダーのコンテキストにアクセスする

使用可能なサービスは、すべての値コンバーターの場合と同じです。 ただし、それぞれの値コンバーターがサービス コンテキストを受け取る方法が違います。 サービスへのアクセスと、使用できるサービスについては、「 [Type Converters and Markup Extensions for XAML](type-converters-and-markup-extensions.md)」のトピックをご覧ください。

## <a name="type-converters-in-the-xaml-node-stream"></a>XAML ノード ストリームでの型コンバーター

XAML ノード ストリームを処理している場合、型コンバーターのアクションや最終結果はまだ実行されていません。 読み込みパスでは、読み込むために最終的に型変換する必要がある属性文字列は、開始メンバーおよび終了メンバー内でテキスト値のままです。 この処理のために最終的に必要になる型コンバーターは、 <xref:System.Xaml.XamlMember.TypeConverter%2A?displayProperty=nameWithType> プロパティを使用することで判別できます。 ただし、 <xref:System.Xaml.XamlMember.TypeConverter%2A?displayProperty=nameWithType> から有効な値を取得するには、基になるメンバー、またはメンバーが使用するオブジェクト値の型を介してこのような情報にアクセスできる XAML スキーマ コンテキストを持っていることが必要です。 型変換の動作を呼び出すためにも、型マッピングと、コンバーター インスタンスの作成が必要であるため、XAML スキーマ コンテキストが必要になります。

## <a name="see-also"></a>関連項目

- <xref:System.ComponentModel.TypeConverterAttribute>
- [XAML の型コンバーターおよびマークアップ拡張機能](type-converters-and-markup-extensions.md)
- [XAML の概要 (WPF)](../fundamentals/xaml.md)
