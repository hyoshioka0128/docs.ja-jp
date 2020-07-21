---
title: XAML の型コンバーターおよびマークアップ拡張機能
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], type converter services
- XAML [XAML Services], value converters
- XAML [XAML Services], markup extension services
- value converters for XAML [XAML Services]
- XAML [XAML Services], service context
ms.assetid: db07a952-05ce-4aa4-b6f9-aac7397d0326
ms.openlocfilehash: bee94b03d4fd6e6f5ef8571e83f554b381dd6582
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432888"
---
# <a name="type-converters-and-markup-extensions-for-xaml"></a>XAML の型コンバーターおよびマークアップ拡張機能

型コンバーターとマークアップ拡張機能は、XAML 型システムと XAML ライターが、オブジェクト グラフ コンポーネントを生成するために使用する 2 つの手法です。 型コンバーターとマークアップ拡張機能は、一部の特性を共有しますが、XAML ノード ストリームでは異なる方法で表現されます。 このドキュメント セットでは、型コンバーター、マークアップ拡張機能、およびこれに類似したコンストラクトを、値コンバーターと総称することがあります。

## <a name="value-converters"></a>値コンバーター

XAML では、さまざまなシナリオで値コンバーターが使用されます。 XAML におけるさまざまな種類の値コンバーターは次のとおりです。

- 型コンバーター

- マークアップ拡張機能

- 値シリアライザー

- XAML テキスト構文のロジックを提供する関連クラスまたはサポート クラス

## <a name="type-converters"></a>型コンバーター

NET XAML サービス定義では、型コンバーターは CLR<xref:System.ComponentModel.TypeConverter>クラスから派生するクラスです。 <xref:System.ComponentModel.TypeConverter>は、XAML が存在する前に .NET にあったクラスです。 本来の目的は、プロパティ ウィンドウと、IDE プロパティの同様のテキストベースの編集メタファーをサポートすることでした。 .NET に XAML を<xref:System.ComponentModel.TypeConverter>導入すると、(属性値または XAML 値ノードに含まれる) テキスト構文をオブジェクトに変換できます。 また、<xref:System.ComponentModel.TypeConverter> を使用して、オブジェクト値をテキスト構文にシリアル化することもできます。 <xref:System.ComponentModel.TypeConverter>は、Windows プレゼンテーション ファンデーション (WPF) および Windows コミュニケーション ファウンデーション (WCF) の以前のフレームワーク固有の XAML 実装でも使用されていました。 XAML の <xref:System.ComponentModel.TypeConverter> の詳細については、「 [Type Converters for XAML Overview](type-converters-overview.md)といった以前のフレームワーク固有の XAML 実装でも使用されていました。

## <a name="markup-extensions"></a>マークアップ拡張機能

