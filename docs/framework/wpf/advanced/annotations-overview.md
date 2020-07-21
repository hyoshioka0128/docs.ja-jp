---
title: 注釈の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- highlights [WPF]
- documents [WPF], annotations
- sticky notes [WPF]
ms.assetid: 716bf474-29bd-4c74-84a4-8e0744bdad62
ms.openlocfilehash: 433fee08d44720640d3f9d1bf2511a6a267eb58e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79145463"
---
# <a name="annotations-overview"></a>注釈の概要
用紙にメモやコメントを書くことは普通の行為であり、人はそれを当たり前のことと思っています。 そのようなメモやコメントが "注釈" です。注釈をドキュメントに追加することで情報に目印を付け、興味のある内容を強調表示し、後で参照します。 印刷したドキュメントにメモを書くことは簡単で一般的な行為ですが、電子ドキュメントに個人的なコメントを追加する機能は利用できるとしても一般的に非常に限定されています。  
  
 このトピックでは、一般的な種類の注釈について取り上げます (特に付箋やハイライトについて)。また、Microsoft Annotations Framework では、Windows Presentation Foundation (WPF) ドキュメント表示コントロールを使用し、アプリケーションでそのような種類の注釈を便利に利用できます。  注釈を利用できる WPF ドキュメント表示コントロールには、<xref:System.Windows.Controls.FlowDocumentReader> や <xref:System.Windows.Controls.FlowDocumentScrollViewer> の他に、<xref:System.Windows.Controls.Primitives.DocumentViewerBase> から派生したコントロール (<xref:System.Windows.Controls.DocumentViewer> や <xref:System.Windows.Controls.FlowDocumentPageViewer> など) があります。  

<a name="caf1_type_stickynotes"></a>
## <a name="sticky-notes"></a>付箋  
 典型的な付箋とは、色の付いた小さな紙切れに情報を記入し、書類に "貼り付ける" というものです。 デジタル付箋は電子ドキュメントのために同様の機能を提供しますが、さまざまなコンテンツを追加できるという柔軟性があります。タイプしたテキスト、手書きのメモ (Tablet PC の "インク" ストロークなど)、Web リンクなどです。  
  
 次の図では、蛍光ペン、テキスト付箋、インク付箋で注釈を付けていることを確認できます。  
  
 ![強調表示、テキストとインク付箋注釈。](./media/caf-stickynote.jpg "CAF_StickyNote")  
  
 次は、アプリケーションで注釈サポートを有効にするためのメソッドのサンプルです。  
  
 [!code-csharp[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](~/samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXml/CSharp/Window1.xaml.cs#docviewxmlstartannotations)]
 [!code-vb[DocViewerAnnotationsXml#DocViewXmlStartAnnotations](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DocViewerAnnotationsXml/visualbasic/window1.xaml.vb#docviewxmlstartannotations)]  
  
<a name="caf1_type_callouts"></a>
## <a name="highlights"></a>強調表示  
 書面であれば、下線を引いたり、蛍光ペンでなぞったり、ドキュメント内の単語を囲んだり、余白に目印や注釈を付けたりするなど、さまざまな方法で書き込みを行い、興味のある項目を目立たせることができます。  Microsoft Annotations Framework の注釈の強調表示にも同様の機能があります。WPF ドキュメント表示コントロールに表示される情報に書き込むことができます。  
  
 次の図は、注釈の強調表示のサンプルです。  
  
 ![注釈の強調表示](./media/caf-callouts.png "CAF_Callouts")  
  
 注釈を付けるときは、一般的に、最初に興味のあるテキストや項目を選択し、右クリックして注釈オプションの <xref:System.Windows.Controls.ContextMenu> を表示します。  次の例では、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を利用し、<xref:System.Windows.Controls.ContextMenu> を宣言しています。ユーザーはルーティング コマンドにアクセスし、注釈を作成、管理できます。  
  
 [!code-xaml[DocViewerAnnotationsXps#CreateDeleteAnnotations](~/samples/snippets/csharp/VS_Snippets_Wpf/DocViewerAnnotationsXps/CSharp/Window1.xaml#createdeleteannotations)]  
  
<a name="caf1_framework_data_anchoring"></a>
## <a name="data-anchoring"></a>データの固定  
 Annotations Framework は、表示レイアウトの特定の位置に注釈を結び付けるだけでなく、ユーザーが選択するデータに注釈を固定します。 そのため、スクロールしたり、表示ウィンドウのサイズを変更したりするなど、ドキュメントの表示が変わっても、注釈はそれが固定されているデータにとどまります。 たとえば、次の図をご覧ください。選択したテキストが蛍光ペンでなぞられています。 ドキュメントの表示が変わると (スクロール、サイズ変更、拡大/縮小、その他の移動)、蛍光ペンは元のデータ選択と一緒に移動します。  
  
 ![注釈データ固定](./media/caf-dataanchoring.png "CAF_DataAnchoring")  
  
<a name="matching_annotations_with_annotated_objects"></a>
## <a name="matching-annotations-with-annotated-objects"></a>注釈と注釈付きオブジェクトを照合する  
 注釈とそれに対応する注釈付きオブジェクトを照合できます。 たとえば、コメント ウィンドウが付いている単純なドキュメント リーダー アプリケーションを想像してください。 そのコメント ウィンドウにはリスト ボックスがあり、そのリスト ボックスに、ドキュメントに固定されている注釈の一覧からのテキストが表示されます。 リスト ボックスの項目を選択すると、それに対応する注釈オブジェクトが固定されている段落がドキュメントに表示されます。  
  
 次の例を見ると、コメント ウィンドウとして機能するそのようなリスト ボックスのイベント ハンドラーの実装方法がわかります。  
  
 [!code-csharp[FlowDocumentAnnotatedViewer#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/CSharp/Window1.xaml.cs#handler)]
 [!code-vb[FlowDocumentAnnotatedViewer#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDocumentAnnotatedViewer/visualbasic/window1.xaml.vb#handler)]  
  
 他のシナリオ例としては、電子メールを利用し、ドキュメント リーダー間で注釈や付箋を交換できるアプリケーションがあります。 そのような機能を利用すると、交換された注釈を含むページにドキュメント リーダーで移動できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Primitives.DocumentViewerBase>
- <xref:System.Windows.Controls.DocumentViewer>
- <xref:System.Windows.Controls.FlowDocumentPageViewer>
- <xref:System.Windows.Controls.FlowDocumentScrollViewer>
- <xref:System.Windows.Controls.FlowDocumentReader>
- <xref:System.Windows.Annotations.IAnchorInfo>
- [注釈スキーマ](annotations-schema.md)
- [ContextMenu の概要](../controls/contextmenu-overview.md)
- [コマンド実行の概要](commanding-overview.md)
- [フロー ドキュメントの概要](flow-document-overview.md)
- [方法: メニュー アイテムにコマンドを追加する](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms741839(v=vs.90))
