---
title: '方法: Visual Studio を構成して Web サービスを呼び出す XAML ブラウザー アプリケーションをデバッグする'
ms.date: 03/30/2017
helpviewer_keywords:
- debugging XBAPs that call a Web service [WPF]
- debugging security exceptions for XBAPs [WPF]
- security exception for XBAPs [WPF], debugging
- configuring Visual Studio to debug XAML browser applications [WPF]
- configuring Visual Studio to debug XBAPs [WPF]
ms.assetid: fd1db082-a7bb-4c4b-9331-6ad74a0682d0
ms.openlocfilehash: d8cfae2fb47876d578c51e5f4acdfe0c31e752fe
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73460905"
---
# <a name="how-to-configure-visual-studio-to-debug-a-xaml-browser-application-to-call-a-web-service"></a>方法: Visual Studio を構成して Web サービスを呼び出す XAML ブラウザー アプリケーションをデバッグする
XAML ブラウザー アプリケーション (XBAP) は、インターネット ゾーン アクセス許可セットに制限された部分信頼セキュリティ サンドボックス内で実行されます。 このアクセス許可セットでは、Web サービスの呼び出しが、XBAP アプリケーションの起点サイトにある Web サービスのみに制限されます。 ただし、XBAP が Visual Studio 2005 からデバッグされている場合、それが参照している Web サービスと同じ起点サイトであるとは見なされません。 これにより、XBAP が Web サービスを呼び出そうとすると、セキュリティ例外が発生します。 ただし、Visual Studio 2005 XAML ブラウザー アプリケーション (WPF) プロジェクトは、デバッグ中に呼び出される Web サービスと同じ起点サイトを持つことをシミュレートするように構成できます。 これにより、XBAP では、セキュリティ例外を発生させることなく、Web サービスを安全に呼び出すことができます。

## <a name="configuring-visual-studio"></a>Visual Studio の構成
 Web サービスを呼び出す XBAP をデバッグするように Visual Studio 2005 を構成するには:

1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **プロジェクト デザイナー**で、 **[デバッグ]** タブをクリックします。

3. **[開始動作]** セクションで **[外部プログラムの開始]** を選択し、次のように入力します。

     `C:\WINDOWS\System32\PresentationHost.exe`

4. **[開始オプション]** セクションで、 **[コマンドライン引数]** テキスト ボックスに次のように入力します。

     `-debug`  *filename*

     **-debug** パラメーターの *filename* の値は、.xbap ファイル名です。次はその例です。

     `-debug c:\example.xbap`

> [!NOTE]
> これは、Visual Studio 2005 XAML ブラウザー アプリケーション (WPF) プロジェクト テンプレートで作成されるソリューションの既定の構成です。

1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **プロジェクト デザイナー**で、 **[デバッグ]** タブをクリックします。

3. **[開始オプション]** セクションで、次のコマンド ライン パラメーターを **[コマンドライン引数]** テキスト ボックスに追加します。

     `-debugSecurityZoneURL`  *URL*

     **-debugSecurityZoneURL** パラメーターの *URL* の値は、アプリケーションの起点サイトとしてシミュレートする場所の URL です。

 例として、次の URL の Web サービスを使用する XAML ブラウザー アプリケーション (XBAP) を考えてみます。

 `http://services.msdn.microsoft.com/ContentServices/ContentService.asmx`

 この Web サービスの起点サイト URL は次のとおりです。

 `http://services.msdn.microsoft.com`

 その結果、完全な **-debugSecurityZoneURL** コマンド ライン パラメーターと値は次のようになります。

 `-debugSecurityZoneURL http://services.msdn.microsoft.com`

## <a name="see-also"></a>関連項目

- [WPF ホスト (PresentationHost.exe)](wpf-host-presentationhost-exe.md)
