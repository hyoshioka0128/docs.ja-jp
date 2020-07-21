---
title: ドキュメント
ms.date: 03/30/2017
helpviewer_keywords:
- documents [WPF], packaging
- documents [WPF], text layout
- documents [WPF], XPS
- 'XPS documents [WPF], , '
- documents [WPF], controls
- documents [WPF], types of
- documents [WPF], browser-viewable
ms.assetid: 6e8db7bc-050a-4070-aa72-bb8c46e87ff8
ms.openlocfilehash: e88604c42b253b48ee605f42f24fe301e339f74b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174681"
---
# <a name="documents-in-wpf"></a>WPF のドキュメント
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は、Windows の前の世代よりも簡単にアクセスおよび読み取りを行うことができるように設計されている、高品質なコンテンツの作成を可能にするさまざまなドキュメント機能を提供します。 拡張された機能と品質に加えて、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、ドキュメントの表示、パッケージ化、およびセキュリティの統合されたサービスも提供します。 ここでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のドキュメントの種類とドキュメントのパッケージ化の概要を説明します。  

<a name="types_of_documents"></a>
## <a name="types-of-documents"></a>ドキュメントの種類  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、ドキュメントは用途に基づいて大きく 2 つのカテゴリに分けられます。これらのドキュメントのカテゴリは "固定ドキュメント" および "フロー ドキュメント" と呼ばれます。  
  
 固定ドキュメントは、使用されるディスプレイまたはプリンター ハードウェアに関係なく、正確な "What You See Is What You Get" (WYSIWYG) プレゼンテーションを必要とするアプリケーションを対象に用意されています。 固定ドキュメントの一般的な用途としては、元のページ デザインに準拠していることが重要になるデスクトップ パブリッシング、ワード プロセッシング、およびフォーム レイアウトなどがあります。 レイアウトの一部として、固定ドキュメントでは、使用中のディスプレイまたは印刷デバイスに依存しないコンテンツ要素の正確な配置位置が保持されます。 たとえば、96 dpi のディスプレイに表示される固定ドキュメント ページは、600 dpi のレーザー プリンターに出力される場合に、4800 dpi の写真植字に出力される場合とまったく同じように表示されます。 ドキュメントの品質は各デバイスの機能に応じて最大化されますが、ページ レイアウトはすべての場合において同じになります。  
  
 これに対して、フロー ドキュメントは、表示と読みやすさを最適化するように設計されており、ドキュメントが主に読みやすさを目的としている場合に最適です。 フロー ドキュメントは、1 つの定義済みのレイアウトに設定するのではなく、ウィンドウのサイズ、デバイスの解像度、省略可能なユーザー設定など、ランタイム変数に基づいてコンテンツを動的に調整したりリフローしたりします。 Web ページは、そのコンテンツが現在のウィンドウに収まるように動的にフォーマットされるフロー ドキュメントの簡単な例です。 フロー ドキュメントは、ランタイム環境に基づいて、ユーザーにとっての表示と読みやすさを最適化します。 たとえば、同じフロー ドキュメントでも、高解像度の 19 インチ ディスプレイなのか、小型の 2x3 インチの PDA 画面なのかに応じて、最も読みやすくなるように書式設定が動的に変更されます。 また、フロー ドキュメントには、検索、読みやすさを最適化するモードの表示、およびフォントのサイズと外観を変更する機能を含むさまざまな組み込み機能があります。  フロー ドキュメントの図、例、および詳細については、「[フロー ドキュメントの概要](flow-document-overview.md)」を参照してください。  
  
