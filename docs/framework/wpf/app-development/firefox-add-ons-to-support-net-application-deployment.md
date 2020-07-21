---
title: .NET アプリケーションの配置をサポートするための Firefox のアドオン
ms.date: 03/30/2017
helpviewer_keywords:
- Firefox add-ons for .NET application deployment
- WPF plug-in for Firefox
- .NET application deployment [WPF], deploying with Firefox add-ons
- .NET Framework Assistant for Firefox
ms.assetid: 2403403b-9b14-48e9-b70d-fa288a3c9081
ms.openlocfilehash: 56f5f633092d8aa0bfabdb0570ec26f14221838d
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2020
ms.locfileid: "77124612"
---
# <a name="firefox-add-ons-to-support-net-application-deployment"></a>.NET アプリケーションの配置をサポートするための Firefox のアドオン
Firefox 用 Windows Presentation Foundation (WPF) プラグインと Firefox 用 .NET Framework Assistant を使用すると、XAML ブラウザー アプリケーション (XBAP)、Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]、ClickOnce アプリケーションが、Mozilla Firefox ブラウザーで動作できるようになります。  
  
## <a name="wpf-plug-in-for-firefox"></a>Firefox に対応した WPF プラグイン  
 Firefox 用 WPF プラグインを使用すると、XBAP および Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルは、Firefox ブラウザーでナビゲートしたり、最上位または HTML IFRAME で実行したりできます。 XBAP は、Web サーバーに発行して、サポートされているブラウザー内で起動できる WPF アプリケーションです。 Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] は、XML ファイルのように、ナビゲートしたり、サポートされているブラウザーで表示したりできる、XAML のみのファイルです。  
  
 Firefox 用 WPF プラグインは、.NET Framework 3.5 でインストールされます。 Windows 7 には .NET Framework 3.5 が含まれていますが、Firefox 用 WPF プラグインは含まれていません。 Firefox 用 WPF プラグインを Windows 7 にインストールすることはできません。  
  
 .NET Framework 4 には、Firefox 用 WPF プラグインは含まれていません。 ただし、.NET Framework 3.5 と .NET Framework 4 の両方がインストールされている場合は、.NET Framework 3.5 で Firefox 用 WPF プラグインがインストールされます。 したがって、WPF ホストで正しいバージョンのフレームワークが読み込まれるため、.NET Framework 4 アプリケーションはやはり実行されます。 詳細については、「[WPF ホスト (PresentationHost.exe)](wpf-host-presentationhost-exe.md)」を参照してください。  
  
## <a name="net-framework-assistant-for-firefox"></a>.NET Framework Assistant for Firefox  
 Firefox 用 .NET Framework Assistant を使用すると、スタンドアロンの ClickOnce アプリケーションを Firefox ブラウザーから実行できます。 Firefox 用 .NET Framework Assistant は、Firefox ブラウザーの前と後どちらでインストールされても、同じように機能します。 Firefox ブラウザーが起動されたときに、.NET Framework 3.5 SP1 がインストールされていると、Firefox によって .NET Framework Assistant が検出されてインストールされます。 ユーザーは、Firefox 用 .NET Framework Assistant を次のように構成できます。  
  
- ClickOnce アプリケーションを実行する前にプロンプトを表示する。  
  
- .NET Framework のインストールされている全バージョンまたは最新バージョンのみを報告する。  
  
 Firefox 用 .NET Framework Assistant は、.NET Framework 3.5 SP1 に含まれています。 Firefox 用 .NET Framework Assistant の削除については、「[Firefox 用 .NET Framework Assistant を削除する方法](https://support.microsoft.com/help/963707/how-to-remove-the-net-framework-assistant-for-firefox)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [WPF アプリケーションの配置](deploying-a-wpf-application-wpf.md)
- [WPF XAML ブラウザー アプリケーションの概要](wpf-xaml-browser-applications-overview.md)
- [Firefox に対応した WPF プラグインがインストールされているかどうかを確認する](how-to-detect-whether-the-wpf-plug-in-for-firefox-is-installed.md)
