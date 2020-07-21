---
title: XAML からの読み込み
ms.date: 03/30/2017
ms.assetid: 1f103ef6-7bed-4f16-ae52-9e665c5a43d7
ms.openlocfilehash: d07ddef8fb982aa0bf707cb688cd23f04bb231d5
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142720"
---
# <a name="load-from-xaml"></a>XAML からの読み込み
このサンプルでは、XamlBuildTask ツールを実行することなく、XAML ワークフローを動的に読み込む方法を示します。 代わりに、このサンプルでは <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> メソッドを呼び出します。 サンプルは、<xref:System.Activities.XamlIntegration.ActivityXamlServices>クラスを使用して XAML ワークフローを読み込み、それらを実行する Windows プレゼンテーション ファンデーション (WPF) クライアント アプリケーションです。 <xref:System.Activities.XamlIntegration.ActivityXamlServices> クラスを使用して XAML ワークフローが読み込まれると、実行可能な <xref:System.Activities.DynamicActivity%601> が返されます。

#### <a name="to-use-this-sample"></a>このサンプルを使用するには

1. Visual Studio 2010 を使用して、読み込み元 XAML.sln ソリューション ファイルを開きます。

2. ソリューションをビルドするには、Ctrl キーと Shift キーを押しながら B キーを押します。

3. ソリューションを実行するには、Ctrl キーを押しながら F5 キーを押します。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Built-InActivities\DynamicActivity\LoadFromXAML`
