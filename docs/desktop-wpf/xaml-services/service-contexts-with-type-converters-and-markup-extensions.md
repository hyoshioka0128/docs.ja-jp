---
title: 型コンバーターおよびマークアップ拡張機能で使用できるサービス コンテキスト
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], type converter services how-to
ms.assetid: b4dad00f-03da-4579-a4e9-d8d72d2ccbce
ms.openlocfilehash: 59c4385eb4df8c622be6164cdb0a1a911c445ca8
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432894"
---
# <a name="service-contexts-available-to-type-converters-and-markup-extensions"></a>型コンバーターおよびマークアップ拡張機能で使用できるサービス コンテキスト
型コンバーターとマークアップ拡張機能の使用をサポートする型の作成者には、マークアップまたは周辺のオブジェクト グラフ構造体のどこで使用されているかを示す文脈情報が必要です。 情報は、指定されるオブジェクトを正しくインスタンス化するため、またオブジェクト グラフ内の既存オブジェクトへのオブジェクト参照を行うために必要です。 NET XAML サービスを使用する場合、必要なコンテキストは一連のサービス インターフェイスとして公開されます。 型コンバーターまたはマークアップ拡張のサポート コードでは、 <xref:System.Xaml.XamlObjectWriter> または関連する型から渡される使用可能なサービス プロバイダー コンテキストを使用して、サービスを照会できます。 XAML スキーマ コンテキストは、このようなサービスを通じて直接使用できます。 このトピックでは、値コンバーター実装からサービス コンテキストにアクセスする方法を説明し、通常使用できるサービスとその役割の一覧を示します。

## <a name="obtaining-services"></a>サービスの取得

値コンバーターの実装者は、通常、値コンバーターが適用される何らかの種類のコンテキストにアクセスする必要があります。 このコンテキストには、アクティブな XAML スキーマ コンテキスト、XAML スキーマ コンテキスト、XAML オブジェクト ライターが提供する型マッピング システムへのアクセスなどの情報が含まれる場合があります。 マークアップ拡張機能または型コンバーターの実装で使用されるサービスは、各仮想メソッドのシグネチャの一部であるコンテキスト パラメーターを通じて伝達されます。 いずれの場合でも、コンテキストに <xref:System.IServiceProvider> が実装されているので、 <xref:System.IServiceProvider.GetService%2A?displayProperty=nameWithType> を呼び出してサービスを要求することができます。

## <a name="services-for-a-markup-extension"></a>マークアップ拡張機能のサービス

<xref:System.Windows.Markup.MarkupExtension> には、仮想メソッドが 1 つだけあります ( <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>)。 入力パラメーター `serviceProvider` は、XAML プロセッサによってマークアップ拡張機能が呼び出されたときに、サービスが実装に伝達される方法を示します。 次の疑似コードは、マークアップ拡張機能の実装が <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A>でサービスを照会する方法を示します。

```csharp
public override object ProvideValue(IServiceProvider serviceProvider)
{
...
    // Get the IXamlTypeResolver from the service provider
    if (serviceProvider == null)
    {
        throw new ArgumentNullException("serviceProvider");
    }
    IXamlTypeResolver xamlTypeResolver = serviceProvider.GetService(typeof(IXamlTypeResolver)) as IXamlTypeResolver;
    if (xamlTypeResolver == null)
   {
        throw new ArgumentException("IXamlTypeResolver"));
    }
...
}
```

## <a name="services-for-a-type-converter"></a>型コンバーターのサービス

<xref:System.ComponentModel.TypeConverter> には、サービス コンテキストを使用し、XAML の使用をサポートする仮想メソッドが 4 つあります。 これらのメソッドは、それぞれ入力パラメーター `context` を渡します。 このパラメーターの型は <xref:System.ComponentModel.ITypeDescriptorContext>ですが、そのインターフェイスは <xref:System.IServiceProvider>を継承するため、型コンバーターの実装では <xref:System.IServiceProvider.GetService%2A> メソッドを使用できます。

次の疑似コードは、XAML の使用に対する型コンバーターの実装が、そのオーバーライドの 1 つ (このケースでは <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A>) の中でサービスを照会する方法を示します。

