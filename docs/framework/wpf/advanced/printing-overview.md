---
title: 印刷の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- print path [WPF], XPS
- printers [WPF], XPSDrv-based
- printing [WPF]
- PrintQueue class PrintServer class [WPF]
- XML Paper Specification (XPS) file format
- XPS (XML Paper Specification) file format
- XPSDrv-based printers
- GDI print path [WPF]
ms.assetid: 0de8ac41-9aa6-413d-a121-7aa6f41539b1
ms.openlocfilehash: 902d51341850b5245b9fa6410b1954b2ab373bbc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187208"
---
# <a name="printing-overview"></a>印刷の概要
Microsoft .NET Framework では、Windows Presentation Foundation (WPF) を使用するアプリケーション開発者は、豊富な新しい印刷および印刷システム管理 API を利用できます。 また、Windows Vista では、Windows フォーム アプリケーションを作成する開発者と、アンマネージド コードを使用する開発者も、これらの印刷システム拡張機能の一部を使用できます。 この新しい機能の中核となるのが、新しい XML Paper Specification (XPS) ファイル形式と XPS 印刷パスです。  
  
 このトピックは、次のセクションで構成されています。  
  
<a name="introduction_to_XPS"></a>
## <a name="about-xps"></a>XPS について  
 XPS は、電子ドキュメント形式、スプール ファイル形式、およびページ記述言語です。 XML、Open Packaging Conventions (OPC)、その他の業界標を使用してクロスプラットフォームのドキュメントを作成する OpenDocument 形式の 1 つです。 XPS により、デジタル ドキュメントの作成、共有、印刷、表示、アーカイブを行うプロセスが簡略化されます。 XPS の追加情報については、「[XPS ドキュメント](/windows/desktop/printdocs/documents)」を参照してください。  
  
 WPF を使用した XPS ベースのコンテンツの印刷手法のいくつかは、「[XPS ファイルをプログラムにより印刷する](how-to-programmatically-print-xps-files.md)」で説明されています。 このトピックに含まれるコンテンツの確認中にこれらのサンプルを参照すると、役に立つ場合があります。 (アンマネージド コードの開発者は、[MXDC_ESCAPE 関数](/windows/desktop/printdocs/mxdc-escape)のドキュメントを参照する必要があります。 Windows フォームの開発者は、<xref:System.Drawing.Printing> 名前空間の API を使用する必要があります。この名前空間では、完全な XPS 印刷パスはサポートされていませんが、ハイブリッドの GDI-XPS 印刷パスがサポートされています。 以下の**印刷パスのアーキテクチャ**をご覧ください。)  
  
<a name="XPS_print_path_intro"></a>
## <a name="xps-print-path"></a>XPS 印刷パス  
 XML Paper Specification (XPS) 印刷パスは、Windows アプリケーションでの印刷の処理方法を再定義する Windows の新機能です。 XPS は、ドキュメントのプレゼンテーション言語 (RTF など)、印刷スプーラの形式 (WMF など)、ページ記述言語 (PCL や Postscript など) に置き換えることができるため、新しい印刷パスでは、アプリケーションの公開から印刷ドライバーまたはデバイスでの最終処理まで、XPS 形式が維持されます。  
  
 XPS 印刷パスは、XPS のプリンター ドライバー モデル (XPSDrv) 上に構築されています。XPSDrv により、開発者は "What You See Is What You Get" (WYSIWYG) の印刷、色のサポートの向上、および印刷のパフォーマンスの大幅な向上など、いくつかの利点を得られます。 (XPSDrv の詳細については、[Windows Driver Kit のドキュメント](/windows-hardware/drivers/)をご覧ください)。  
  
 XPS ドキュメントの印刷スプーラの操作は、基本的に Windows の以前のバージョンと同じです。 ただし、既存の GDI 印刷パスに加えて XPS 印刷パスをサポートするように強化されました。 新しい印刷パスで、XPS スプール ファイルがネイティブに使用されます。 Windows の以前のバージョン向けに記述されたユーザー モードのプリンター ドライバーは引き続き機能しますが、XPS 印刷パスを使用するためには、XPS プリンター ドライバー (XPSDrv) が必要になります。  
  
 XPS 印刷パスには次のような大きな利点があります。  
  
- WYSIWYG 印刷のサポート  
  
- 高度なカラー プロファイルのネイティブ サポート (1 チャンネルあたり 32 ビット (bpc)、CMYK、名前付きの色、n インクなど)、および透明度とグラデーションのネイティブ サポート。  
  
- .NET Framework と Win32 ベースのアプリケーションの両方における印刷パフォーマンスの向上。  
  
