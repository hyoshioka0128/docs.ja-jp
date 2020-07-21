---
title: XAML サービス
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], System.Xaml concepts
- XAML Services in WPF [XAML Services]
- System.Xaml [XAML Services], conceptual documentation
ms.assetid: 0e11f386-808c-4eae-9ba6-029ad7ba2211
ms.openlocfilehash: bfb3efb479668bcd70a3ce87b80253a73c18bb51
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "85840371"
---
# <a name="xaml-services"></a>XAML サービス

このトピックでは、.NET XAML サービスと呼ばれるテクノロジ セットの機能について説明します。 説明するサービスと API の大部分は、アセンブリ `System.Xaml`内にあります。 サービスには、リーダーとライター、スキーマ クラスとスキーマ サポート、ファクトリ、クラスの属性、XAML 言語の組み込みサポート、およびその他の XAML 言語機能が含まれます。

## <a name="about-this-documentation"></a>このドキュメントについて

.NET XAML サービスの概念に関するドキュメントでは、XAML 言語について、さらに、それを特定のフレームワーク (Windows Presentation Foundation (WPF) や Windows Workflow Foundation など) または特定のテクノロジ機能領域 (<xref:Microsoft.Build.Framework.XamlTypes> のビルド カスタマイズ機能など) に適用する方法について以前に経験があることを前提としています。 このドキュメントは、マークアップ言語としての XAML の基本、XAML 構文の用語、またはその他の入門的な内容について説明を試みるものではありません。 代わりに、このドキュメントでは、特に System.Xaml アセンブリ ライブラリ内で有効になっている .NET XAML サービスの使用方法を重点的に説明します。 これらの API のほとんどは、XAML 言語の統合と拡張性のシナリオで使用されます。 それには、次のようなシナリオがあります。

- ベースの XAML リーダーまたは XAML ライターの機能を拡張する (XAML ノード ストリームを直接処理する。独自の XAML リーダーまたは XAML ライターを派生させる)。

- 特定のフレームワーク依存関係を持たない、XAML で使用可能なカスタム型を定義し、その型を属性化することで XAML 型のシステム特性を .NET XAML サービスに伝達する

- XAML マークアップ ソース用のビジュアル デザイナーやインタラクティブ エディターなどのアプリケーションのコンポーネントとして XAML リーダーまたは XAML ライターをホストする。

- XAML 値コンバーターを記述する (マークアップ拡張機能、カスタム型用の型コンバーター)。

- カスタム XAML スキーマ コンテキストを定義する (バッキング型ソースに対して代替のアセンブリ読み込み手法を使用する。常にアセンブリを反映するわけではなく、既知の型の参照手法を使用する。共通言語ランタイム (CLR) `AppDomain` とそれに関連付けられたセキュリティ モデルを使用しない、読み込まれたアセンブリの概念を使用する)。

- 基本の XAML 型システムを拡張する。

- XAML 型システムに、および型バッキングの評価方法に影響を与える`Lookup` または `Invoker` 手法を使用する。

言語としての XAML に関する入門資料をお探しの場合は、[XAML の概要 (WPF)](../fundamentals/xaml.md)に関するページを参照してみてください。 そのトピックでは、Windows Presentation Foundation (WPF) にも、XAML マークアップおよび XAML 言語機能の使い方にも初心者である対象ユーザー向けに XAML が説明されています。 その他にも有用なドキュメントとして、[XAML 言語仕様](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))内の入門資料があります。

## <a name="net-xaml-services-and-systemxaml-in-the-net-architecture"></a>.NET アーキテクチャでの .NET XAML サービスと `System.Xaml`

.NET XAML サービスと `System.Xaml` アセンブリでは、XAML 言語機能をサポートするために必要な多くのものが定義されます。 これには、XAML リーダーと XAML ライターの基底クラスが含まれます。 .NET XAML サービスに追加された最も重要な機能は XAML 用の型システム表現であり、これはフレームワーク固有の XAML 実装のいずれにも存在していませんでした。 型システム表現では、フレームワークの特定の機能に依存することなく XAML 機能を中心としたオブジェクト指向の方法で XAML が表されます。

