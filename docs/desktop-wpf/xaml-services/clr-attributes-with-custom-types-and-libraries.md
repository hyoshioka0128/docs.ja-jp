---
title: カスタム型およびライブラリの XAML 関連の CLR 属性
ms.date: 03/30/2017
helpviewer_keywords:
- CLR attributes for custom types [XAML Services]
ms.assetid: 5dfb299a-b6e2-41b8-8694-e6ac987547f1
ms.openlocfilehash: 5481d02e4d393312fa0f0dd13b45c54acc567e13
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432984"
---
# <a name="xaml-related-clr-attributes-for-custom-types-and-libraries"></a>カスタム型とカスタム ライブラリの XAML 関連の CLR 属性

このトピックでは、.NET XAML サービスによって定義される共通言語ランタイム (CLR) 属性について説明します。 また、アセンブリまたは型へのアプリケーションの XAML 関連のシナリオを持つ .NET で定義されている他の CLR 属性についても説明します。 これらの CLR 属性を持つアセンブリ、型、またはメンバーに対する属性は、型に関連する XAML 型システム情報を提供します。 情報は、XAML ノード ストリームを直接処理するために .NET XAML サービスを使用する任意の XAML コンシューマーに提供されるか、専用の XAML リーダーと XAML ライターを介して提供されます。

## <a name="xaml-related-clr-attributes-for-custom-types-and-custom-members"></a>カスタム型とカスタム メンバーの XAML 関連の CLR 属性

CLR 属性を使用すると、CLR 全体を使用して型を定義することになります。 CLR を使用して型バッキングを定義する場合、.NET XAML サービス XAML ライターが使用する既定の XAML スキーマ コンテキストは、アセンブリのバッキングに対するリフレクションを通じて CLR 属性を読み取ることができます。

次のセクションでは、カスタム型またはカスタム メンバーに適用できる XAML 関連の属性について説明します。 各 CLR 属性は、XAML 型システムに関連する情報を伝達します。 読み込みパスでは、属性付き情報は、XAML リーダーが有効な XAML ノード ストリームを形成するのに役立つか、XAML ライターが有効なオブジェクト グラフを生成するのに役立ちます。 保存パスでは、属性付きの情報は、XAML リーダーが XAML 型システム情報を再構成する有効な XAML ノード ストリームを形成するのに役立ちます。または、XAML ライターまたはその他の XAML コンシューマーのシリアル化ヒントまたは要件を宣言します。

### <a name="ambientattribute"></a>アンビエント属性

**リファレンス ドキュメント:**<xref:System.Windows.Markup.AmbientAttribute>

**適用対象:** アタッチ可能なプロパティを`get`サポートするクラス、プロパティ、またはアクセサーのメンバー。

**引数:** なし

<xref:System.Windows.Markup.AmbientAttribute>プロパティ、または属性付きの型を受け取るすべてのプロパティは、XAML のアンビエント プロパティの概念の下で解釈されることを示します。 アンビエントの概念は XAML プロセッサがメンバーの型の所有者を確認する方法と関連します。 アンビエント プロパティは、オブジェクト グラフを作成するときにパーサー コンテキストで値が使用できると予想されるが、作成される直接の XAML ノード セットに対して通常の型メンバー検索が中断されるプロパティです。

アンビエント概念は、CLR 属性が定義<xref:System.AttributeTargets>する方法のプロパティとして表されないアタッチ可能なメンバーに適用できます。 メソッドのアトリビューションの使用方法は、XAML のアタッチ`get`可能な使用法をサポートするアクセサーにのみ適用する必要があります。

### <a name="constructorargumentattribute"></a>コンストラクター属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.ConstructorArgumentAttribute>

**適用対象:** クラス

**引数:** 1 つのコンストラクター引数に一致するプロパティの名前を指定する文字列。