- 業界標準の XPS 形式。  
  
 基本的な印刷シナリオでは、ユーザー インターフェイス、構成、およびジョブの送信用の 1 つのエントリ ポイントで、簡単かつ直感的な API を使用できます。 高度なシナリオ用に、[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] のカスタマイズ (または [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] がまったくない)、同期または非同期の印刷、および一括印刷の機能のサポートが追加されました。 いずれのオプションでも、完全または部分的な信頼モードでの印刷のサポートを提供します。  
  
 XPS は、拡張性を考慮して設計されています。 機能拡張フレームワークを使用して、機能を XPS にモジュール形式で追加できます。 拡張機能は、次のとおりです。  
  
- 印刷スキーマ。 パブリックのスキーマは定期的に更新され、デバイスの機能を迅速に拡張することができます。 (下記の「**PrintTicket と PrintCapabilities**」をご覧ください。)  
  
- 拡張可能なフィルター パイプライン。 XPS プリンター ドライバー (XPSDrv) フィルター パイプラインは、XPS ドキュメントの直接的および拡張性の高い印刷を可能にするように作られています。 詳細については、「[XPSDrv プリンター ドライバー](/windows-hardware/drivers/print/xpsdrv-printer-drivers)」を参照してください。
  
### <a name="print-path-architecture"></a>印刷パスのアーキテクチャ  
 Win32 アプリケーションと .NET Framework アプリケーションでは XPS がサポートされていますが、Win32 アプリケーションと Windows フォーム アプリケーションでは、XPS プリンター ドライバー (XPSDrv) 用に XPS 形式のコンテンツを作成するため、GDI から XPS への変換が使用されます。 これらのアプリケーションでは、XPS 印刷パスを使用する必要はなく、Enhanced Metafile (EMF) ベースの印刷を引き続き使用できます。 ただし、XPS の機能と拡張機能のほとんどは、XPS 印刷パスを対象としたアプリケーション以外では使用できません。  
  
 Win32 アプリケーションと Windows フォーム アプリケーションで XPSDrv ベースのプリンターを使用できるようにするため、XPS プリンター ドライバー (XPSDrv) では GDI 形式から XPS 形式への変換がサポートされています。 XPSDrv モデルには XPS 形式から GDI 形式へのコンバーターも用意されているため、Win32 アプリケーションで XPS ドキュメントを印刷できます。 WPF アプリケーションでは、書き込み操作の対象の印刷キューに XPSDrv ドライバーがない場合は常に、<xref:System.Windows.Xps.XpsDocumentWriter> クラスの <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> メソッドと <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> メソッドによって、XPS 形式から GDI 形式への変換が自動的に行われます。 (Windows フォーム アプリケーションでは XPS ドキュメントを印刷できません)。  
  
 次の図では、印刷サブシステムが示され、Microsoft によって提供される部分と、ソフトウェアおよびハードウェアのベンダーによって定義される部分が示されています。  
  
 ![XPS 印刷システムを示すスクリーンショット。](./media/printing-overview/xml-paper-specification-print-system.png)  
  
### <a name="basic-xps-printing"></a>XPS の基本的な印刷  
 WPF では、基本 API と高度な API の両方が定義されています。 広範な印刷のカスタマイズや完全な XPS の機能セットへのアクセスを必要としないアプリケーションでは、基本的な印刷サポートを使用できます。 基本的な印刷サポートは、最小構成を必要とし、使い慣れた [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を特長とする印刷ダイアログ コントロールを介して公開されます。 XPS の機能の多くは、この簡略化された印刷モデルによって使用できます。  
  
#### <a name="printdialog"></a>PrintDialog  
 <xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType> コントロールには、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)]、構成、および XPS ジョブの送信用に 1 つのエントリ ポイントが用意されています。 コントロールのインスタンス化と使用方法については、「[方法 : 印刷ダイアログ ボックスを呼び出す](how-to-invoke-a-print-dialog.md)」をご覧ください。  
  
### <a name="advanced-xps-printing"></a>高度な XPS の印刷  
 XPS 機能の完全なセットにアクセスするには、高度な印刷 API を使用する必要があります。 いくつかの関連する API について、以下で詳しく説明します。 XPS 印刷パス API の完全な一覧については、<xref:System.Windows.Xps> および <xref:System.Printing> 名前空間のリファレンスを参照してください。  
  
