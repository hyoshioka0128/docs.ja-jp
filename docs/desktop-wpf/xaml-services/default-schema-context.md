---
title: 既定の XAML スキーマ コンテキストと WPF XAML スキーマ コンテキスト
ms.date: 03/30/2017
ms.assetid: 04e06a15-09b3-4210-9bdf-9a64c2eccb83
ms.openlocfilehash: 2e92372de61230a98a02282cc28fc3f479cd94eb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "81433080"
---
# <a name="default-xaml-schema-context-and-wpf-xaml-schema-context"></a>既定の XAML スキーマ コンテキストと WPF XAML スキーマ コンテキスト
XAML スキーマ コンテキストは、特定の XAML ボキャブラリを使用する XAML の運用環境がオブジェクトの書き込み動作とどのように相互作用するかを修飾する概念エンティティです。 このトピックでは、.NET XAML サービスの機能と、CLR 型システムに基づく関連する既定の XAML スキーマ コンテキストについて説明します。 このトピックでは、WPF で使用される XAML スキーマ コンテキストについても説明します。

## <a name="default-xaml-schema-context"></a>既定の XAML スキーマ コンテキスト

.NET XAML サービスは、既定の XAML スキーマ コンテキストを実装し、使用します。 既定の XAML スキーマ コンテキストの動作は、クラスの API<xref:System.Xaml.XamlSchemaContext>で常に完全に表示されるとは限りません。 ただし、多くの場合、既定の XAML スキーマ コンテキストが影響する動作は、XAML 型システムの共通 API (メンバー<xref:System.Xaml.XamlMember>や<xref:System.Xaml.XamlType>など) を通じて、または既定の XAML スキーマ コンテキストを使用する XAML リーダーや XAML ライターに公開された API を通じて観察できます。

コンストラクターを呼び<xref:System.Xaml.XamlSchemaContext>出すことによって、既定の動作をカプセル化<xref:System.Xaml.XamlSchemaContext>する を作成できます。 これにより、既定の XAML スキーマ コンテキストが明示的に作成されます。 入力パラメーターを明示的に受け取らない API を使用して XAML リーダーまたは XAML ライターを初期化した場合、同<xref:System.Xaml.XamlSchemaContext>じ既定の XAML スキーマ コンテキストが暗黙的に作成されます。

既定の XAML スキーマ コンテキストは、型マッピングの動作に CLR リフレクションを使用します。 これには、定義する CLR<xref:System.Type>と関連<xref:System.Reflection.PropertyInfo>する<xref:System.Reflection.MethodInfo>の検証が含まれます。 また、型またはメンバーに対する CLR 属性は、CLR バッキング型を使用する XAML 型または XAML メンバー情報の詳細を入力するために使用されます。 既定の XAML スキーマ コンテキストでは、`Invoker`必要な情報が CLR 型システムから取得できるため、パターンなどの型システム拡張手法は必要ありません。

アセンブリ読み込みロジックの場合、既定の XAML スキーマ コンテキストは、主に XAML 名前空間マッピングで提供されるアセンブリ値に依存します。 また、<xref:System.Xaml.XamlReaderSettings.LocalAssembly%2A>内部型の読み込みなどのシナリオで、読み込むアセンブリをヒントにすることもできます。

## <a name="wpf-xaml-schema-context"></a>WPF XAML スキーマ コンテキスト

WPF XAML スキーマ コンテキストは、WPF 実装が既定以外の XAML スキーマ コンテキストを実装することによって導入できる機能の種類の興味深い図を提供するため、このトピックで説明します。 また、XAML スキーマ コンテキストの概念は、WPF XAML に対応する WPF ドキュメントではあまり説明されていません。XAML スキーマ コンテキストで有効になる動作は、既定の XAML スキーマ コンテキストの動作に関する説明と統合されている場合にのみ、完全に理解できる可能性があります。 WPF XAML スキーマ コンテキストは、次の動作を実装します。