<xref:System.Windows.Markup.ConstructorArgumentAttribute>パラメーターなしのコンストラクター構文を使用してオブジェクトを初期化できること、および指定した名前のプロパティが構築情報を提供することを指定します。 この情報は主に XAML シリアル化用です。 詳細については、「<xref:System.Windows.Markup.ConstructorArgumentAttribute>」を参照してください。

### <a name="contentpropertyattribute"></a>プロパティ属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.ContentPropertyAttribute>

**適用対象:** クラス

**引数:** 属性付き型のメンバーの名前を指定する文字列。

<xref:System.Windows.Markup.ContentPropertyAttribute>は、引数によって指定されたプロパティが、その型の XAML コンテンツ プロパティとして機能することを示します。 XAML コンテンツ プロパティ定義は、定義する型に割り当て可能なすべての派生型に継承されます。 特定の派生型に適用することで、特定の派生型の<xref:System.Windows.Markup.ContentPropertyAttribute>定義をオーバーライドできます。

XAML コンテンツ プロパティとして機能するプロパティの場合、プロパティのプロパティ要素のタグ付けを XAML の使用法で省略できます。 通常、コンテンツ モデルとコンテインメント モデルの合理化された XAML マークアップを昇格させる XAML コンテンツ プロパティを指定します。 XAML コンテンツ プロパティとして指定できるメンバーは 1 つだけであるため、XAML コンテンツ プロパティとして指定する必要がある型のコンテナー プロパティの中から、デザインを選択できる場合があります。 その他のコンテナー プロパティは、明示的なプロパティ要素と共に使用する必要があります。

XAML ノード ストリームでは、XAML コンテンツ`StartMember`プロパティ`EndMember`は引き続き生成され、ノードは<xref:System.Xaml.XamlMember>. メンバーが XAML コンテンツ プロパティかどうかを確認するには、位置<xref:System.Xaml.XamlType>から値を`StartObject`調べ、の値を<xref:System.Xaml.XamlType.ContentProperty%2A>取得します。

### <a name="contentwrapperattribute"></a>コンテンツラッパー属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.ContentWrapperAttribute>

**適用対象:** クラス、特にコレクション型。

**引数:** 外部<xref:System.Type>コンテンツのコンテンツ ラッパー型として使用する型を指定する A。

<xref:System.Windows.Markup.ContentWrapperAttribute>外部コンテンツのラップに使用される、関連付けられたコレクション型の 1 つ以上の型を指定します。 外部コンテンツとは、コンテンツ プロパティの型に対する型システムの制約が、所有する型の XAML の使用がサポートする可能性のあるコンテンツ ケースのすべてをキャプチャしない場合を指します。 たとえば、特定の型のコンテンツに対する XAML サポートは、厳密に型<xref:System.Collections.ObjectModel.Collection%601>指定されたジェネリック の文字列をサポートする場合があります。 コンテンツ ラッパーは、テキスト関連のコンテンツ モデルの移行など、既存のマークアップ規則を XAML のコレクションに割り当て可能な値の概念に移行する場合に役立ちます。

複数のコンテンツ ラッパー タイプを指定するには、属性を複数回適用します。

### <a name="dependsonattribute"></a>属性の指定

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.DependsOnAttribute>

**適用対象:** プロパティ

**引数:** 属性付き型の別のメンバーの名前を指定する文字列。

<xref:System.Windows.Markup.DependsOnAttribute>属性付きプロパティが別のプロパティの値に依存することを示します。 この属性をプロパティ定義に適用すると、XAML オブジェクトの書き込み時に、依存プロパティが最初に処理されるようになります。 の使用法<xref:System.Windows.Markup.DependsOnAttribute>は、有効なオブジェクトの作成のために解析の特定の順序に従う必要がある型のプロパティの例外的なケースを指定します。

プロパティ定義には複数<xref:System.Windows.Markup.DependsOnAttribute>のケースを適用できます。

### <a name="markupextensionreturntypeattribute"></a>プロパティの一種

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.MarkupExtensionReturnTypeAttribute>