```csharp
public override object ConvertFrom(ITypeDescriptorContext typeDescriptorContext,
  CultureInfo cultureInfo,
  object source)
{
    IRootObjectProvider rootProvider = typeDescriptorContext.GetService(typeof(IRootObjectProvider)) as IRootObjectProvider;
    if (rootProvider != null && source is String)
    {
        //return something, else ...
    }
    throw GetConvertFromException(source);
}
```

## <a name="services-for-a-value-serializer"></a>値シリアライザー サービス

値シリアライザーのコンテキストでは、 <xref:System.Windows.Markup.ValueSerializer> クラスに固有のサービス プロバイダー型 <xref:System.Windows.Markup.IValueSerializerContext>を使用します。 このコンテキストは、 <xref:System.Windows.Markup.ValueSerializer> の 4 つの仮想メソッドのオーバーライドに渡されます。 サービスを取得するには、コンテキストから <xref:System.IServiceProvider.GetService%2A> を呼び出します。

## <a name="using-the-xaml-service-provider-contexts"></a>XAML サービス プロバイダー コンテキストの使用

マークアップ拡張機能または型<xref:System.IServiceProvider.GetService%2A>コンバーターが使用できる XAML サービスにアクセスするためのサービス プロバイダーは内部クラスとして実装され、インターフェイスを通じてのみ公開され、関連するコンテキストに渡される方法が提供されます。 既定の .NET XAML サービスのロード パスまたは保存パスの実装で XAML 処理操作がサービス コンテキストを必要とする関連するマークアップ拡張機能または型コンバーター メソッドを呼び出すたびに、この内部オブジェクトが渡されます。 状況に応じて、システムのサービス コンテキストは `MarkupExtensionContext` か `TextSyntaxContext`を提供しますが、これら両方のクラスの詳細は内部にあります。 これらのクラスとの対話は、 <xref:System.IServiceProvider.GetService%2A>を通してサービスを要求することに限定されます。

## <a name="available-services-from-the-net-xaml-service-context"></a>.NET XAML サービス コンテキストから利用できるサービス

.NET XAML サービスは、マークアップ拡張機能、型コンバーター、値のシリアライザー、およびその他の使用法のサービスを定義します。 この後のセクションでは、これらの各サービスについて説明し、実装でのサービスの使用方法についてガイダンスを提供します。

### <a name="iserviceprovider"></a>IServiceProvider

**リファレンス ドキュメント**:<xref:System.IServiceProvider>

**関連する:** を呼び出<xref:System.IServiceProvider.GetService%2A?displayProperty=nameWithType>すことができるように、.NET でサービス ベースのインフラストラクチャの基本的な操作。

### <a name="itypedescriptorcontext"></a>ITypeDescriptorContext

**リファレンス ドキュメント**:<xref:System.ComponentModel.ITypeDescriptorContext>

<xref:System.IServiceProvider> の派生クラスです。 このクラスは <xref:System.ComponentModel.TypeConverter> の標準シグネチャのコンテキストを表します。 <xref:System.ComponentModel.TypeConverter> は、.NET Framework 1.0 の時点から存在していたクラスです。 つまり、XAML や、文字列値の型変換という XAML <xref:System.ComponentModel.TypeConverter> のシナリオが登場する前から使用されていました。 NET XAML サービスのコンテキストでは、<xref:System.ComponentModel.TypeConverter>メソッドは明示的に実装されます。 その明示的な実装の動作により、 <xref:System.ComponentModel.ITypeDescriptorContext> API が XAML の型システムまたは XAML からのオブジェクトの読み取りや書き込みに関連したものでないことが、呼び出し側に示されます。 <xref:System.ComponentModel.ITypeDescriptorContext.Container%2A>、<xref:System.ComponentModel.ITypeDescriptorContext.Instance%2A>および<xref:System.ComponentModel.ITypeDescriptorContext.PropertyDescriptor%2A>.NET `null` XAML サービス のコンテキストから戻る一般的な。

### <a name="ivalueserializercontext"></a>IValueSerializerContext

**リファレンス ドキュメント**:<xref:System.Windows.Markup.IValueSerializerContext>

<xref:System.ComponentModel.ITypeDescriptorContext> から派生します。これについても、XAML の型システムに不適切な影響を与えないようにするために、明示的な実装に依存します。 <xref:System.Windows.Markup.ValueSerializer>の静的ルックアップ ヘルパー メソッドをサポートします。

### <a name="ixamltyperesolver"></a>IXamlTypeResolver

