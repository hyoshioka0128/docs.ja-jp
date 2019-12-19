---
title: XAML サービス
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], System.Xaml concepts
- XAML Services in WPF [XAML Services]
- System.Xaml [XAML Services], conceptual documentation
ms.assetid: 0e11f386-808c-4eae-9ba6-029ad7ba2211
ms.openlocfilehash: 8e1e8dc9a1410d05c19e4dd1bccb30c65d7c5e66
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74837286"
---
# <a name="xaml-services"></a>XAML サービス
このトピックでは、.NET Framework XAML サービスと呼ばれるテクノロジセットの機能について説明します。 説明されているサービスと Api の大部分は、アセンブリシステム .Xaml にあります。これは、.NET Framework 4 セットの .NET core アセンブリで導入されたアセンブリです。 サービスには、リーダーとライター、スキーマクラスとスキーマのサポート、ファクトリ、クラスの属性、XAML 言語の組み込みサポート、およびその他の XAML 言語機能が含まれます。  
  
## <a name="about-this-documentation"></a>このドキュメントについて  
 .NET Framework XAML サービスの概念ドキュメントでは、XAML 言語の以前の経験があること、および特定のフレームワーク ([!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] や Windows Workflow Foundation など) や特定のテクノロジ機能領域 (<xref:Microsoft.Build.Framework.XamlTypes>のビルドカスタマイズ機能など) にどのように適用されるかを前提としています。 このドキュメントでは、マークアップ言語、XAML 構文の用語、またはその他の入門資料としての XAML の基本については説明しません。 代わりに、このドキュメントでは、特に、システムの .Xaml アセンブリライブラリで有効になっている .NET Framework XAML サービスを使用する方法について説明します。 これらの Api のほとんどは、XAML 言語の統合と拡張性のシナリオに使用されます。 これには、次のいずれかが含まれます。  
  
- 基本 XAML リーダーまたは XAML ライターの機能を拡張する (XAML ノードストリームを直接処理する、独自の XAML リーダーまたは XAML ライターを派生させる)。  
  
- 特定のフレームワークの依存関係を持たない XAML 使用可能なカスタム型の定義、および xaml 型システムの特性を .NET Framework XAML サービスに伝えるための型の属性。  
  
- Xaml リーダーまたは xaml ライターをアプリケーションのコンポーネントとしてホストする (xaml マークアップソースのビジュアルデザイナーや対話型エディターなど)。  
  
- XAML 値コンバーター (マークアップ拡張機能、カスタム型の型コンバーター) の記述。  
  
- カスタム XAML スキーマコンテキストを定義する (バッキング型のソースに対して代替のアセンブリ読み込み手法を使用する、常にアセンブリを反映するのではなく、既知の型の参照手法を使用する、CLR `AppDomain` とそれに関連付けられているセキュリティモデルを使用しない、読み込まれたアセンブリの概念を使用する)。  
  
- 基本 XAML 型システムの拡張。  
  
- `Lookup` または `Invoker` 手法を使用した XAML 型システムへの影響、および型の戻り方の評価方法。  
  
 XAML の概要については、「 [xaml の概要 (WPF)」](../../desktop-wpf/fundamentals/xaml.md)を参照してください。 このトピックでは、[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] と xaml マークアップおよび XAML 言語機能を使用するための新しい対象ユーザー向けの XAML について説明します。 もう1つの便利なドキュメントは、 [XAML 言語仕様](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))の入門資料です。  
  
## <a name="net-framework-xaml-services-and-systemxaml-in-the-net-architecture"></a>.NET アーキテクチャでの XAML サービスと app.xaml の .NET Framework  
 以前のバージョンの Microsoft .NET Framework では、XAML 言語機能のサポートは Microsoft .NET フレームワーク ([!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]、Windows Workflow Foundation および Windows Communication Foundation (WCF)) 上に構築されたフレームワークによって実装されていました。そのため、使用している特定のフレームワークに応じて、動作と API が変化します。 これには、XAML パーサーとそのオブジェクトグラフの作成機構、XAML 言語の組み込み、シリアル化のサポートなどが含まれます。  
  
 .NET Framework 4 では、.NET Framework xaml サービスと、xaml 言語機能をサポートするために必要なものの多くが定義されています。 これには、XAML リーダーと XAML ライターの基本クラスが含まれます。 フレームワーク固有の XAML 実装に含まれていなかった .NET Framework XAML サービスに追加された最も重要な機能は、XAML の型システム表現です。 型システム表現は、フレームワークの特定の機能に依存することなく XAML 機能を中心としたオブジェクト指向の方法で XAML を表します。  
  
 XAML 型システムは、マークアップフォームや、XAML オリジンの実行時の仕様によって制限されません。また、特定のバッキング型システムによって制限されることもありません。 XAML 型システムには、型、メンバー、XAML スキーマコンテキスト、XML レベルの概念、およびその他の XAML 言語の概念や XAML の組み込みに対するオブジェクト表現が含まれています。 Xaml 型システムを使用または拡張することにより、xaml リーダーや XAML ライターなどのクラスから派生させ、フレームワーク、テクノロジ、またはを使用するアプリケーションや、またはを使用するアプリケーションによって実現される特定の機能に XAML 表現の機能を拡張できます。XAML を生成します。 Xaml スキーマコンテキストの概念を使用すると、XAML オブジェクトライターの実装、テクノロジのバッキング型システム、コンテキスト内のアセンブリ情報を通じて伝達される、XAML ノードの組み合わせから、実用的なオブジェクトグラフの書き込み操作を行うことができます。電源. XAML スキーマの概念の詳細については、「」を参照してください。 「[既定の Xaml スキーマコンテキスト」と「WPF XAML スキーマコンテキスト」を](default-xaml-schema-context-and-wpf-xaml-schema-context.md)参照してください。  
  