**適用対象:**<xref:System.Windows.Markup.MarkupExtension>派生型であることが予想されるクラス。

**引数:** 属性<xref:System.Type>付`ProvideValue`<xref:System.Windows.Markup.MarkupExtension>きの結果として予想される最も正確な型を指定する A。

詳細については、「 [XAML の概要のマークアップ拡張機能](markup-extensions-overview.md)」を参照してください。

### <a name="namescopepropertyattribute"></a>プロパティ属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.NameScopePropertyAttribute>

**適用対象:** クラス

**引数:** アトリビューションの 2 つの形式をサポートします。

- 属性付き型のプロパティの名前を指定する文字列。

- プロパティの名前を指定する文字列と、名前付き<xref:System.Type>プロパティを定義する型のを指定する文字列。 このフォームは、XAML 名前スコープ プロパティとしてアタッチ可能なメンバーを指定するためのフォームです。

<xref:System.Windows.Markup.NameScopePropertyAttribute>属性付きクラスの XAML 名前スコープ値を提供するプロパティを指定します。 XAML 名前スコープ プロパティは、実際の XAML 名前<xref:System.Windows.Markup.INameScope>スコープ、ストア、および動作を実装し、保持するオブジェクトを参照する必要があります。

### <a name="runtimenamepropertyattribute"></a>プロパティ属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>

**適用対象:** クラス

**引数:** 属性付き型のランタイム名プロパティの名前を指定する文字列。

<xref:System.Windows.Markup.RuntimeNamePropertyAttribute>は、 XAML [x:Name ディレクティブ](xname-directive.md)にマップされる属性付き型のプロパティを報告します。 プロパティは、読み取<xref:System.String>り/書き込み可能である必要があります。

定義は、定義する型に割り当て可能なすべての派生型を継承します。 特定の派生型に適用することで、特定の派生型の<xref:System.Windows.Markup.RuntimeNamePropertyAttribute>定義をオーバーライドできます。

### <a name="trimsurroundingwhitespaceattribute"></a>トリム周辺空白属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>

**適用対象:** 種類

**引数:** なし。

<xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>は、空白の重要なコンテンツ (が含まれるコレクションによって保持されるコンテンツ) 内の子要素として表示<xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>される特定の型に適用されます。 <xref:System.Windows.Markup.TrimSurroundingWhitespaceAttribute>は主に保存パスに関連していますが、 を調べること<xref:System.Xaml.XamlType.TrimSurroundingWhitespace%2A?displayProperty=nameWithType>によって、ロード パスの XAML 型システムで使用できます。 詳細については、「 [XAML での空白の処理](white-space-processing.md)」を参照してください。

### <a name="typeconverterattribute"></a>TypeConverterAttribute

**リファレンス ドキュメント:**  <xref:System.ComponentModel.TypeConverterAttribute>

**適用対象:** クラス、プロパティ、メソッド (XAML で有効なメソッドの唯`get`一のケースは、アタッチ可能なメンバーをサポートするアクセサーです)。

**引数:** の<xref:System.Type>. <xref:System.ComponentModel.TypeConverter>

<xref:System.ComponentModel.TypeConverterAttribute>XAML コンテキストでカスタム<xref:System.ComponentModel.TypeConverter>を参照します。 これにより<xref:System.ComponentModel.TypeConverter>、カスタム型またはその型のメンバーに対する型変換動作が提供されます。

型コンバーター<xref:System.ComponentModel.TypeConverterAttribute>の実装を参照して、型に属性を適用します。 クラス、構造体、またはインターフェイスに XAML の型コンバーターを定義できます。 列挙型の型変換を提供する必要はありません。

型コンバーターは、マークアップ内の属性または初期化テキストに使用される文字列から目的の変換先の型に変換できる必要があります。 詳細については、「[型コンバーターと XAML](../../framework/wpf/advanced/typeconverters-and-xaml.md)」を参照してください。