**リファレンス ドキュメント**:<xref:System.Windows.Markup.IXamlTypeResolver>

**定義元:**  <xref:System.Windows.Markup> 名前空間、System.Xaml アセンブリ

**関連:** 読み込みパスのシナリオ、および XAML スキーマ コンテキストとの対話

**サービス API:**  <xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A>

XAML ライターがオブジェクト グラフに CLR オブジェクトを構築するときに必要な、XAML から CLR への型マッピングに影響を与えることができます。 <xref:System.Windows.Markup.IXamlTypeResolver.Resolve%2A> は、XAML の型名 (<xref:System.Xaml.XamlType.Name%2A?displayProperty=nameWithType>) に対応する、プレフィックス修飾されていることのある文字列を処理し、CLR の <xref:System.Type>を返します。 型の解決は、通常、XAML スキーマ コンテキストに大きく依存します。 XAML スキーマ コンテキストだけが、どのアセンブリが読み込まれているか、これらのアセンブリの中で、型を解決するためにアクセスできる、またはアクセスする必要があるものはどれかといった考慮事項を認識しています。

### <a name="iuricontext"></a>IUriContext

**リファレンス ドキュメント**:<xref:System.Windows.Markup.IUriContext>

**定義元:**  <xref:System.Windows.Markup> 名前空間、System.Xaml アセンブリ

**関連:** URI または `x:Uri` 値であるメンバー値を処理する読み込みパスおよび保存パス。

**サービス API:**  <xref:System.Windows.Markup.IUriContext.BaseUri%2A>

このサービスは、グローバルに使用できる URI ルート (存在する場合) を報告します。 URI ルートは、相対 URI を絶対 URI に解決する場合、またはその逆を行う場合に使用できます。 このシナリオは主に、特定のフレームワークによって、またはフレームワークでよく使用されるルート要素クラスの機能によって公開されるアプリケーション サービスに関連しています。 ベース URI は、XAML リーダーの設定として確立することができます。その後、XAML オブジェクト ライターに渡され、このサービスによってレポートされます。

### <a name="iambientprovider"></a>IAmbientProvider

**リファレンス ドキュメント**:<xref:System.Xaml.IAmbientProvider>

**定義元:**  <xref:System.Xaml> 名前空間、System.Xaml アセンブリ

**関連:** 型の参照の遅延または最適化を処理する読み込みパス。

**サービス API:**  <xref:System.Xaml.IAmbientProvider.GetAllAmbientValues%2A>、その他 3 つ。

XAML におけるアンビエンスの概念は、型の特定のメンバーをアンビエントとしてマーク付けする手法です。 あるいは、型のインスタンスを保持するすべてのプロパティ値をアンビエント プロパティと見なす必要がある場合には、型をアンビエントにすることもできます。 XAML ノード ストリームの先にあるか、オブジェクト グラフの下位にあるマークアップ拡張機能または型コンバーターは、読み込み時にアンビエント プロパティまたは型インスタンスにアクセスしたり、保存時にアンビエント構造の情報を活用したりできます。 これにより、 <xref:System.Windows.Markup.IXamlTypeResolver> や `x:Type`など、その他のサービスの型解決に必要な修飾の程度が左右されます。 <xref:System.Xaml.AmbientPropertyValue> も参照してください。

### <a name="ixamlschemacontextprovider"></a>IXamlSchemaContextProvider

**リファレンス ドキュメント**:<xref:System.Xaml.IXamlSchemaContextProvider>

**定義元:**  <xref:System.Xaml> 名前空間、System.Xaml アセンブリ

**関連:** 読み込みパス、および XAML 型をバッキング型に解決する必要があるその他の操作。

**サービス API:**  <xref:System.Xaml.IXamlSchemaContextProvider.SchemaContext%2A>

遅延コンテンツを統合するには、同じスキーマ コンテキストを遅延領域に対しても適用する必要があるので、遅延読み込み操作には XAML スキーマ コンテキストが必要です。 XAML スキーマ コンテキストの役割の詳細については、「 [XAML Services](../../../api/index.md)」を参照してください。

### <a name="irootobjectprovider"></a>IRootObjectProvider

**リファレンス ドキュメント**:<xref:System.Xaml.IRootObjectProvider>

**定義元:**  <xref:System.Xaml> 名前空間、System.Xaml アセンブリ