## <a name="xaml-node-streams-xaml-readers-and-xaml-writers"></a>XAML ノードストリーム、XAML リーダー、および XAML ライター  
 Xaml 言語と xaml を言語として使用する特定のテクノロジとの間の関係で XAML サービスが果たす .NET Framework 役割について理解するには、XAML ノードストリームの概念と、その概念によって API がどのように整形されるかを理解しておくことをお勧めします。関する. Xaml ノードストリームは、xaml 言語表現と、XAML が表すまたは定義するオブジェクトグラフとの間の中間概念です。  
  
- XAML リーダーは、何らかの形式で XAML を処理し、XAML ノードストリームを生成するエンティティです。 API では、XAML リーダーは <xref:System.Xaml.XamlReader>基本クラスによって表されます。  
  
- XAML ライターは、XAML ノードストリームを処理して他のものを生成するエンティティです。 API では、XAML ライターは <xref:System.Xaml.XamlWriter>基本クラスによって表されます。  
  
 XAML に関連する最も一般的な2つのシナリオは、オブジェクトグラフをインスタンス化するための XAML の読み込みと、アプリケーションまたはツールからのオブジェクトグラフの保存、および XAML 表現の生成 (通常はテキストファイルとして保存されたマークアップ形式) です。 XAML の読み込みとオブジェクトグラフの作成は、多くの場合、読み込みパスとしてこのドキュメントで参照されます。 既存のオブジェクトグラフを XAML に保存またはシリアル化することは、このドキュメントでは通常、保存パスと呼ばれます。  
  
 最も一般的な読み込みパスの種類は、次のように記述できます。  
  
- XAML 表現から、UTF エンコードされた XML 形式で開始し、テキストファイルとして保存します。  
  
- XAML を <xref:System.Xaml.XamlXmlReader>に読み込みます。 <xref:System.Xaml.XamlXmlReader> は <xref:System.Xaml.XamlReader> サブクラスです。  
  
- その結果、XAML ノードストリームが生成されます。 XAML ノードストリームの個々のノードには、<xref:System.Xaml.XamlXmlReader> / <xref:System.Xaml.XamlReader> API を使用してアクセスできます。 ここでの最も一般的な操作は、XAML ノードストリームを進め、"現在のレコード" の比喩を使用して各ノードを処理することです。  
  
- 生成されたノードを XAML ノードストリームから <xref:System.Xaml.XamlObjectWriter> API に渡します。 <xref:System.Xaml.XamlObjectWriter> は <xref:System.Xaml.XamlWriter> サブクラスです。  
  
- <xref:System.Xaml.XamlObjectWriter> は、ソース XAML ノードストリームの進行に従って、オブジェクトグラフを一度に1つずつ書き込みます。 これは、XAML スキーマコンテキストと、バッキング型システムおよびフレームワークのアセンブリおよび型にアクセスできる実装によって行われます。  
  
- XAML ノードストリームの末尾で <xref:System.Xaml.XamlObjectWriter.Result%2A> を呼び出して、オブジェクトグラフのルートオブジェクトを取得します。  
  
 最も一般的な保存パスの種類は、次のように記述できます。  
  
- アプリケーションの実行時間全体のオブジェクトグラフ、実行時の UI コンテンツと状態、または実行時のアプリケーションのオブジェクト表現全体の小さなセグメントを使用して開始します。  
  
- アプリケーションルートやドキュメントルートなどの論理開始オブジェクトから、オブジェクトを <xref:System.Xaml.XamlObjectReader>に読み込みます。 <xref:System.Xaml.XamlObjectReader> は <xref:System.Xaml.XamlReader> サブクラスです。  
  