型のすべての値に適用するのではなく、XAML の型コンバーターの動作を特定のプロパティに対して確立することもできます。 この場合、プロパティ定義<xref:System.ComponentModel.TypeConverterAttribute>(特定`get`の定義と`set`定義ではなく外側の定義) に適用されます。

カスタムアタッチ可能なメンバーの XAML 使用法の型コンバーターの動作は、XAML<xref:System.ComponentModel.TypeConverterAttribute>の`get`使用法をサポートするメソッド アクセサーに適用することで割り当てることができます。

と同様<xref:System.ComponentModel.TypeConverter>に<xref:System.ComponentModel.TypeConverterAttribute>、XAML が存在する前に .NET に存在し、型コンバーター モデルは他の目的を果たしました。 を参照して使用<xref:System.ComponentModel.TypeConverterAttribute>するには、完全に修飾するか、ステートメントを`using`提供する<xref:System.ComponentModel>必要があります。 プロジェクトにシステム アセンブリも含めます。

### <a name="uidpropertyattribute"></a>プロパティ属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.UidPropertyAttribute>

**適用対象:** クラス

**引数:** 関連するプロパティを名前で参照する文字列。

[x:Uid ディレクティブ](xuid-directive.md)をエイリアスするクラスの CLR プロパティを示します。

### <a name="usableduringinitializationattribute"></a>初期化中に使用できる属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.UsableDuringInitializationAttribute>

**適用対象:** クラス

**引数:** ブール値。 属性の目的に使用する場合は、値を に設定する`true`必要があります。

XAML オブジェクト グラフの作成時に型をトップダウンで構築するかどうかを示します。 これは高度な概念であり、おそらくプログラミング モデルの定義と密接に関連しています。 詳細については、「<xref:System.Windows.Markup.UsableDuringInitializationAttribute>」を参照してください。

### <a name="valueserializerattribute"></a>属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.ValueSerializerAttribute>

**適用対象:** クラス、プロパティ、メソッド (XAML で有効なメソッドの唯`get`一のケースは、アタッチ可能なメンバーをサポートするアクセサーです)。

**引数:** 属性<xref:System.Type>付き型のすべてのプロパティ、または特定の属性付きプロパティをシリアル化するときに使用する、値シリアライザー サポート クラスを指定する A。

<xref:System.Windows.Markup.ValueSerializer>は、より多くの状態とコンテキストを必要とする値の<xref:System.ComponentModel.TypeConverter>シリアル化クラスを指定します。 <xref:System.Windows.Markup.ValueSerializer>アタッチ可能なメンバーの静的<xref:System.Windows.Markup.ValueSerializerAttribute>`get`アクセサー メソッドに属性を適用することで、アタッチ可能なメンバーに関連付けることができます。 値のシリアル化は、列挙体、インターフェイス、および構造体にも適用できますが、デリゲートには適用できません。

### <a name="whitespacesignificantcollectionattribute"></a>クラス名の属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>

**適用対象:** クラス、特に、オブジェクト要素の周囲の空白が UI 表現にとって重要である場合に、混在したコンテンツをホストすることが期待されるコレクション型。

**引数:** なし。

<xref:System.Windows.Markup.WhitespaceSignificantCollectionAttribute>コレクション型は、コレクション内の XAML ノード ストリームの値ノードの構築に影響を与える XAML プロセッサによって重要な空白として処理する必要があることを示します。 詳細については、「 [XAML での空白の処理](white-space-processing.md)」を参照してください。

### <a name="xamldeferloadattribute"></a>属性を保留にします。

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.XamlDeferLoadAttribute>

**適用対象:** クラス、プロパティ。