XAML 型システムは、XAML オリジンのマークアップ フォームまたはランタイム仕様によって制限されることもなければ、特定のバッキング型システムによって制限されることもありません。 XAML 型システムには、型、メンバー、XAML スキーマ コンテキスト、XML レベルの概念、およびその他の XAML 言語の概念または XAML の組み込みに関するオブジェクト表現が含まれています。 XAML 型システムを使用または拡張すれば、XMAL リーダーや XAML ライターなどのクラスから派生させ、フレームワーク、テクノロジ、または XAML を使用または生成するアプリケーションによって有効にされる特定の機能に、XAML 表現の機能を拡張できます。 XAML スキーマ コンテキストの概念では、XAML オブジェクト ライターの実装と、コンテキスト内のアセンブリ情報を介して通信されるテクノロジのバッキング型システムと、XAML ノード ソースとの組み合わせから、実用的なオブジェクト グラフ書き込み操作が可能になります。 XAML スキーマの概念の詳細については、 「[既定の XAML スキーマ コンテキストと WPF XAML スキーマ コンテキスト](default-schema-context.md)」を参照してください。

## <a name="xaml-node-streams-xaml-readers-and-xaml-writers"></a>XAML ノード ストリーム、XAML リーダー、および XAML ライター

XAML 言語と、XAML を言語として使用する特定のテクノロジとのリレーションシップで .NET XAML サービスが果たす役割を理解するには、XAML ノード ストリームの概念について、さらにその概念によって API と用語をどのように形成されるかについて理解することが有効です。 XAML ノード ストリームは、XAML 言語表現と、XAML で表現または定義されるオブジェクト グラフとの間の概念的な中間体です。

- XAML リーダーは、何らかの形式で XAML を処理し、XAML ノード ストリームを生成するエンティティです。 API では、XAML リーダーは基底クラス <xref:System.Xaml.XamlReader> によって表されます。

- XAML ライターは、XAML ノード ストリームを処理して他のものを生成するエンティティです。 API では、XAML ライターは基底クラス <xref:System.Xaml.XamlWriter> によって表されます。

  XAML を必要とする最も一般的な 2 つのシナリオは、XAML を読み込んでオブジェクト グラフをインスタンス化するというものと、アプリケーションまたはツールからのオブジェクト グラフを保存して XAML 表現を生成するというものです (通常はテキスト ファイルとして保存されるマークアップ形式)。 XAML の読み込みとオブジェクト グラフの作成は、このドキュメントではしばしば読み込みパスと呼ばれます。 既存のオブジェクト グラフを XAML に保存またはシリアル化することは、このドキュメントではしばしば保存パスと呼ばれます。

  最も一般的な型の読み込みパスは、次のように記述できます。

- XAML 表現から開始し (UTF でエンコードされた XML 形式)、テキスト ファイルとして保存します。

- その XAML を <xref:System.Xaml.XamlXmlReader> に読み込みます。 <xref:System.Xaml.XamlXmlReader> は <xref:System.Xaml.XamlReader> サブクラスです。

- 結果は XAML ノード ストリームです。 XAML ノード ストリームの個々のノードには、<xref:System.Xaml.XamlXmlReader> / <xref:System.Xaml.XamlReader> API を使用してアクセスできます。 ここでの最も代表的な操作は、XAML ノード ストリームを進め、"現在のレコード" のメタファーを使用して各ノードを処理することです。

- 生成されたノードを XAML ノード ストリームから <xref:System.Xaml.XamlObjectWriter> API に渡します。 <xref:System.Xaml.XamlObjectWriter> は <xref:System.Xaml.XamlWriter> サブクラスです。

- <xref:System.Xaml.XamlObjectWriter> では、ソース XAML ノード ストリームの進行状況に従って、オブジェクト グラフが書き込まれます (一度に 1 つのオブジェクト)。 オブジェクトの作成は、XAML スキーマ コンテキストと、バッキング型システムおよびフレームワークのアセンブリおよび型にアクセスできる実装とによって行われます。

- XAML ノード ストリームの末尾で <xref:System.Xaml.XamlObjectWriter.Result%2A> を呼び出して、オブジェクト グラフのルート オブジェクトを取得します。

  最も一般的な型の保存パスは、次のように記述できます。

- まずは、アプリケーション実行時全体のオブジェクト グラフ、実行時の UI コンテンツと状態、または実行時のアプリケーションのオブジェクト表現全体のより小さなセグメントから始めます。

- アプリケーション ルートやドキュメント ルートなどの論理開始オブジェクトから、オブジェクトを <xref:System.Xaml.XamlObjectReader> に読み込みます。 <xref:System.Xaml.XamlObjectReader> は <xref:System.Xaml.XamlReader> サブクラスです。

- 結果は XAML ノード ストリームです。 <xref:System.Xaml.XamlObjectReader> および <xref:System.Xaml.XamlReader> API を使用すれば、XAML ノード ストリームの個々のノードにアクセスできます。 ここでの最も代表的な操作は、XAML ノード ストリームを進め、"現在のレコード" のメタファーを使用して各ノードを処理することです。