**ルックアップのオーバーライド:** WPF には、属性を持たずに機能する XAML コンテンツ プロパティがある<xref:System.Windows.Markup.ContentPropertyAttribute>XAML 用のコンテンツ モデルがいくつかあります。 <xref:System.Xaml.XamlType.LookupContentProperty%2A>WPF のオーバーライドは、この動作を実装します。

**WPF 式の遅延:** WPF には、ランタイム コンテキストが使用可能になるまで値を遅延する式クラスがいくつか用意されています。 また、テンプレートの展開は、遅延テクニックに依存する実行時の動作です。

**システムルックアップの最適化を入力します。** WPF には、数百の WPF 定義クラスを継承する基本クラス メンバー定義など、広範な XAML ボキャブラリとオブジェクト モデルがあります。 また、WPF 自体は複数のアセンブリに分散されます。 WPF では、参照テーブルやその他の手法を使用して、型の参照を最適化します。 これにより、既定の XAML スキーマ コンテキストと CLR ベースの型検索に対するパフォーマンスが向上します。 ルックアップ テーブルに型が存在しない場合、動作では既定の XAML スキーマ コンテキストに似た XAML スキーマ コンテキスト手法が使用されます。

**拡張機能と Xaml メンバー拡張機能:** WPF では、プロパティの概念を依存関係プロパティと、ルーティング イベントを使用したイベントの概念を拡張します。 これらの概念を XAML 処理操作に対してより<xref:System.Xaml.XamlType>詳細<xref:System.Xaml.XamlMember>に表示できるように、WPF は、依存関係プロパティとルーティング イベントの特性を報告する内部プロパティを拡張および追加します。

### <a name="accessing-the-wpf-xaml-schema-context"></a>WPF XAML スキーマ コンテキストへのアクセス

WPF<xref:System.Windows.Markup.XamlReader?displayProperty=nameWithType>または<xref:System.Windows.Markup.XamlWriter?displayProperty=nameWithType>に基づく XAML 手法を使用している場合、WPF XAML スキーマ コンテキストは、これらの XAML リーダーおよび XAML ライターの実装で既に使用されています。

WPF XAML スキーマ コンテキストで初期化されない他の XAML リーダーまたは XAML ライターの実装を使用している場合は、 から作業 WPF XAML<xref:System.Windows.Markup.XamlReader.GetWpfSchemaContext%2A?displayProperty=nameWithType>スキーマ コンテキストを取得できる場合があります。 この値は、<xref:System.Xaml.XamlSchemaContext>を使用する他の API の初期化として使用できます。 たとえば、初期化を呼び<xref:System.Xaml.XamlXmlReader.%23ctor%2A>出して、WPF XAML スキーマ コンテキストを渡すことができます。 または、XAML 型のシステム操作に WPF XAML スキーマ コンテキストを使用できます。 これには、<xref:System.Xaml.XamlType>または<xref:System.Xaml.XamlMember>の構築の初期化、または<xref:System.Xaml.XamlSchemaContext.GetXamlType%2A?displayProperty=nameWithType>呼び出しが含まれます。

純粋な XAML ノード ストリームの観点から WPF XAML の特定の側面にアクセスする場合、WPF フレームワーク機能の一部がまだ機能していない可能性があることに注意してください。 たとえば、コントロールの WPF テンプレートはまだ適用されていません。 したがって、実行時に完全なビジュアル ツリーが設定されるプロパティにアクセスすると、テンプレートを参照するプロパティ値のみが表示されることがあります。 WPF マークアップ拡張機能に提供されるサービス コンテキストは、ランタイム以外の状況から提供された場合は正確でない可能性があり、オブジェクト グラフを書き込もうとすると例外が発生する可能性があります。

## <a name="xaml-and-assembly-loading"></a>XAML とアセンブリの読み込み