**引数:** 2 つのアトリビューション フォーム型を文字列として、または<xref:System.Type>型としてサポートします。 [https://docs.microsoft.com/azure/active-directory/develop/scenario-protected-web-api-overview](<xref:System.Windows.Markup.XamlDeferLoadAttribute> ) をご覧ください。

クラスまたはプロパティに XAML の遅延読み込みの使用 (テンプレート動作など) が含まれていることを示し、遅延動作を有効にするクラスと、その宛先/コンテンツ タイプを報告します。

### <a name="xamlsetmarkupextensionattribute"></a>属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.XamlSetMarkupExtensionAttribute>

**適用対象:** クラス

**引数:** コールバックの名前を指定します。

クラスがマークアップ拡張機能を使用して 1 つ以上のプロパティの値を提供できることを示し、クラスの任意のプロパティに対してマークアップ拡張機能の設定操作を実行する前に XAML ライターが呼び出す必要があるハンドラーを参照します。

### <a name="xamlsettypeconverterattribute"></a>クラスの種類の属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.XamlSetTypeConverterAttribute>

**適用対象:** クラス

**引数:** コールバックの名前を指定します。

クラスが型コンバーターを使用して 1 つ以上のプロパティの値を提供できることを示し、クラスの任意のプロパティに対して型コンバーターのセット操作を実行する前に XAML ライターが呼び出す必要があるハンドラーを参照します。

### <a name="xmllangpropertyattribute"></a>プロパティ属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.XmlLangPropertyAttribute>

**適用対象:** クラス

**引数:** 属性付き型でエイリアス`xml:lang`するプロパティの名前を指定する文字列。

<xref:System.Windows.Markup.XmlLangPropertyAttribute>は、XML`lang`ディレクティブにマップされる属性付きの型のプロパティを報告します。 プロパティは必ずしも型<xref:System.String>ではありませんが、文字列から割り当て可能である必要があります (代入は、型コンバーターをプロパティの型に関連付けることによって行われるか、特定のプロパティに関連付けることによって行うことができます)。 プロパティは読み取り/書き込み可能である必要があります。

マッピング`xml:lang`のシナリオは、XMLDOM を使用して特別に処理することなく、ランタイム オブジェクト モデルが XML で指定された言語情報にアクセスできるようにすることです。

定義は、定義する型に割り当て可能なすべての派生型を継承します。 特定の派生型に適用することで<xref:System.Windows.Markup.XmlLangPropertyAttribute>、特定の派生型の定義をオーバーライドできますが、これは一般的なシナリオではありません。

## <a name="xaml-related-clr-attributes-at-the-assembly-level"></a>アセンブリ レベルでの XAML 関連の CLR 属性

次のセクションでは、型またはメンバー定義には適用されず、代わりにアセンブリに適用される XAML 関連の属性について説明します。 これらの属性は、XAML で使用するカスタム型を含むライブラリを定義するという全体的な目標に関連しています。 属性の一部は、必ずしも XAML ノード ストリームに直接影響を与えるわけではありませんが、他のコンシューマーが使用するためにノード ストリームに渡されます。 情報のコンシューマーには、XAML 名前空間情報と関連付けられたプレフィックス情報を必要とするデザイン環境やシリアル化プロセスが含まれます。 XAML スキーマ コンテキスト (.NET XAML サービスの既定値を含む) もこの情報を使用します。

### <a name="xmlnscompatiblewithattribute"></a>属性と互換性のある Xmlns

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute>

**引数:**

- 使用する XAML 名前空間の識別子を指定する文字列。

- 前の引数から XAML 名前空間を使用できる XAML 名前空間の識別子を指定する文字列。

  <xref:System.Windows.Markup.XmlnsCompatibleWithAttribute>XAML 名前空間を別の XAML 名前空間に含めることができることを指定します。 通常、包含する側の XAML 名前空間は、あらかじめ定義した <xref:System.Windows.Markup.XmlnsDefinitionAttribute> で示されます。 この方法は、ライブラリ内の XAML ボキャブラリのバージョン管理や、以前に定義されたマークアップと以前に定義されたバージョンのボキャブラリに対する互換性を持たせるために使用できます。

### <a name="xmlnsdefinitionattribute"></a>属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.XmlnsDefinitionAttribute>

**引数:**

- 定義する XAML 名前空間の識別子を指定する文字列。

- CLR 名前空間の名前を指定する文字列。 CLR 名前空間はアセンブリ内でパブリック型を定義する必要があり、少なくとも 1 つの CLR 名前空間型は XAML の使用を目的としている必要があります。

  <xref:System.Windows.Markup.XmlnsDefinitionAttribute>XAML 名前空間と CLR 名前空間の間のアセンブリごとにマッピングを指定します。

  アセンブリ<xref:System.Windows.Markup.XmlnsDefinitionAttribute>には複数の方法を適用できます。 これは、次の理由の任意の組み合わせで行われます。

- ライブラリ設計には、ランタイム API アクセスの論理編成用の複数の CLR 名前空間が含まれています。ただし、同じ XAML 名前空間を参照することで、これらの名前空間のすべての型を XAML で使用できるようにします。 この場合、同じ<xref:System.Windows.Markup.XmlnsDefinitionAttribute><xref:System.Windows.Markup.XmlnsDefinitionAttribute.XmlNamespace%2A>値を使用して異なる<xref:System.Windows.Markup.XmlnsDefinitionAttribute.ClrNamespace%2A>値を使用して複数の属性を適用します。 これは、フレームワークまたはアプリケーションが共通の使用法で既定の XAML 名前空間にする XAML 名前空間のマッピングを定義する場合に特に便利です。

- ライブラリデザインには複数の CLR 名前空間が含まれ、これらの CLR 名前空間での型の使用法を意図的に XAML 名前空間で分離する必要があります。

- アセンブリ内で CLR 名前空間を定義し、複数の XAML 名前空間を介してアクセスできるようにします。 このシナリオは、同じコードベースで複数のボキャブラリをサポートしている場合に発生します。

- 1 つ以上の CLR 名前空間で XAML 言語サポートを定義します。 この場合、値は<xref:System.Windows.Markup.XmlnsDefinitionAttribute.XmlNamespace%2A>にする`http://schemas.microsoft.com/winfx/2006/xaml`必要があります。

### <a name="xmlnsprefixattribute"></a>属性

**リファレンス ドキュメント:**  <xref:System.Windows.Markup.XmlnsPrefixAttribute>

**引数:**

- XAML 名前空間の識別子を指定する文字列。

- 推奨されるプレフィックスを指定する文字列。

  <xref:System.Windows.Markup.XmlnsDefinitionAttribute>XAML 名前空間に使用する推奨プレフィックスを指定します。 このプレフィックスは、.NET XAML サービス<xref:System.Xaml.XamlXmlWriter>によってシリアル化された XAML ファイルに要素と属性を書き込む場合、または XAML を実装するライブラリが XAML 編集機能を備えたデザイン環境と対話する場合に役立ちます。

  アセンブリ<xref:System.Windows.Markup.XmlnsPrefixAttribute>には複数の方法を適用できます。 これは、次の理由の任意の組み合わせで行われます。

- アセンブリでは、複数の XAML 名前空間の型を定義しています。 この場合は、XAML 名前空間ごとに異なるプレフィックス値を定義します。

- 複数のボキャブラリをサポートしており、各ボキャブラリと XAML 名前空間に異なるプレフィックスを使用します。

- アセンブリで XAML 言語サポートを定義し、 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> `http://schemas.microsoft.com/winfx/2006/xaml`の を持ちます。 この場合、通常はプレフィックス`x`を昇格させる必要があります。

> [!NOTE]
> .NET XAML サービスは、XAML 関連<xref:System.Windows.Markup.RootNamespaceAttribute>の属性も定義します。 この属性は、プロジェクト システムサポートのアセンブリ レベルの属性であり、XAML カスタム型には関係ありません。

## <a name="see-also"></a>関連項目

- <xref:System.Attribute>
- [.NET XAML サービスで使用するカスタム型の定義](define-custom-types.md)