#### <a name="printticket-and-printcapabilities"></a>PrintTicket と PrintCapabilities  
 <xref:System.Printing.PrintTicket> クラスと <xref:System.Printing.PrintCapabilities> クラスは、XPS の高度な機能の基盤となります。 いずれの種類のオブジェクトも、照合順序、両面印刷、ホチキス止めなど、XML 形式の印刷向け機能の構造になっています。これらの構造は、印刷スキーマによって定義されます。 <xref:System.Printing.PrintTicket> は、プリンターに印刷ジョブの処理方法を指示します。 <xref:System.Printing.PrintCapabilities> クラスは、プリンターの機能を定義します。 プリンターの機能のクエリを実行すると、プリンターのサポート機能を最大限に活用する <xref:System.Printing.PrintTicket> を作成できます。 同様に、サポートされていない機能を回避できます。  
  
 次の例は、プリンターの <xref:System.Printing.PrintCapabilities> でクエリを実行する方法と、コードを使用した <xref:System.Printing.PrintTicket> の作成方法を示しています。  
  
 [!code-cpp[xpscreate#PrinterCapabilities](~/samples/snippets/cpp/VS_Snippets_Wpf/XpsCreate/CPP/XpsCreate.cpp#printercapabilities)]
 [!code-csharp[xpscreate#PrinterCapabilities](~/samples/snippets/csharp/VS_Snippets_Wpf/XpsCreate/CSharp/XpsCreate.cs#printercapabilities)]
 [!code-vb[xpscreate#PrinterCapabilities](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XpsCreate/visualbasic/xpscreate.vb#printercapabilities)]  
  
#### <a name="printserver-and-printqueue"></a>PrintServer と PrintQueue  
 <xref:System.Printing.PrintServer> クラスはネットワーク プリント サーバーを表し、<xref:System.Printing.PrintQueue> クラスはプリンターとそれに関連付けられた出力ジョブのキューを表します。 これらの API を併用すると、サーバーの印刷ジョブを高度に管理できます。 <xref:System.Printing.PrintServer>、またはその派生クラスのいずれかを使用すると、<xref:System.Printing.PrintQueue> を管理できます。 新しい印刷ジョブをキューに挿入するには、<xref:System.Printing.PrintQueue.AddJob%2A> メソッドを使用します。  
  
 次の例は、コードを使用して <xref:System.Printing.LocalPrintServer> を作成し、既定の <xref:System.Printing.PrintQueue> にアクセスする方法を示しています。  
  
 [!code-csharp[xpsprint#PrintQueueSnip](~/samples/snippets/csharp/VS_Snippets_Wpf/XpsPrint/CSharp/XpsPrintHelper.cs#printqueuesnip)]
 [!code-vb[xpsprint#PrintQueueSnip](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XpsPrint/visualbasic/xpsprinthelper.vb#printqueuesnip)]  
  
#### <a name="xpsdocumentwriter"></a>XpsDocumentWriter  
 <xref:System.Windows.Xps.XpsDocumentWriter> を、その多くの <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> メソッドおよび <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> メソッドと共に使用すると、XPS ドキュメントを <xref:System.Printing.PrintQueue> に書き込むことができます。 たとえば、<xref:System.Windows.Xps.XpsDocumentWriter.Write%28System.Windows.Documents.FixedPage%2CSystem.Printing.PrintTicket%29> メソッドを使用すると、XPS ドキュメントと <xref:System.Printing.PrintTicket> を同期的に出力できます。 <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%28System.Windows.Documents.FixedDocument%2CSystem.Printing.PrintTicket%29> メソッドを使用すると、XPS ドキュメントと <xref:System.Printing.PrintTicket> を非同期的に出力できます。  
  
 次の例は、コードを使用して <xref:System.Windows.Xps.XpsDocumentWriter> を作成する方法を示しています。  
  
 [!code-csharp[XpsPrint#PrintQueueSnip](~/samples/snippets/csharp/VS_Snippets_Wpf/XpsPrint/CSharp/XpsPrintHelper.cs#printqueuesnip)]
 [!code-vb[XpsPrint#PrintQueueSnip](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XpsPrint/visualbasic/xpsprinthelper.vb#printqueuesnip)]  
  
 さらに <xref:System.Printing.PrintQueue.AddJob%2A> メソッドは印刷方法を提供します。 「[方法 : XPS ファイルをプログラムにより印刷する](how-to-programmatically-print-xps-files.md)」をご覧ください。 詳細について。  
  
<a name="GDI_Print_Path_intro"></a>
## <a name="gdi-print-path"></a>GDI 印刷パス  
 WPF アプリケーションでは XPS 印刷パスがネイティブにサポートされていますが、Win32 アプリケーションと Windows フォーム アプリケーションでも一部の XPS の機能を利用できます。 XPS プリンター ドライバー (XPSDrv) では、GDI ベースの出力を XPS 形式に変換できます。 高度なシナリオ用に、[Microsoft XPS Document Converter (MXDC)](/windows/desktop/printdocs/microsoft-xps-document-converter--mxdc-) を使用した、コンテンツのカスタム変換がサポートされています。 同様に、WPF アプリケーションでも、<xref:System.Windows.Xps.XpsDocumentWriter> クラスの <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A> メソッドまたは <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A> メソッドのいずれかを呼び出し、対象の印刷キューとして XpsDrv 以外のプリンターを指定することにより、GDI 印刷パスに出力することができます。  

XPS の機能またはサポートを必要としないアプリケーションでは、現在の GDI 印刷パスは変更されません。  
  
- GDI 印刷パスとさまざまな XPS 変換オプションに関するその他の関連資料については、「[Microsoft XPS Document Converter (MXDC)](/windows/desktop/printdocs/microsoft-xps-document-converter--mxdc-)」および「[XPSDrv プリンター ドライバー](/windows-hardware/drivers/print/xpsdrv-printer-drivers)」を参照してください。  
  
<a name="XPS_Driver_Model_intro"></a>
## <a name="xpsdrv-driver-model"></a>XPSDrv ドライバー モデル  
 XPS 印刷パスでは、XPS 対応のプリンターまたはドライバーに出力する場合に、ネイティブの印刷スプール形式として XPS を使用すると、スプーラーの効率性が高まります。 スプール処理の簡略化により、ドキュメントをスプールする前に、EMF データ ファイルなどの中間スプール ファイルを生成する必要がなくなります。 スプール ファイルのサイズを小さくすると、XPS 印刷パスのネットワーク トラフィックが減少し、印刷のパフォーマンスが向上します。  
  
 EMF は、サービスのレンダリングのために、アプリケーションの出力を GDI に対する一連の呼び出しとして表すクローズ形式です。 EMF と異なり、XPS スプール形式では、XPS ベースのプリンター ドライバー (XPSDrv) に出力するときにさらに解釈する必要のない、実際のドキュメントが表されます。 ドライバーは、その形式のデータを直接操作できます。 この機能により、EMF ファイルと GDI ベースの印刷ドライバーを使用するときに、データと色空間の変換が必要なくなります。  
  
 同等の EMF と比較すると、XPS プリンター ドライバー (XPSDrv) を対象とする XPS ドキュメントを使用すると、通常はスプール ファイルのサイズが減少します。ただし、例外もあります。  
  
- ベクター グラフィックが非常に複雑で、複数の階層があるか、非効率的に記述されている場合、同じグラフィックスのビットマップ形式のバージョンよりもサイズが大きくなることがあります。  
  
- 画面表示の目的で、XPS ファイルにはデバイス フォントおよびコンピューター ベースのフォントが埋め込まれます。一方、GDI のスプール ファイルにはデバイス フォントは埋め込まれません。 しかし、両方の種類のフォントがサブセット化されているため (下記参照)、プリンター ドライバーは、ファイルをプリンターに送信する前にデバイス フォントを削除することができます。  
  
 スプール サイズの削減は、いくつかのメカニズムを通じて行われます。  
  
- **フォントのサブセット化**。 実際のドキュメント内で使用される文字のみが XPS ファイルに格納されます。  
  
- **高度なグラフィックスのサポート**。 透過性とグラデーションのプリミティブのネイティブ サポートにより、XPS ドキュメントの内容のラスタライズを回避できます。  
  
- **共通リソースの識別**。 複数回使用するリソース (会社のロゴを表す画像など) は共有リソースとして扱われ、一度だけ読み込まれます。  
  
- **ZIP 圧縮**。 すべての XPS ドキュメントで ZIP 圧縮が使用されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.PrintDialog>
- <xref:System.Windows.Xps.XpsDocumentWriter>
- <xref:System.Windows.Xps.Packaging.XpsDocument>
- <xref:System.Printing.PrintTicket>
- <xref:System.Printing.PrintCapabilities>
- <xref:System.Printing.PrintServer>
- <xref:System.Printing.PrintQueue>
- [方法トピック](printing-how-to-topics.md)
- [WPF のドキュメント](documents-in-wpf.md)
- [XPS ドキュメント](/windows/desktop/printdocs/documents)
- [ドキュメントのシリアル化および保存](document-serialization-and-storage.md)
- [Microsoft XPS Document Converter (MXDC)](/windows/desktop/printdocs/microsoft-xps-document-converter--mxdc-)