- 生成されたノードを XAML ノード ストリームから <xref:System.Xaml.XamlXmlWriter> API に渡します。 <xref:System.Xaml.XamlXmlWriter> は <xref:System.Xaml.XamlWriter> サブクラスです。

- <xref:System.Xaml.XamlXmlWriter> では、XAML が XML UTF エンコードで書き込まれます。 これは、テキスト ファイルまたはストリームとして、あるいは他の形式で保存できます。

- <xref:System.Xaml.XamlXmlWriter.Flush%2A> を呼び出して、最終的な出力を取得します。

XAML ノード ストリームの概念の詳細については、「[XAML ノード ストリームの構造と概念について](understanding-xaml-node-stream-structures-and-concepts.md)」を参照してください。

### <a name="the-xamlservices-class"></a>XamlServices クラス

XAML ノード ストリームを処理する必要は必ずしもありません。 基本的な読み込みパスまたは基本的な保存パスが必要な場合は、<xref:System.Xaml.XamlServices> クラスの API を使用できます。

- 読み込みパスは、<xref:System.Xaml.XamlServices.Load%2A> のさまざまなシグネチャによって実装されます。 ファイルまたはストリームを読み込むか、XAML 入力をラップした <xref:System.Xml.XmlReader>、<xref:System.IO.TextReader>、または <xref:System.Xaml.XamlReader> を (そのリーダーの API を使用して読み込むことにより) 読み込むことができます。

- <xref:System.Xaml.XamlServices.Save%2A> のさまざまなシグネチャによって、オブジェクト グラフが保存され、出力がストリーム、ファイル、または <xref:System.Xml.XmlWriter>/<xref:System.IO.TextWriter> インスタンスとして生成されます。

- <xref:System.Xaml.XamlServices.Transform%2A> では、読み込みパスと保存パスを単一の操作としてリンクすることによって、XAML が変換されます。 <xref:System.Xaml.XamlReader> および <xref:System.Xaml.XamlWriter>に対して異なるスキーマ コンテキストまたは異なるバッキング型システムを使用することが可能です。これは、結果として生成される XAML がどのように変換されるかに影響します。

<xref:System.Xaml.XamlServices> の使用方法の詳細については、「[XAMLServices クラスおよび基本的な XAML の読み取りまたは書き込み](basic-reading-writing.md)」を参照してください。

## <a name="xaml-type-system"></a>XAML 型システム

XAML 型システムには、XAML ノード ストリームの特定の単一のノードを操作するために必要な API が用意されています。

<xref:System.Xaml.XamlType> はオブジェクトの表現です - 開始オブジェクト ノードと終了オブジェクト ノードの間で処理するものです。

<xref:System.Xaml.XamlMember> はオブジェクトのメンバーの表現です - 開始メンバー ノードと終了メンバー ノードの間で処理するものです。

<xref:System.Xaml.XamlType.GetAllMembers%2A>、<xref:System.Xaml.XamlType.GetMember%2A>、<xref:System.Xaml.XamlMember.DeclaringType%2A> などの API では、<xref:System.Xaml.XamlType> と <xref:System.Xaml.XamlMember> 間のリレーションシップが報告されます。

.NET XAML サービスによって実装される XAML 型システムの既定の動作は、共通言語ランタイム (CLR) と、リフレクションを使用することによるアセンブリでの CLR 型のスタティック分析に基づいています。 したがって、特定の CLR 型の場合、XAML 型システムの既定の実装では、その型とそのメンバーの XAML スキーマを公開し、XAML 型システムの観点からレポートすることができます。 既定の XAML 型システムでは、型を割り当てできるかどうかの概念が CLR 継承にマップされます。さらに、インスタンスや値型などの概念が CLR のサポート中の動作および機能にマップされます。

## <a name="reference-for-xaml-language-features"></a>XAML 言語機能のリファレンス

XAML をサポートするために、.NET XAML サービスには、XAML 言語の XAML 名前空間に定義される XAML 言語の概念の特定の実装が用意されています。 これらは特定のリファレンス ページとしてドキュメント化されています。 言語機能のドキュメント化は、.NET XAML サービスによって定義された XAML リーダーまたは XAML ライターによってそれらの言語機能が処理されるときに、それらがどのように動作するかの観点に基づいて行われます。 詳細については、「[XAML 名前空間 (x:) 言語機能](namespace-language-features.md)」を参照してください。