<a name="document_viewer"></a>
## <a name="document-controls-and-text-layout"></a>ドキュメント コントロールとテキスト レイアウト  
 .NET Framework には、アプリケーション内の固定ドキュメント、フロー ドキュメント、および一般的なテキストの使用を簡略化する、事前にビルドされたコントロールのセットが用意されています。  固定ドキュメントのコンテンツの表示は、<xref:System.Windows.Controls.DocumentViewer> コントロールを使用してサポートされます。  フロー ドキュメントのコンテンツの表示は、異なるユーザー シナリオに割り当てられている <xref:System.Windows.Controls.FlowDocumentReader>、<xref:System.Windows.Controls.FlowDocumentPageViewer>、および <xref:System.Windows.Controls.FlowDocumentScrollViewer> という 3 つの異なるコントロールによってサポートされます (後述のセクションを参照してください)。  その他の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールでは、一般的なテキストの使用をサポートする簡略化されたレイアウトが提供されます (後述の「[ユーザー インターフェイスのテキスト](#text_in_the_user_interface)」を参照してください)。  
  
### <a name="fixed-document-control---documentviewer"></a>固定ドキュメント コントロール - DocumentViewer  
 <xref:System.Windows.Controls.DocumentViewer> コントロールは <xref:System.Windows.Documents.FixedDocument> コンテンツを表示するように設計されています。 <xref:System.Windows.Controls.DocumentViewer> コントロールは、印刷出力、クリップボードへのコピー、拡大、およびテキスト検索の機能を含む共通の操作へのサポートが組み込まれている直感的なユーザー インターフェイスを提供します。 コントロールは、使い慣れたスクロール機構を使用してコンテンツのページへのアクセスを提供します。 すべての [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールと同様に、<xref:System.Windows.Controls.DocumentViewer> は、事実上すべてのアプリケーションまたは環境に視覚的にコントロールを統合できるようにする、完全なスタイル変更または一部のスタイル変更をサポートします。  
  
 <xref:System.Windows.Controls.DocumentViewer> は、読み取り専用の形でコンテンツを表示するように設計されています。コンテンツの編集または変更は行うことはできず、サポートされていません。  
  
<a name="flow_document"></a>
### <a name="flow-document-controls"></a>フロー ドキュメント コントロール  

> [!NOTE]
> フロー ドキュメント機能の詳細、およびフロー ドキュメントの作成方法については、「[フロー ドキュメントの概要](flow-document-overview.md)」を参照してください。  
  
 フロー ドキュメントのコンテンツの表示は、<xref:System.Windows.Controls.FlowDocumentReader>、<xref:System.Windows.Controls.FlowDocumentPageViewer>、および <xref:System.Windows.Controls.FlowDocumentScrollViewer> という 3 つのコントロールによってサポートされます。  
  
#### <a name="flowdocumentreader"></a>FlowDocumentReader  
 <xref:System.Windows.Controls.FlowDocumentReader> には、単一ページ (一度に 1 ページ) 表示モード、2 ページ (読書形式) 表示モード、連続スクロール (ボトムレス) 表示モードなど、さまざまな表示モードをユーザーが動的に選択できるようにするための機能が用意されています。  これらの表示モードの詳細については、「<xref:System.Windows.Controls.FlowDocumentReaderViewingMode>」を参照してください。  表示モードを動的に切り替える必要がない場合は、<xref:System.Windows.Controls.FlowDocumentPageViewer> および <xref:System.Windows.Controls.FlowDocumentScrollViewer> を使用すると便利です。これらは、特定の表示モードに固定された軽量のフロー コンテンツ ビューアーです。  
  
#### <a name="flowdocumentpageviewer-and-flowdocumentscrollviewer"></a>FlowDocumentPageViewer と FlowDocumentScrollViewer  
 <xref:System.Windows.Controls.FlowDocumentPageViewer> は、コンテンツを一度に 1 ページずつ表示し、<xref:System.Windows.Controls.FlowDocumentScrollViewer> はコンテンツを連続したスクロール モードで表示します。  <xref:System.Windows.Controls.FlowDocumentPageViewer> と <xref:System.Windows.Controls.FlowDocumentScrollViewer> とは、いずれも特定の表示モードに固定されています。 <xref:System.Windows.Controls.FlowDocumentReader> と比較してください。このリーダーでは、<xref:System.Windows.Controls.FlowDocumentReaderViewingMode> 列挙体により各種表示モードを動的に切り替えることができますが、<xref:System.Windows.Controls.FlowDocumentPageViewer> や <xref:System.Windows.Controls.FlowDocumentScrollViewer> よりも多くのリソースを消費します。  
  
 既定では、垂直スクロール バーは常に表示され、水平スクロール バーは必要に応じて表示されます。 <xref:System.Windows.Controls.FlowDocumentScrollViewer> の既定の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] にはツール バーが含まれませんが、<xref:System.Windows.Controls.FlowDocumentScrollViewer.IsToolBarVisible%2A> プロパティを使用して組み込みツール バーを有効にできます。  
  
<a name="text_in_the_user_interface"></a>
### <a name="text-in-the-user-interface"></a>ユーザー インターフェイスのテキスト  
 ドキュメントへのテキストの追加だけでなく、テキストはもちろん、フォームなどのアプリケーション UI で使用できます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、画面にテキストを描画するための複数のコントロールが含まれています。 各コントロールは異なるシナリオを対象にしており、それぞれに一連の機能と制限があります。 一般的に、[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] で短い文を使用するなど限定的なテキストのサポートが必要な場合は、<xref:System.Windows.Controls.TextBlock> 要素を使用するべきです。 最小限のテキスト サポートが必要な場合には、<xref:System.Windows.Controls.Label> を使用します。 詳細については、「[TextBlock の概要](../controls/textblock-overview.md)」を参照してください。  
  
<a name="packaging"></a>
## <a name="document-packaging"></a>ドキュメントのパッケージ化  
 <xref:System.IO.Packaging> API は、簡単にアクセスでき、移植可能で、配布しやすい単一のコンテナー内のアプリケーション データ、ドキュメント コンテンツ、および関連リソースを編成するための効率的な方法を提供します。 ZIP ファイルは、複数のオブジェクトを 1 つの単位として保持することができる <xref:System.IO.Packaging.Package> の種類の一例です。 パッケージ化の API は、XML ファイルおよび ZIP ファイル アーキテクチャと共に Open Packaging Conventions 標準を使用して、既定の <xref:System.IO.Packaging.ZipPackage> 実装を提供します。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のパッケージ化 API は、パッケージの作成、およびパッケージへのオブジェクトの格納とそれらのオブジェクトへのアクセスを簡単にします。 <xref:System.IO.Packaging.Package> に格納されたオブジェクトは <xref:System.IO.Packaging.PackagePart> ("パーツ") と呼ばれます。 パッケージには、パーツの発行元を識別し、パッケージのコンテンツが変更されていないことを検証するのに使用できる署名されたデジタル証明書を含めることもできます。  パッケージには、追加情報をパッケージに追加できたり、既存のパーツのコンテンツを実際に変更することなく特定のパーツに関連付けたりすることができる、<xref:System.IO.Packaging.PackageRelationship> 機能も含まれます。  パッケージ サービスでは、Microsoft Windows Rights Management (RM) もサポートされます。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] パッケージ アーキテクチャは、さまざまな重要な技術の基盤として機能します。  
  
- XML Paper Specification (XPS) に準拠する XPS ドキュメント。  
  
- Microsoft Office "12" Open XML 形式のドキュメント (.docx)。  
  
- 独自のアプリケーション設計のカスタム保存形式。  
  
 パッケージ化 API に基づいて、<xref:System.Windows.Xps.Packaging.XpsDocument> は、特に [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 固定コンテンツ ドキュメントを格納するために設計されています。 <xref:System.Windows.Xps.Packaging.XpsDocument> は、ビューアーで開き、<xref:System.Windows.Controls.DocumentViewer> コントロールに表示し、印刷スプールにルーティングし、XPS と互換性のあるプリンターに直接出力することができる、自己完結型ドキュメントです。  
  
 以下のセクションでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で提供されている <xref:System.IO.Packaging.Package> および <xref:System.Windows.Xps.Packaging.XpsDocument> API について追加情報を示します。  
  
<a name="packages"></a>
### <a name="package-components"></a>パッケージ コンポーネント  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] パッケージ化 API は、アプリケーション データとドキュメントを 1 つの移植可能な単位に編成できるようにします。 ZIP ファイルは、最もよく使用されるパッケージの種類の 1 つであり、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で用意されている既定のパッケージの種類です。  <xref:System.IO.Packaging.Package> 自体は、<xref:System.IO.Packaging.ZipPackage> が標準のオープン XML および ZIP ファイル アーキテクチャを使用して実装される元となる抽象クラスです。  <xref:System.IO.Packaging.Package.Open%2A> メソッドは、既定では <xref:System.IO.Packaging.ZipPackage> を使用して ZIP ファイルを作成および使用します。 パッケージには、次の 3 種類の基本的な項目を含めることができます。  
  
|||  
|-|-|  
|<xref:System.IO.Packaging.PackagePart>|アプリケーション コンテンツ、データ、ドキュメント、およびリソース ファイル。|  
|<xref:System.IO.Packaging.PackageDigitalSignature>|識別、認証、および検証のための [X.509 証明書]。|  
|<xref:System.IO.Packaging.PackageRelationship>|パッケージまたは特定のパーツに関連する追加された情報。|  
  
<a name="PackageParts"></a>
#### <a name="packageparts"></a>PackageParts  
 <xref:System.IO.Packaging.PackagePart> ("パーツ") は <xref:System.IO.Packaging.Package> に格納されたオブジェクトを参照する抽象クラスです。 ZIP ファイルでは、パッケージ パーツは ZIP ファイル内に格納された個別のファイルに対応します。  <xref:System.IO.Packaging.ZipPackagePart> は、<xref:System.IO.Packaging.ZipPackage> 内に格納されるシリアル化可能なオブジェクトに対する既定の実装を提供します。  ファイル システムと同様に、パッケージに含まれているパーツは、階層的ディレクトリまたは "フォルダー スタイル" 編成で格納されます。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] パッケージ化 API を使用すると、アプリケーションは、単一の ZIP ファイル コンテナーを使用して、複数の <xref:System.IO.Packaging.PackagePart> オブジェクトの書き込み、格納、および読み取りを行うことができます。  
  
<a name="PackageDigitalSignatures"></a>
#### <a name="packagedigitalsignatures"></a>PackageDigitalSignatures  
 セキュリティ保護のために、パッケージ内のパーツに <xref:System.IO.Packaging.PackageDigitalSignature> ("デジタル署名") を関連付けることができます。 <xref:System.IO.Packaging.PackageDigitalSignature> には、次の 2 つの機能を提供する [509] が組み込まれています。  
  
1. パーツの発行元を識別および認証します。  
  
2. パーツが変更されていないことを検証します。  
  
 デジタル署名はパーツを変更できなくするものではありませんが、パーツが何らかの方法で変更されている場合、デジタル署名に対する検証チェックは失敗します。 その後、アプリケーションでは適切なアクションを実行することができます。たとえば、パーツを開く操作をブロックしたり、パーツが変更されていて安全ではないことをユーザーに知らせたりすることができます。  
  
<a name="PackageRelationships"></a>
#### <a name="packagerelationships"></a>PackageRelationships  
 <xref:System.IO.Packaging.PackageRelationship> ("リレーションシップ") は、追加情報をパッケージまたはパッケージ内のパーツに関連付けるための機構を提供します。 リレーションシップは、実際のパーツのコンテンツを変更することなく追加情報をパーツに関連付けることができるパッケージ レベルの機能です。 パーツのコンテンツに新しいデータを直接挿入するのは、次のように多くの場合において実用的ではありません。  
  
- パーツの実際の種類およびそのコンテンツ スキーマが不明な場合。  
  
- わかっている場合でも、コンテンツ スキーマが新しい情報を追加する方法を提供しない可能性がある場合。  
  
- パーツが、デジタル署名されたり、暗号化されたり、変更できなくされたりする可能性がある場合。  
  
 パッケージ リレーションシップは、追加情報を個別のパーツまたはパッケージ全体に追加または関連付けるための検出可能な方法を提供します。 パッケージ リレーションシップは、次の 2 つの主要な機能のために使用されます。  
  
1. 1 つのパーツから別のパーツへの依存関係の定義。  
  
2. メモまたはパーツに関連したその他のデータを追加する情報リレーションシップの定義。  
  
 <xref:System.IO.Packaging.PackageRelationship> は、依存関係を定義し、パッケージのパーツまたはパッケージ全体に関連付けられたその他の情報を追加するための、すばやく検出可能な方法を提供します。  
  
<a name="Dependency_Relationships"></a>
##### <a name="dependency-relationships"></a>依存関係  
 依存関係は、1 つのパーツによって他のパーツに対して作成される依存関係を記述するために使用されます。 たとえば、パッケージには、1 つ以上の \<img> イメージ タグを含む HTML パーツが含まれている場合があります。 イメージ タグは、パッケージの内部またはパッケージの外部 (インターネット経由でアクセスできる場合など) にあるその他のパーツとして配置されているイメージを参照します。 HTML ファイルに関連付けられている <xref:System.IO.Packaging.PackageRelationship> を作成すると、依存リソースの検出およびアクセスがすばやく簡単になります。 ブラウザーまたはビューアー アプリケーションは、パーツ リレーションシップに直接アクセスし、スキーマが不明である場合や、ドキュメントの解析を行わない状態でも依存リソースをすぐにアセンブルできます。  
  
<a name="Information_Relationships"></a>
##### <a name="information-relationships"></a>情報リレーションシップ  
 メモまたは注釈と同様に、<xref:System.IO.Packaging.PackageRelationship> は、実際にパーツのコンテンツ自体を変更することなく、パーツに関連付けられるその他の種類の情報を格納するために使用することもできます。  
  
<a name="XPS_Documents"></a>
## <a name="xps-documents"></a>XPS ドキュメント  
 XML Paper Specification (XPS) ドキュメントは、レンダリングのために必要なすべてのリソースおよび情報と共に 1 つ以上の固定ドキュメントを格納するパッケージです。  XPS はネイティブな Windows Vista 印刷スプール ファイル形式でもあります。  <xref:System.Windows.Xps.Packaging.XpsDocument> は、標準 ZIP データセットに格納され、イメージ ファイルやフォント ファイルなどのバイナリ コンポーネントと XML コンポーネントを組み合わせて格納できます。 [PackageRelationships](#PackageRelationships) は、ドキュメントを完全にレンダリングするために必要なコンテンツとリソースの間の依存関係を定義するために使用されます。  <xref:System.Windows.Xps.Packaging.XpsDocument> の設計は、次のような複数の用途をサポートする高品質な単一のドキュメント ソリューションを提供します。  
  
- 単一の移植可能で配布しやすいファイルとして、固定ドキュメント コンテンツおよびリソースを読み取り、書き込み、および格納する。  
  
- XPS ビューアー アプリケーションを使用してドキュメントを表示する。  
  
- Windows Vista のネイティブな印刷スプール出力形式でドキュメントを出力する。  
  
- XPS と互換性があるプリンターにドキュメントを直接ルーティングする。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Documents.FixedDocument>
- <xref:System.Windows.Documents.FlowDocument>
- <xref:System.Windows.Xps.Packaging.XpsDocument>
- <xref:System.IO.Packaging.ZipPackage>
- <xref:System.IO.Packaging.ZipPackagePart>
- <xref:System.IO.Packaging.PackageRelationship>
- <xref:System.Windows.Controls.DocumentViewer>
- [[テキスト]](optimizing-performance-text.md)
- [フロー ドキュメントの概要](flow-document-overview.md)
- [印刷の概要](printing-overview.md)
- [ドキュメントのシリアル化および保存](document-serialization-and-storage.md)
