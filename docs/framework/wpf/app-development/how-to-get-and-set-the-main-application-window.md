---
title: '方法: メイン アプリケーション ウィンドウを取得して設定する'
description: 次の例に従って、Windows Presentation Foundation (WPF) アプリケーション内でメイン アプリケーション ウィンドウを取得して設定します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- windows objects [WPF], setting
- setting windows objects [WPF]
- windows objects [WPF], getting
- getting windows objects [WPF]
ms.assetid: ec902bc4-4a59-46f5-8ec1-963b46789356
ms.openlocfilehash: 9bb5bce9b90482796acd8c62e77dc8bd9a850eeb
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622680"
---
# <a name="how-to-get-and-set-the-main-application-window"></a>方法: メイン アプリケーション ウィンドウを取得して設定する
この例では、メイン アプリケーション ウィンドウを取得および設定する方法を示します。  
  
## <a name="example"></a>例  
 Windows Presentation Foundation (WPF) アプリケーション内で最初にインスタンス化された <xref:System.Windows.Window> は、<xref:System.Windows.Application> によってメイン アプリケーション ウィンドウとして自動的に設定されます。 通常、最初にインスタンス化される <xref:System.Windows.Window> は、スタートアップ URI (Uniform Resource Identifier) として指定されているウィンドウです (「<xref:System.Windows.Application.StartupUri%2A>」を参照)。  
  
 最初の <xref:System.Windows.Window> は、コードを使用してインスタンス化することもできます。 1 つの例として、次のように、アプリケーションの起動時にウィンドウを開くことがあります。  
  
 [!code-csharp[HOWTOWindowManagementSnippets#FirstWindowUsingCodeCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/App.xaml.cs#firstwindowusingcodecodebehind)]
 [!code-vb[HOWTOWindowManagementSnippets#FirstWindowUsingCodeCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/application.xaml.vb#firstwindowusingcodecodebehind)]  
  
 場合によっては、最初にインスタンス化される <xref:System.Windows.Window> が、実際にはメイン アプリケーション ウィンドウではないことがあります (スプラッシュ スクリーンなど)。 この場合は、次のように、マークアップを使用してメイン アプリケーション ウィンドウを指定できます。  
  
 [!code-xaml[ApplicationMainWindowSnippets#SetApplicationMainWindowXAML](~/samples/snippets/xaml/VS_Snippets_Wpf/ApplicationMainWindowSnippets/XAML/App.xaml#setapplicationmainwindowxaml)]  
  
 メイン ウィンドウが自動または手動のどちらで指定されるかにかかわらず、次のようなコードを使用して、<xref:System.Windows.Application.MainWindow%2A> からメイン ウィンドウを取得できます。  
  
 [!code-csharp[ApplicationMainWindowSnippets#GetApplicationMainWindowCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationMainWindowSnippets/CSharp/App.xaml.cs#getapplicationmainwindowcode)]
 [!code-vb[ApplicationMainWindowSnippets#GetApplicationMainWindowCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationMainWindowSnippets/visualbasic/application.xaml.vb#getapplicationmainwindowcode)]
