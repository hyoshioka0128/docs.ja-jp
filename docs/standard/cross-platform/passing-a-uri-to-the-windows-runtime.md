---
title: Windows ランタイムへの URI の引き渡し
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Runtime, .NET Framework support for
- Windows Runtime, passing a URI to
ms.assetid: 3eb5ce6f-f304-4f87-8e81-0f25092f5ad4
ms.openlocfilehash: 7152fb02abf430c0d0e27b82550e4006e3958e93
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288889"
---
# <a name="passing-a-uri-to-the-windows-runtime"></a>Windows ランタイムへの URI の引き渡し
Windows ランタイムのメソッドは絶対 URI だけを受け取ります。 Windows ランタイムメソッドに相対 URI を渡すと、 <xref:System.ArgumentException> 例外がスローされます。 その理由: .NET Framework コードで Windows ランタイムを使用すると、クラスは <xref:Windows.Foundation.Uri?displayProperty=nameWithType> Intellisense でとして表示されます <xref:System.Uri?displayProperty=nameWithType> 。 クラスでは <xref:System.Uri?displayProperty=nameWithType> 相対 uri を使用でき <xref:Windows.Foundation.Uri?displayProperty=nameWithType> ますが、クラスでは許可されません。 これは、Windows ランタイムコンポーネントで公開するメソッドにも当てはまります。 URI を受け取るメソッドをコンポーネントで公開する場合、コードのシグネチャには <xref:System.Uri?displayProperty=nameWithType> が含まれます。 ただし、コンポーネントのユーザーには、という署名が含まれ <xref:Windows.Foundation.Uri?displayProperty=nameWithType> ます。 コンポーネントに渡す URI は、絶対 URI でなければなりません。  
  
このトピックでは、絶対 URI を検出する方法と、アプリ パッケージ内のリソースを参照するときに絶対 URI を作成する方法を説明します。  
  
## <a name="detecting-and-using-an-absolute-uri"></a>絶対 URI の検出と使用  
プロパティを使用して、 <xref:System.Uri.IsAbsoluteUri%2A?displayProperty=nameWithType> Windows ランタイムに渡す前に URI が絶対 URI であることを確認します。 このプロパティを使用する方が、<xref:System.ArgumentException> 例外をキャッチして処理するより効率的です。  
  
## <a name="using-an-absolute-uri-for-a-resource-in-the-app-package"></a>アプリ パッケージのリソースに対する絶対 URI の使用  
アプリのパッケージに含まれるリソースに対して URI を指定するには、`ms-appx` スキームまたは `ms-appx-web` スキームを使用して絶対 URI を作成します。  
  
次の例では、 <xref:Windows.UI.Xaml.Controls.WebView.Source%2A> <xref:Windows.UI.Xaml.Controls.WebView> <xref:Windows.UI.Xaml.Controls.Image.Source%2A> <xref:Windows.UI.Xaml.Controls.Image> XAML とコードの両方を使用して、コントロールのプロパティと、コントロールのプロパティを、Pages という名前のフォルダーに格納されているリソースに設定する方法を示します。  
  
[!code-xaml[System.URIToWindowsURI#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml#1)]  
[!code-csharp[System.URIToWindowsURI#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.uritowindowsuri/cs/mainpage.xaml.cs#2)]
[!code-vb[System.URIToWindowsURI#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.uritowindowsuri/vb/mainpage.xaml.vb#2)]  
  
これらのスキームの詳細については、Windows デベロッパー センターの「[URI スキーム](/windows/uwp/app-resources/uri-schemes)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Windows ストア アプリおよび Windows ランタイムのための .NET Framework サポート](support-for-windows-store-apps-and-windows-runtime.md)
