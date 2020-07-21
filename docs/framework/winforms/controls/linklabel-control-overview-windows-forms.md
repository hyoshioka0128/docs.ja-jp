---
title: LinkLabel コントロールの概要
ms.date: 03/30/2017
f1_keywords:
- LinkLabel
helpviewer_keywords:
- links [Windows Forms], LinkLabel control
- Label control [Windows Forms], about Label control
- LinkLabel control [Windows Forms], about LinkLabel control
ms.assetid: 9e248549-10ca-43a3-bb5e-60f583d369f1
ms.openlocfilehash: 3e8607644c858ae804e384c974b5e81c1786c6a1
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81739521"
---
# <a name="linklabel-control-overview-windows-forms"></a>LinkLabel コントロールの概要 (Windows フォーム)
Windows フォーム<xref:System.Windows.Forms.LinkLabel>コントロールを使用すると、Web スタイルのリンクを Windows フォーム アプリケーションに追加できます。 コントロールを<xref:System.Windows.Forms.LinkLabel>使用できるすべてのものに対してコントロールを<xref:System.Windows.Forms.Label>使用できます。テキストの一部をファイル、フォルダ、または Web ページへのリンクとして設定することもできます。  
  
## <a name="what-you-can-do-with-the-linklabel-control"></a>リンクラベル コントロールで実行できる操作  
 コントロールには、コントロールのすべてのプロパティ、メソッド、およびイベントのほかに<xref:System.Windows.Forms.Label>、ハイパーリンクとリンクの色のプロパティがあります。 <xref:System.Windows.Forms.LinkLabel> この<xref:System.Windows.Forms.LinkLabel.LinkArea%2A>プロパティは、リンクをアクティブにするテキストの領域を設定します。 <xref:System.Windows.Forms.LinkLabel.LinkColor%2A>、、<xref:System.Windows.Forms.LinkLabel.VisitedLinkColor%2A>および<xref:System.Windows.Forms.LinkLabel.ActiveLinkColor%2A>プロパティはリンクの色を設定します。 イベント<xref:System.Windows.Forms.LinkLabel.LinkClicked>は、リンク テキストが選択されたときに何が起こるかを決定します。  
  
 コントロールの<xref:System.Windows.Forms.LinkLabel>最も簡単な使用方法は、 プロパティを使用して<xref:System.Windows.Forms.LinkLabel.LinkArea%2A>1 つのリンクを表示することですが、 プロパティを<xref:System.Windows.Forms.LinkLabel.Links%2A>使用して複数のハイパーリンクを表示することもできます。 この<xref:System.Windows.Forms.LinkLabel.Links%2A>プロパティを使用すると、リンクのコレクションにアクセスできます。 個々の<xref:System.Windows.Forms.LinkLabel.Link>オブジェクトのプロパティでデータ<xref:System.Windows.Forms.LinkLabel.Link.LinkData%2A>を指定することもできます。 プロパティの<xref:System.Windows.Forms.LinkLabel.Link.LinkData%2A>値は、表示するファイルの場所や Web サイトのアドレスを格納するために使用できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.LinkLabel>
- [Label コントロールの概要](label-control-overview-windows-forms.md)
- [方法: Windows フォーム LinkLabel コントロールでオブジェクトまたは Web ページにリンクする](link-to-an-object-or-web-page-with-wf-linklabel-control.md)
- [方法: Windows フォーム LinkLabel コントロールの表示形式を変更する](how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)