- その結果、XAML ノードストリームが生成されます。 XAML ノードストリームの個々のノードには、<xref:System.Xaml.XamlObjectReader> と <xref:System.Xaml.XamlReader> API を使用してアクセスできます。 ここでの最も一般的な操作は、XAML ノードストリームを進め、"現在のレコード" の比喩を使用して各ノードを処理することです。  
  
- 生成されたノードを XAML ノードストリームから <xref:System.Xaml.XamlXmlWriter> API に渡します。 <xref:System.Xaml.XamlXmlWriter> は <xref:System.Xaml.XamlWriter> サブクラスです。  
  
- <xref:System.Xaml.XamlXmlWriter> は、XAML を XML UTF エンコーディングで書き込みます。 これは、テキストファイル、ストリーム、または他の形式で保存できます。  
  
- <xref:System.Xaml.XamlXmlWriter.Flush%2A> を呼び出して、最終的な出力を取得します。  
  
 XAML ノード ストリームの概念の詳細については、「[XAML ノード ストリームの構造と概念について](understanding-xaml-node-stream-structures-and-concepts.md)」を参照してください。  
  
### <a name="the-xamlservices-class"></a>XamlServices クラス  
 XAML ノードストリームを処理する必要は必ずしも必要ではありません。 基本的な読み込みパスまたは基本的な保存パスが必要な場合は、<xref:System.Xaml.XamlServices> クラスで Api を使用できます。  
  
- <xref:System.Xaml.XamlServices.Load%2A> のさまざまなシグネチャは、読み込みパスを実装します。 ファイルまたはストリームを読み込むことも、<xref:System.Xml.XmlReader>、<xref:System.IO.TextReader>、またはそのリーダーの Api を使用して読み込むことによって XAML 入力をラップする <xref:System.Xaml.XamlReader> を読み込むこともできます。  
  
- オブジェクトグラフを保存し、ストリーム、ファイル、または <xref:System.Xml.XmlWriter>/<xref:System.IO.TextWriter> インスタンスとして出力を生成 <xref:System.Xaml.XamlServices.Save%2A> のさまざまなシグネチャ。  
  
- <xref:System.Xaml.XamlServices.Transform%2A> は、読み込みパスと保存パスを1つの操作としてリンクすることによって、XAML を変換します。 異なるスキーマコンテキストまたは異なるバッキング型システムを <xref:System.Xaml.XamlReader> および <xref:System.Xaml.XamlWriter>に使用できます。これは、結果として得られる XAML の変換方法に影響します。  
  
 <xref:System.Xaml.XamlServices>の使用方法の詳細については、「 [Xamlservices クラス」と「基本的な XAML の読み取りと書き込み](xamlservices-class-and-basic-xaml-reading-or-writing.md)」を参照してください。  
  
## <a name="xaml-type-system"></a>XAML 型システム  
 Xaml 型システムには、XAML ノードストリームの特定のノードを操作するために必要な Api が用意されています。  
  
 <xref:System.Xaml.XamlType> はオブジェクトの表現で、[開始オブジェクト] ノードと [オブジェクトの終了] ノードの間で処理されます。  
  
 <xref:System.Xaml.XamlMember> は、オブジェクトのメンバーの表現です。開始メンバーノードと終了メンバーノードの間で処理されます。  
  
 <xref:System.Xaml.XamlType.GetAllMembers%2A> や <xref:System.Xaml.XamlType.GetMember%2A> <xref:System.Xaml.XamlMember.DeclaringType%2A> などの Api は、<xref:System.Xaml.XamlType> と <xref:System.Xaml.XamlMember>間のリレーションシップを報告します。  
  
 .NET Framework XAML サービスによって実装される XAML 型システムの既定の動作は、共通言語ランタイム (CLR) と、リフレクションを使用したアセンブリ内の CLR 型のスタティック分析に基づいています。 したがって、特定の CLR 型について、XAML 型システムの既定の実装では、その型とそのメンバーの XAML スキーマを公開し、XAML 型システムの観点からレポートすることができます。 既定の XAML 型システムでは、型の割り当て機能の概念が CLR 継承にマップされます。また、インスタンスの概念、値型なども CLR のサポートする動作と機能にマップされます。  
  
## <a name="reference-for-xaml-language-features"></a>XAML 言語機能のリファレンス  
 Xaml をサポートするために、xaml 言語の XAML 名前空間に対して定義されている xaml 言語の概念の特定の実装を .NET Framework XAML サービスに提供します。 これらは、特定の参照ページとして記載されています。 言語機能は、xaml リーダーまたは .NET Framework XAML サービスによって定義された xaml ライターによって処理されるときに、これらの言語機能がどのように動作するかについての観点から説明されています。 詳細については、「 [XAML Namespace (x:) Language Features](xaml-namespace-x-language-features.md)」を参照してください。