NET XAML サービスの実装では、マークアップ拡張機能は、クラスから<xref:System.Windows.Markup.MarkupExtension>派生するクラスです。 この形式のマークアップ拡張機能は、XAML 言語で考案された概念です。 マークアップ拡張機能は、サービス クラスを呼び出してロジックを提供する、拡張性を持ったエスケープ シーケンスのようなものと考えることができます。 マークアップの観点からすると、XAML プロセッサは、テキスト文字列内の左中かっこ ({) で始まるテキスト シーケンスによってマークアップ拡張機能を汎用的に認識します。

マークアップ拡張機能は、型コンバーターとは異なります。 型コンバーターは、通常、型またはメンバーに関連付けられ、 オブジェクト グラフの作成またはシリアル化においてそれらのエンティティに関連付けられたテキスト構文が検出されると呼び出されます。

マークアップ拡張機能は、単一のサポート サービス クラスに関連付けられますが、任意のメンバー値に適用できます。 (ただし、マークアップ拡張機能を実装して、サービス コンテキストを使用して、特定のメンバーまたは変換先の型への使用を意図的に制限できます)。マークアップ拡張機能は、型コンバーターの関連付けをオーバーライドできます。 または、テキスト構文をサポートしないメンバーの属性値を指定するためにマークアップ拡張機能を使用することもできます。

XAML でのマークアップ拡張機能の実装パターンの詳細については、「 [Markup Extensions for XAML Overview](markup-extensions-overview.md)」を参照してください。

## <a name="value-serializers"></a>値シリアライザー

<xref:System.Windows.Markup.ValueSerializer> は、オブジェクトを文字列に変換するために最適化された特殊な型コンバーターです。 XAML の <xref:System.Windows.Markup.ValueSerializer> は、 `ConvertFrom` メソッドを一切実装しません。 <xref:System.Windows.Markup.ValueSerializer> 実装は、 <xref:System.ComponentModel.TypeConverter> 実装と同様の方法でサービスを取得します 仮想メソッドは入力 `context` パラメーターを提供しています。 `context` パラメーターの型は <xref:System.Windows.Markup.IValueSerializerContext>であり、 <xref:System.IServiceProvider> インターフェイスを継承し、 <xref:System.IServiceProvider.GetService%2A> メソッドを持ちます。

XAML 型システムと、シリアル化のために XAML ノード ループ処理を使用する XAML ライターの実装では、型またはメンバーに関連付けられた値コンバーターは、独自の <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> プロパティによって報告されます。 シリアル化を実行する XAML ライターにとっては、 <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> と <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> が存在する場合には、読み込みパス用に型コンバーターを使用し、保存パス用に値シリアライザーを使用する必要があるということを意味しています。 <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> は存在するものの、 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> が `null`の場合は、保存パス用にも型コンバーターを使用します。

## <a name="other-value-converters"></a>その他の値コンバーター

値コンバーターは、型コンバーターまたはマークアップ拡張機能の特定のパターンを超えて拡張できます。 ただし、このカスタマイズでは、.NET XAML サービスによって提供される XAML 型システムの再定義も必要になります。 既存の XAML 型システムには、型コンバーター、マークアップ拡張機能、および値シリアライザー向けの表現とレポート システムがありますが、値変換のカスタム形式向けの表現とレポート システムはありません。 カスタム値コンバーターを作成する場合は、 <xref:System.Xaml.Schema.XamlValueConverter%601> 型を使用します。

## <a name="type-converters-and-markup-extensions-in-combination"></a>型コンバーターとマークアップ拡張機能の組み合わせ

マークアップ拡張機能と型コンバーターは、XAML の異なる状況で使用されます。 マークアップ拡張機能の使用時にはコンテキストを利用できますが、マークアップ拡張機能が値を提供するプロパティの型変換動作は一般にマークアップ拡張機能の実装ではチェックされません。 つまり、マークアップ拡張機能が `ProvideValue` 出力としてテキスト文字列を返す場合でも、特定のプロパティまたはプロパティ値型に適用される、その文字列に対する型変換動作は呼び出されません。 一般に、マークアップ拡張機能の目的は、型コンバーターを呼び出さずに文字列を処理してオブジェクトを返すことです。

## <a name="service-context-for-a-value-converter"></a>値コンバーターのサービス コンテキスト

値コンバーターを実装する際には、通常、値コンバーターが適用されるコンテキストにアクセスする必要があります。 このコンテキストは、サービス コンテキストと呼ばれます。 サービス コンテキストには、アクティブな XAML スキーマ コンテキスト、XAML スキーマ コンテキスト、XAML オブジェクト ライターが提供する型マッピング システムへのアクセスなどの情報が含まれる場合があります。 値コンバーターで使用可能なサービス コンテキストとサービス コンテキストが提供するサービスへのアクセス方法の詳細については、「 [Service Contexts Available to Type Converters and Markup Extensions](service-contexts-with-type-converters-and-markup-extensions.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Markup.MarkupExtension>
- <xref:System.Xaml.XamlObjectWriter>
- [XAML のマークアップ拡張機能の概要](markup-extensions-overview.md)
- [XAML の型コンバーターの概要](type-converters-overview.md)
- [型コンバーターおよびマークアップ拡張機能で使用できるサービス コンテキスト](service-contexts-with-type-converters-and-markup-extensions.md)
