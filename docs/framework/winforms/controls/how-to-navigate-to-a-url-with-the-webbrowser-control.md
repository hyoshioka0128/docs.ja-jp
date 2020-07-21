---
title: '方法: WebBrowser コントロールで URL に移動する'
description: Windows フォーム WebBrowser コントロールを使用して特定の URL に移動する方法について説明します。 また、新しいドキュメントが読み込まれるタイミングを確認する方法についても説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
f1_keywords:
- WebBrowser.Navigate
helpviewer_keywords:
- WebBrowser control [Windows Forms], examples
- URLs [Windows Forms], navigating to
- WebBrowser control [Windows Forms], navigating to URLs
- examples [Windows Forms], WebBrowser control
ms.assetid: b3ec38cb-f509-4d0b-bd79-9f3611259c62
ms.openlocfilehash: e6ad360cc73a84ca040869832bb59d354cb78bd5
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325567"
---
# <a name="how-to-navigate-to-a-url-with-the-webbrowser-control"></a>方法: WebBrowser コントロールで URL に移動する
コントロールを特定の URL に移動する方法を次のコード例に示し <xref:System.Windows.Forms.WebBrowser> ます。

 新しいドキュメントが完全に読み込まれたことを確認するには、イベントを処理し <xref:System.Windows.Forms.WebBrowser.DocumentCompleted> ます。 このイベントのデモンストレーションについては、「[方法: WebBrowser コントロールで印刷](how-to-print-with-a-webbrowser-control.md)する」を参照してください。

## <a name="example"></a>例

```vb
Me.webBrowser1.Navigate("https://www.microsoft.com")
```

```csharp
this.webBrowser1.Navigate("https://www.microsoft.com");
```

## <a name="compiling-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- `webBrowser1` という名前の <xref:System.Windows.Forms.WebBrowser> コントロール。

- `System` アセンブリおよび `System.Windows.Forms` アセンブリへの参照。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.WebBrowser>
- <xref:System.Windows.Forms.WebBrowser.DocumentCompleted?displayProperty=nameWithType>
- <xref:System.Windows.Forms.WebBrowser.Navigating?displayProperty=nameWithType>
- <xref:System.Windows.Forms.WebBrowser.Navigated?displayProperty=nameWithType>
- [WebBrowser コントロール](webbrowser-control-windows-forms.md)
- [方法: WebBrowser コントロールを使用して印刷する](how-to-print-with-a-webbrowser-control.md)
