---
title: WebBrowser コントロールの概要
description: WebBrowser コントロールを使用して、Web コントロールを1つのアプリケーション内の Windows フォームコントロールとシームレスに結合する方法について説明します。
ms.date: 03/30/2017
f1_keywords:
- WebBrowser
helpviewer_keywords:
- WebBrowser control [Windows Forms], about
- Web pages [Windows Forms], displaying in applications
ms.assetid: 6e3e1cc2-9c48-4136-9659-e99e4e60b7e9
ms.openlocfilehash: 6a0548bb0f5905d8f848ab13fb82d32b50caa891
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325737"
---
# <a name="webbrowser-control-overview"></a>WebBrowser コントロールの概要
コントロールは、 <xref:System.Windows.Forms.WebBrowser> WebBrowser ActiveX コントロールのマネージラッパーを提供します。 マネージラッパーを使用すると、Windows フォームクライアントアプリケーションで Web ページを表示できます。 コントロールを使用して、 <xref:System.Windows.Forms.WebBrowser> Internet explorer の Web 閲覧機能をアプリケーションで複製することも、Internet explorer の既定の機能を無効にして、簡単な HTML ドキュメントビューアーとしてコントロールを使用することもできます。 コントロールを使用して、DHTML ベースのユーザーインターフェイス要素をフォームに追加し、コントロールでホストされているという事実を非表示にすることもでき <xref:System.Windows.Forms.WebBrowser> ます。 この方法を使用すると、Web コントロールを1つのアプリケーション内の Windows フォームコントロールとシームレスに組み合わせることができます。  
  
## <a name="frequently-used-properties-methods-and-events"></a>頻繁に使用されるプロパティ、メソッド、およびイベント  
 <xref:System.Windows.Forms.WebBrowser>コントロールには、Internet Explorer で検出されたコントロールを実装するために使用できるプロパティ、メソッド、およびイベントがいくつかあります。 たとえば、メソッドを使用して `Navigate` アドレスバーを実装し、、、、およびの各メソッドを使用して、 `GoBack` `GoForward` `Stop` `Refresh` ツールバーにナビゲーションボタンを実装できます。 イベントを処理して、プロパティの値とタイトルバーにプロパティの値を指定して `Navigated` アドレスバーを更新でき `Url` `DocumentTitle` ます。  
  
 アプリケーション内で独自のページコンテンツを生成する場合は、プロパティを設定でき `DocumentText` ます。 HTML ドキュメントオブジェクトモデル (DOM) に慣れている場合は、プロパティを使用して現在の Web ページの内容を操作することもでき `Document` ます。 このプロパティを使用すると、ファイル間を移動する代わりに、メモリ内のドキュメントを格納および変更できます。  
  
 `Document`また、プロパティを使用すると、クライアントアプリケーションコードから Web ページスクリプトコードに実装されているメソッドを呼び出すこともできます。 スクリプトコードからクライアントアプリケーションコードにアクセスするには、プロパティを設定し `ObjectForScripting` ます。 指定したオブジェクトは、スクリプトコードによってオブジェクトとしてアクセスでき `window.external` ます。  
  
|名前|説明|  
|----------|-----------------|  
|<xref:System.Windows.Forms.WebBrowser.Document%2A> プロパティ|現在の Web ページの HTML ドキュメントオブジェクトモデル (DOM) へのマネージアクセスを提供するオブジェクトを取得します。|  
|<xref:System.Windows.Forms.WebBrowser.DocumentCompleted> イベント|Web ページの読み込みが終了したときに発生します。|  
|<xref:System.Windows.Forms.WebBrowser.DocumentText%2A> プロパティ|現在の Web ページの HTML コンテンツを取得または設定します。|  
|<xref:System.Windows.Forms.WebBrowser.DocumentTitle%2A> プロパティ|現在の Web ページのタイトルを取得します。|  
|<xref:System.Windows.Forms.WebBrowser.GoBack%2A> メソッド|履歴内の前のページに移動します。|  
|<xref:System.Windows.Forms.WebBrowser.GoForward%2A> メソッド|履歴の次のページに移動します。|  
|<xref:System.Windows.Forms.WebBrowser.Navigate%2A> メソッド|指定された URL に移動します。|  
|<xref:System.Windows.Forms.WebBrowser.Navigating> イベント|ナビゲーションが開始される前に発生し、アクションをキャンセルできるようにします。|  
|<xref:System.Windows.Forms.WebBrowser.ObjectForScripting%2A> プロパティ|Web ページスクリプトコードがアプリケーションとの通信に使用できるオブジェクトを取得または設定します。|  
|<xref:System.Windows.Forms.WebBrowser.Print%2A> メソッド|現在の Web ページを印刷します。|  
|<xref:System.Windows.Forms.WebBrowser.Refresh%2A> メソッド|現在の Web ページを再読み込みします。|  
|<xref:System.Windows.Forms.WebBrowser.Stop%2A> メソッド|現在のナビゲーションを停止し、サウンドやアニメーションなどの動的なページ要素を停止します。|  
|<xref:System.Windows.Forms.WebBrowser.Url%2A> プロパティ|現在の Web ページの URL を取得または設定します。 このプロパティを設定すると、コントロールが新しい URL に移動します。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.WebBrowser>
- <xref:System.Windows.Forms.WebBrowserDocumentCompletedEventArgs>
- <xref:System.Windows.Forms.WebBrowserDocumentCompletedEventHandler>
- <xref:System.Windows.Forms.WebBrowserEncryptionLevel>
- <xref:System.Windows.Forms.WebBrowserNavigatedEventArgs>
- <xref:System.Windows.Forms.WebBrowserNavigatedEventHandler>
- <xref:System.Windows.Forms.WebBrowserNavigatingEventArgs>
- <xref:System.Windows.Forms.WebBrowserNavigatingEventHandler>
- <xref:System.Windows.Forms.WebBrowserProgressChangedEventArgs>
- <xref:System.Windows.Forms.WebBrowserReadyState>
- <xref:System.Windows.Forms.WebBrowserRefreshOption>
- [方法: WebBrowser コントロールで URL に移動する](how-to-navigate-to-a-url-with-the-webbrowser-control.md)
- [方法: WebBrowser コントロールを使用して印刷する](how-to-print-with-a-webbrowser-control.md)
- [方法: Windows フォーム アプリケーションに Web ブラウザーの機能を追加する](how-to-add-web-browser-capabilities-to-a-windows-forms-application.md)
- [方法: Windows フォーム アプリケーションで HTML ドキュメントビューアーを作成する](how-to-create-an-html-document-viewer-in-a-windows-forms-application.md)
- [方法: DHTML コードとクライアント アプリケーション コード間の双方向の通信を実装する](implement-two-way-com-between-dhtml-and-client.md)
- [WebBrowser セキュリティ](webbrowser-security.md)
