---
title: .NET XAML サービスの XAML 名前空間
ms.date: 03/30/2017
ms.assetid: e4f15f13-c420-4c1e-aeab-9b6f50212047
ms.openlocfilehash: 2ae57d08fade85c59fea2a54b653a2f775b57415
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "81433062"
---
# <a name="xaml-namespaces-for-net-xaml-services"></a>.NET XAML サービスの XAML 名前空間
XAML 名前空間は、XML 名前空間の定義を拡張する概念です。 XML 名前空間と同様に、マークアップの属性を使用して`xmlns`XAML 名前空間を定義できます。 XAML 名前空間は、XAML ノード ストリームおよびその他の XAML サービス API でも表されます。 このトピックでは、XAML 名前空間の概念を定義し、XAML 名前空間を定義し、XAML スキーマ コンテキストと .NET XAML サービスの他の側面で使用する方法について説明します。  
  
## <a name="xml-namespace-and-xaml-namespace"></a>XML 名前空間と XAML 名前空間  
 XAML 名前空間は特殊な XML 名前空間であり、XAML は特殊な形式の XML であり、マークアップに基本的な XML フォームを使用します。 マークアップでは、XAML 名前空間と、要素に適用される属性`xmlns`を通じて XAML 名前空間とそのマッピングを宣言します。 宣言`xmlns`は、XAML 名前空間が宣言されているのと同じ要素に対して行うことができます。 要素に対して行われた XAML 名前空間宣言は、その要素、その要素のすべての属性、およびその要素のすべての子に対して有効です。 属性名自体がマークアップの属性名の一部としてプレフィックスを参照している限り、属性は、属性を含む要素とは別の XAML 名前空間を使用できます。  
  
 XAML 名前空間と XML 名前空間の違いは、XML 名前空間を使用してスキーマを参照したり、エンティティを区別したりすることです。 XAML では、XAML で使用される型とメンバーは、最終的にはバッキング型に解決する必要があり、XML スキーマの概念はこの機能に適していません。 XAML 名前空間には、この型マッピングを実行するために XAML スキーマ コンテキストが使用可能である必要がある情報が含まれています。  
  