**関連:** 読み込みパス。

**サービス API:**  <xref:System.Xaml.IRootObjectProvider.RootObject%2A>

このサービスは、特定のフレームワークによって、またはフレームワークでよく使用されるルート要素クラスの機能によって公開されるアプリケーション サービスに関連しています。 ルート オブジェクトを取得する 1 つのシナリオは、分離コードとイベント接続をつなげることです。 たとえば、 `x:Class` の WPF 実装は、マークアップ コンパイルと、XAML マークアップの他の場所にあるイベント ハンドラー属性の関連付けにおいて使用されます。 マークアップ コンパイルの部分クラスで定義されたマークアップと分離コードのコネクション ポイントは、ルート要素です。

### <a name="ixamlnamespaceresolver"></a>IXamlNamespaceResolver

**リファレンス ドキュメント**:<xref:System.Xaml.IXamlNamespaceResolver>

**定義元:**  <xref:System.Xaml> 名前空間、System.Xaml アセンブリ

**関連:** 読み込みパス、保存パス。

**サービス API:** <xref:System.Xaml.IXamlNamespaceResolver.GetNamespace%2A> 、保存パスの場合は <xref:System.Xaml.IXamlNamespaceResolver.GetNamespacePrefixes%2A> 。

<xref:System.Xaml.IXamlNamespaceResolver> は、元の XAML マークアップで対応付けられたプレフィックスに基づく XAML 名前空間 ID/URI を返すことができるサービスです。

### <a name="iprovidevaluetarget"></a>IProvideValueTarget

**リファレンス ドキュメント**:<xref:System.Windows.Markup.IProvideValueTarget>

**定義元:**  <xref:System.Windows.Markup> 名前空間、System.Xaml アセンブリ

**関連:** 読み込みパス、保存パス。

**サービス API:**<xref:System.Windows.Markup.IProvideValueTarget.TargetObject%2A> <xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A>、 .  

型コンバーターまたはマークアップ拡張機能は、<xref:System.Windows.Markup.IProvideValueTarget> を使用して、読み込み時に動作している場所に関するコンテキストを取得できます。 実装では、このコンテキストを使用して、特定の使用を無効にすることもできます。 たとえば、WPF では、 <xref:System.Windows.DynamicResourceExtension>などの一部のマークアップ拡張機能内にロジックを保持しています。 そのロジックは、 <xref:System.Windows.Markup.IProvideValueTarget.TargetProperty%2A> を確認して、依存関係のあるプロパティ (または、その他の依存関係のないプロパティの短い一覧) を設定する場合にのみ拡張機能が使用されるようにできます。

### <a name="ixamlnameresolver"></a>IXamlNameResolver

**リファレンス ドキュメント**:<xref:System.Xaml.IXamlNameResolver>

**定義元:**  <xref:System.Xaml> 名前空間、System.Xaml アセンブリ

**関連する:** パス オブジェクト グラフ定義を読み込み`x:Name`、`x:Reference`によって識別されるオブジェクトを解決する、 、またはフレームワーク固有の手法。

**サービス API:**  <xref:System.Xaml.IXamlNameResolver.Resolve%2A>、前方参照を処理する場合などの高度なシナリオで使用されるその他の API。

.NET XAML サービス`x:Reference`の処理の実装は、このサービスに依存します。 特定のフレームワークまたはそのフレームワークをサポートするツールは、このサービスを使用して、 `x:Name` の処理、または同等の (<xref:System.Windows.Markup.RuntimeNamePropertyAttribute> 属性で指定された) プロパティの処理を行います。

### <a name="idestinationtypeprovider"></a>IDestinationTypeProvider

**リファレンス ドキュメント**:<xref:System.Xaml.IDestinationTypeProvider>

**定義元:**  <xref:System.Xaml> 名前空間、System.Xaml アセンブリ

**関連:** 読み込みパスでの間接的な CLR 型情報の解決。

**サービス API:** <xref:System.Xaml.IDestinationTypeProvider.GetDestinationType%2A>

詳細については、「<xref:System.Xaml.IDestinationTypeProvider>」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Markup.MarkupExtension>
- <xref:System.Xaml.XamlObjectWriter>
- [XAML のマークアップ拡張機能の概要](markup-extensions-overview.md)
- [XAML の型コンバーターの概要](type-converters-overview.md)