XAML および .NET XAML サービスのアセンブリ読み込みは、 <xref:System.AppDomain>CLR で定義された概念の と統合されます。 XAML スキーマ コンテキストでは、アセンブリを読み込む方法、または実行時またはデザイン時に型を検索する方法を<xref:System.AppDomain>、その他の要因の使用に基づいて解釈します。 ロジックは、XAML が XAML リーダーの緩い XAML であるか、XAML が DLL`XamlBuildTask`にコンパイルされているか、WPF によって生成された BAML`PresentationBuildTask`であるかによって少し異なります。

WPF の XAML スキーマ コンテキストは、WPF アプリケーション モデルと統合<xref:System.AppDomain>され、WPF 実装の詳細である他の要素も使用されます。

#### <a name="xaml-reader-input-loose-xaml"></a>XAML リーダー入力 (緩い XAML)

01. XAML スキーマ コンテキストは、アプリケーション<xref:System.AppDomain>を反復処理し、最後に読み込まれたアセンブリから始まる名前のすべての側面に一致する既に読み込まれたアセンブリを検索します。 一致が見つかった場合、そのアセンブリは解決に使用されます。

02. それ以外の場合は、CLR <xref:System.Reflection.Assembly> API に基づく次のいずれかの手法を使用してアセンブリを読み込みます。

    - 名前がマッピングで修飾されている場合は、修飾<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>名を呼び出します。

    - 前の手順が失敗した場合は、短い名前 (および存在する場合は公開<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>キー トークン) を使用して を呼び出します。

    - マッピングで名前が修飾されていない場合は、 を<xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType>呼び出します。

#### <a name="xamlbuildtask"></a>XamlBuildTask

`XamlBuildTask`は、WCF (WCF) および Windows ワークフローファウンデーションで使用されます。

アセンブリ参照が常に`XamlBuildTask`完全に修飾されることに注意してください。

1. 修飾<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>名を呼び出します。

2. 前の手順が失敗した場合は、短い名前 (および存在する場合は公開<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>キー トークン) を使用して を呼び出します。

#### <a name="baml-presentationbuildtask"></a>バムラ (ビルドタスク)

BAML のアセンブリ読み込みには、BAML を含む初期アセンブリをコンポーネントとして読み込み、BAML プロダクションで参照される型の型バッキング アセンブリを読み込むという 2 つの側面があります。

##### <a name="assembly-load-for-initial-markup"></a>初期マークアップのアセンブリ読み込み:

マークアップを読み込むアセンブリへの参照は、常に修飾されない。

1. WPF XAML スキーマ コンテキストは、WPF アプリケーション<xref:System.AppDomain>を反復処理し、最後に読み込まれたアセンブリから始めて、名前のすべての側面に一致する既に読み込まれたアセンブリを検索します。 一致が見つかった場合、そのアセンブリは解決に使用されます。

2. 前の手順が失敗した場合は、短い名前 (および存在する場合は公開<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>キー トークン) を使用して を呼び出します。

##### <a name="assembly-references-by-baml-types"></a>BAML タイプによるアセンブリ参照:

BAML の生産で使用される型のアセンブリ参照は、ビルド タスクの出力として常に完全修飾されます。

01. WPF XAML スキーマ コンテキストは、WPF アプリケーション<xref:System.AppDomain>を反復処理し、最後に読み込まれたアセンブリから始めて、名前のすべての側面に一致する既に読み込まれたアセンブリを検索します。 一致が見つかった場合、そのアセンブリは解決に使用されます。

02. それ以外の場合は、次のいずれかの方法を使用してアセンブリを読み込みます。

    - 修飾<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>名を呼び出します。
  
    - 短い名前と公開キー トークンの組み合わせが BAML の読み込み元のアセンブリと一致する場合は、そのアセンブリを使用します。

    - 短縮名 + 公開鍵トークンを<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>使用して を呼び出す。

## <a name="see-also"></a>関連項目

- [XAML ノード ストリームの構造と概念について](understanding-xaml-node-stream-structures-and-concepts.md)