## <a name="xaml-namespace-components"></a>XAML 名前空間コンポーネント  
 XAML 名前空間定義には、プレフィックスと識別子の 2 つのコンポーネントがあります。 これらの各コンポーネントは、XAML 名前空間がマークアップで宣言されるか、XAML 型システムで定義されている場合に存在します。  
  
 プレフィックスは[、XML 1.0 仕様の W3C 名前空間で](https://www.w3.org/TR/REC-xml-names/)許可されている任意の文字列にすることができます。 通常、プレフィックスは一般的なマークアップ ファイルで繰り返されるため、プレフィックスは短い文字列です。 複数の XAML 実装で使用する特定の XAML 名前空間は、特定の従来のプレフィックスを使用します。 たとえば、XAML 言語の XAML 名前空間は、通常はプレフィックス`x`を使用してマップされます。 by.NET 既定の XAML 名前空間を定義できます。 通常、既定の XAML 名前空間は、XAML 実装テクノロジとそのシナリオとボキャブラリによって、プレフィックス省略マークアップの最大化を促進するために意図的に選択されます。  
  
 この識別子は[、XML 1.0 仕様の W3C 名前空間で](https://www.w3.org/TR/REC-xml-names/)許可されている任意の文字列にすることができます。 慣例により、XML 名前空間または XAML 名前空間の識別子は、通常はプロトコルで修飾された絶対 URI として URI 形式で指定されます。 多くの場合、特定の XAML ボキャブラリを定義するバージョン情報はパス文字列の一部として暗黙的に示されます。 XAML 名前空間は、XML URI 規則を超えた追加の識別子規則を追加します。 XAML 名前空間の識別子は、XAML 名前空間の要素として指定された型を解決するために、またはメンバーに属性を解決するために、XAML スキーマ コンテキストで必要な情報を通信します。  
  
 XAML スキーマ コンテキストに情報を伝達するために、XAML 名前空間の識別子は URI 形式のままになる場合があります。 ただし、この場合、URI は特定のアセンブリまたはアセンブリのリストで一致する識別子としても宣言されます。 これは、アセンブリにを帰属させることによってアセンブリで<xref:System.Windows.Markup.XmlnsDefinitionAttribute>行われます。 この方法は、XAML 名前空間を識別し、属性付きアセンブリで CLR ベースの型解決動作をサポートします。 より一般的には、この規則は、XAML スキーマ コンテキストが CLR を組み込む場合や、CLR アセンブリから CLR 属性を読み取るために必要な既定の XAML スキーマ コンテキストに基づいている場合に使用できます。  
  
 XAML 名前空間は、CLR 名前空間と型定義アセンブリを通信する規則によっても識別できます。 この規則は、型を含む<xref:System.Windows.Markup.XmlnsDefinitionAttribute>アセンブリにアトリビューションが存在しない場合に使用されます。 この規則は URI の規則よりも複雑になる可能性があり、アセンブリを参照する方法が複数あるため、あいまいさと重複の可能性もあります。  
  
 CLR 名前空間とアセンブリの規則を使用する識別子の最も基本的な形式は次のとおりです。  
  
 `clr-namespace:clrnsName; assembly=assemblyShortName`
  
 `clr-namespace:`構文`; assembly=`のリテラル コンポーネントです。  
  
 *clrnsName*は、CLR 名前空間を識別する文字列名です。 この文字列名には、CLR 名前空間と他の CLR 名前空間との関係に関するヒントを提供する内部ドット文字 (.) が含まれます。
  
 *アセンブリの文字列名*は、XAML で役立つ型を定義するアセンブリの文字列名です。 宣言された XAML 名前空間を通じてアクセスされる型は、アセンブリによって定義され *、clrnsName*で指定された CLR 名前空間内で宣言される必要があります。 この文字列名は通常、 によって報告される情報<xref:System.Reflection.AssemblyName.Name%2A?displayProperty=nameWithType>と並行して行われます。  
  
 CLR 名前空間とアセンブリの規則のより完全な定義は次のとおりです。  
  
 `clr-namespace:clrnsName; assembly=assemblyName`
  
 *assemblyName*は、入力として有効な文字列<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType>を表します。 この文字列には、カルチャ、公開キー、またはバージョン情報を含めることができます ( これらの概念の定義は<xref:System.Reflection.Assembly>、 のリファレンス トピックで定義されています)。 COFF 形式と証拠 ( の他のオーバーロード<xref:System.Reflection.Assembly.Load%2A>で使用される ) は、XAML アセンブリの読み込み目的には関係ありません。すべてのロード情報は文字列として表示する必要があります。  
  
 アセンブリの公開キーを指定することは、XAML セキュリティの場合や、アセンブリが単純名で読み込まれる場合、またはキャッシュまたはアプリケーション ドメインに事前に存在する場合に存在する可能性のあるあいまいさを取り除く場合に便利な手法です。 詳細については、「 [XAML のセキュリティに関する考慮事項](security-considerations.md)」を参照してください。  
  
## <a name="xaml-namespace-declarations-in-the-xaml-services-api"></a>XAML サービス API での XAML 名前空間宣言  
 XAML サービス API では、XAML 名前空間宣言は<xref:System.Xaml.NamespaceDeclaration>オブジェクトによって表されます。 コードで XAML 名前空間を宣言する場合は、コンストラクター<xref:System.Xaml.NamespaceDeclaration.%23ctor%28System.String%2CSystem.String%29>を呼び出します。 パラメーター`ns`と`prefix`パラメーターは文字列として指定され、これらのパラメーターに提供する入力は、このトピックで前述したように XAML 名前空間識別子と XAML 名前空間プレフィックスの定義に対応します。  
  
 XAML 名前空間情報を XAML ノード ストリームの一部として、または XAML 型システムへの他<xref:System.Xaml.NamespaceDeclaration.Namespace%2A?displayProperty=nameWithType>のアクセスを通じて調べる<xref:System.Xaml.NamespaceDeclaration.Prefix%2A?displayProperty=nameWithType>場合は、XAML 名前空間識別子を報告し、XAML 名前空間プレフィックスを報告します。  
  
 XAML ノード ストリームでは、XAML 名前空間情報は、XAML ノードが適用されるエンティティの前に XAML ノードとして表示されます。 これには、XAML 名前空間情報が XAML ルート`StartObject`要素の前にある場合も含まれます。 詳細については、「 [Understanding XAML Node Stream Structures and Concepts](understanding-xaml-node-stream-structures-and-concepts.md)」を参照してください。  
  
 NET XAML サービス API を使用する多くのシナリオでは、少なくとも 1 つの XAML 名前空間宣言が存在することが予期され、宣言には XAML スキーマ コンテキストで必要な情報が含まれているか、または参照する必要があります。 XAML 名前空間は、読み込まれるアセンブリを指定するか、または既に読み込まれているか、XAML スキーマ コンテキストによって既知の名前空間およびアセンブリ内の特定の型を解決する際に役立つ必要があります。  
  
 XAML ノード ストリームを生成するには、XAML スキーマ コンテキストを通じて XAML 型情報を使用できる必要があります。 作成する各ノードに関連する XAML 名前空間を最初に決定しないと、XAML 型情報を特定できません。 この時点では、型のインスタンスはまだ作成されていませんが、XAML スキーマ コンテキストは、定義するアセンブリとバッキングの種類から情報を検索する必要があります。 たとえば`<Party><PartyFavor/></Party>`、 マークアップ を処理するには、 XAML スキーマ コンテキストが の名前と型`ContentProperty``Party`を決定でき、そのため、`Party`および`PartyFavor`の XAML 名前空間情報も知っている必要があります。 既定の XAML スキーマ コンテキストの場合、静的リフレクションは、ノード ストリームで XAML 型ノードを生成するために必要な XAML 型システム情報の多くを報告します。  
  
 XAML ノード ストリームからオブジェクト グラフを生成するには、元のマークアップで使用され、XAML ノード ストリームに記録された各 XAML プレフィックスに XAML 名前空間宣言が存在する必要があります。 この時点で、インスタンスが作成され、実際の型マッピング動作が発生します。  
  
 XAML 名前空間情報を事前に設定する必要がある場合、XAML スキーマ コンテキストを使用する XAML 名前空間がマークアップで定義されていない場合は、 で XML 名前空間宣言を<xref:System.Xml.XmlParserContext>宣言する方法の 1<xref:System.Xml.XmlReader>つが、 で使用できます。 次に、XAML<xref:System.Xml.XmlReader>リーダー コンストラクターの入力として使用<xref:System.Xaml.XamlServices.Load%28System.Xml.XmlReader%29?displayProperty=nameWithType>します。  
  
 .NET XAML サービスでの XAML 名前空間の処理に関連する他の<xref:System.Windows.Markup.XmlnsDefinitionAttribute>2<xref:System.Windows.Markup.XmlnsPrefixAttribute>つの API は、属性と . これらの属性は、アセンブリに適用されます。 <xref:System.Windows.Markup.XmlnsDefinitionAttribute>は、URI を含む XAML 名前空間宣言を解釈するために XAML スキーマ コンテキストによって使用されます。 <xref:System.Windows.Markup.XmlnsPrefixAttribute>は、特定の XAML 名前空間を予測可能なプレフィックスでシリアル化できるように、XAML を出力するツールによって使用されます。 詳細については、「[カスタム型とライブラリの XAML 関連 CLR 属性](clr-attributes-with-custom-types-and-libraries.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [XAML ノード ストリームの構造と概念について](understanding-xaml-node-stream-structures-and-concepts.md)
