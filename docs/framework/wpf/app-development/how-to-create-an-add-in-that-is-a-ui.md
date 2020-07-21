---
title: '方法: UI であるアドインを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- creating an add-in that is a UI [WPF]
- add-ins [WPF], UI
- creating UI add-ins [WPF]
- UI add-ins [WPF], creating
- implementing UI add-ins [WPF]
- pipeline segments [WPF], creating add-ins
ms.assetid: 86375525-282b-4039-8352-8680051a10ea
ms.openlocfilehash: 339231031b9e57b9f00a2aeb6fbbde8ad66c1ad9
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141030"
---
# <a name="how-to-create-an-add-in-that-is-a-ui"></a>方法: UI であるアドインを作成する
この例では、WPF スタンドアロン アプリケーションによってホストされる、Windows Presentation Foundation (WPF) であるアドインを作成する方法を示します。  
  
 このアドインは、WPF ユーザー コントロール である UI です。 ユーザー コントロールの中身は 1 つのボタンであり、クリックすると、メッセージ ボックスを表示します。 WPF スタンドアロン アプリケーションでは、メイン アプリケーション ウィンドウのコンテンツとして、アドイン UI がホストされます。  
  
 **必須コンポーネント**  
  
 この例では、このシナリオを実現する .NET Framework アドイン モデルの WPF 拡張機能に焦点を当てます。前提条件は、次のとおりです。  
  
- パイプライン、アドイン、ホスト環境など、.NET Framework アドイン モデルの知識。 これらの概念については、「[アドインおよび拡張機能](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))」を参照してください。 パイプライン、アドイン、およびホスト アプリケーションの実装例を示すチュートリアルについては、「[チュートリアル: 拡張性のあるアプリケーションの作成](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb788290(v%3dvs.100))」を参照してください。  
  
- .NET Framework アドイン モデルに対する WPF 拡張機能の知識。 「[WPF のアドインの概要](wpf-add-ins-overview.md)」を参照してください。  
  
## <a name="example"></a>例  
 WPF UI であるアドインを作成するには、各パイプライン セグメント、アドイン、およびホスト アプリケーションに特定のコードが必要です。  

<a name="Contract"></a>
## <a name="implementing-the-contract-pipeline-segment"></a>コントラクト パイプライン セグメントの実装

アドインが UI のときは、アドインのコントラクトで <xref:System.AddIn.Contract.INativeHandleContract> を実装する必要があります。 次のコードに示すように、この例では、`IWPFAddInContract` で <xref:System.AddIn.Contract.INativeHandleContract> が実装されています。  
  
[!code-csharp[SimpleAddInIsAUISample#ContractCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/Contracts/IWPFAddInContract.cs#contractcode)]
[!code-vb[SimpleAddInIsAUISample#ContractCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/Contracts/IWPFAddInContract.vb#contractcode)]

<a name="AddInViewPipeline"></a>
## <a name="implementing-the-add-in-view-pipeline-segment"></a>アドイン ビュー パイプライン セグメントの実装

アドインは <xref:System.Windows.FrameworkElement> 型のサブクラスとして実装されるため、アドイン ビューも <xref:System.Windows.FrameworkElement> のサブクラスである必要があります。 次のコードでは、`WPFAddInView` クラスとして実装されるコントラクトのアドイン ビューを示します。  
  
[!code-csharp[SimpleAddInIsAUISample#AddInViewCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/AddInViews/WPFAddInView.cs#addinviewcode)]  
[!code-vb[SimpleAddInIsAUISample#AddInViewCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/AddInViews/WPFAddInView.vb#AddInViewCode)]  
  
ここでは、アドイン ビューは <xref:System.Windows.Controls.UserControl> から派生します。 したがって、アドイン UI も <xref:System.Windows.Controls.UserControl> から派生する必要があります。  
  
<a name="AddInSideAdapter"></a>
## <a name="implementing-the-add-in-side-adapter-pipeline-segment"></a>アドイン側アダプター パイプライン セグメントの実装

コントラクトは <xref:System.AddIn.Contract.INativeHandleContract> ですが、アドインは <xref:System.Windows.FrameworkElement> です (アドイン ビュー パイプライン セグメントによって指定されたように)。 したがって、<xref:System.Windows.FrameworkElement> は、分離境界を越える前に <xref:System.AddIn.Contract.INativeHandleContract> に変換される必要があります。 この作業は、次のコードで示されているように、アドイン側のアダプターで <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> を呼び出すことによって行われます。  
  
[!code-csharp[SimpleAddInIsAUISample#AddInSideAdapterCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.cs#addinsideadaptercode)]  
[!code-vb[SimpleAddInIsAUISample#AddInSideAdapterCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.vb#addinsideadaptercode)]

アドインで UI が返されるアドイン モデルでは (「[UI を返すアドインを作成する](how-to-create-an-add-in-that-returns-a-ui.md)」を参照)、アドイン アダプターで <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> を呼び出すことによって、<xref:System.Windows.FrameworkElement> から <xref:System.AddIn.Contract.INativeHandleContract> に変換されます。 このモデルでは、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> も呼び出す必要がありますが、これを呼び出すコードを記述するメソッドを実装する必要があります。 このためには、<xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> を呼び出すコードで <xref:System.AddIn.Contract.INativeHandleContract> が予期されている場合は、<xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> をオーバーライドして、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> を呼び出すコードを実装します。 この場合、呼び出し元はホスト側のアダプターであり、これについては、後で説明します。  
  
> [!NOTE]
> このモデルでは、<xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> もオーバーライドして、ホスト アプリケーション UI とアドイン UI の間を Tab キーで移動できるようにする必要があります。 詳細については、「[WPF アドインの概要](wpf-add-ins-overview.md)」の「WPF アドインの制約」を参照してください。  
  
アドイン側のアダプターでは <xref:System.AddIn.Contract.INativeHandleContract> から派生するインターフェイスを実装するため、<xref:System.AddIn.Contract.INativeHandleContract.GetHandle%2A> を実装する必要もありますが、<xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> がオーバーライドされるときは、これは無視されます。  
  
<a name="HostViewPipeline"></a>
## <a name="implementing-the-host-view-pipeline-segment"></a>ホスト ビュー パイプライン セグメントの実装

このモデルのホスト アプリケーションでは、通常、ホスト ビューが <xref:System.Windows.FrameworkElement> サブクラスであることが予期されています。 ホスト側アダプターでは、<xref:System.AddIn.Contract.INativeHandleContract> が分離境界を越えた後で、<xref:System.AddIn.Contract.INativeHandleContract> を <xref:System.Windows.FrameworkElement> に変換する必要があります。 <xref:System.Windows.FrameworkElement> を取得するためにホスト アプリケーションによってメソッドは呼び出されていないため、ホスト ビューでは、<xref:System.Windows.FrameworkElement> を格納することによって、"返す" 必要があります。 したがって、ホスト ビューは、<xref:System.Windows.Controls.UserControl> など、他の UI を格納できる <xref:System.Windows.FrameworkElement> のサブクラスから派生する必要があります。 次のコードでは、`WPFAddInHostView` クラスとして実装されるコントラクトのホスト ビューを示します。  

[!code-csharp[WPFAddInHostView class](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/HostViews/WPFAddInHostView.cs#HostViewCode)]
[!code-vb[WPFAddInHostView class](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/HostViews/WPFAddInHostView.vb#HostViewCode)]

<a name="HostSideAdapter"></a>
## <a name="implementing-the-host-side-adapter-pipeline-segment"></a>ホスト側アダプター パイプライン セグメントの実装

コントラクトは <xref:System.AddIn.Contract.INativeHandleContract> ですが、ホスト アプリケーションでは <xref:System.Windows.Controls.UserControl> が予期されています (ホスト ビューによって指定されたように)。 したがって、<xref:System.AddIn.Contract.INativeHandleContract> は、分離境界を越えた後、ホスト ビューのコンテンツ (<xref:System.Windows.Controls.UserControl> から派生) として設定される前に、<xref:System.Windows.FrameworkElement> に変換される必要があります。  
  
この作業は、次のコードに示されているように、ホスト側アダプターによって行われます。  

[!code-csharp[Host-side adapter](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.cs#HostSideAdapterCode)]
[!code-vb[Host-side adapter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.vb#HostSideAdapterCode)]

このことからもわかるように、ホスト側のアダプターは、アドイン側のアダプターの <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> メソッドを呼び出すことによって、<xref:System.AddIn.Contract.INativeHandleContract> を取得します (ここが <xref:System.AddIn.Contract.INativeHandleContract> が分離境界を越えるポイントです)。  
  
その後、ホスト側のアダプターでは、<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> を呼び出すことによって、<xref:System.AddIn.Contract.INativeHandleContract> が <xref:System.Windows.FrameworkElement> に変換されます。 最後に、<xref:System.Windows.FrameworkElement> がホスト ビューのコンテンツとして設定されます。  
  
<a name="AddIn"></a>
## <a name="implementing-the-add-in"></a>アドインの実装

アドイン側アダプターとアドイン ビューが用意できると、次のコードに示されているように、アドイン ビューから派生することでアドインを実装できます。  

[!code-csharp[Add-in implementation](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/WPFAddIn1/AddInUI.xaml.cs#AddInCodeBehind)]
[!code-vb[Add-in implementation](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/WPFAddIn1/AddInUI.xaml.vb#AddInCodeBehind)]

この例から、このモデルの興味深い利点がわかります。つまり、アドイン開発者は、アドインだけを実装すればよく (これが UI でもあるため)、アドイン クラスとアドイン UI の両方を実装する必要はありません。  
  
<a name="HostApp"></a>
## <a name="implementing-the-host-application"></a>ホスト アプリケーションの実装

ホスト側のアダプターとホスト ビューが作成されると、ホスト アプリケーションは .NET Framework アドイン モデルを使用して、パイプラインを開き、アドインのホスト ビューを取得できます。 これらの手順を次のコードに示します。  

[!code-csharp[Acquiring a host view of the add-in](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInIsAUISample/CSharp/Host/MainWindow.xaml.cs#GetUICode)]
[!code-vb[Acquiring a host view of the add-in](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInIsAUISample/VisualBasic/Host/MainWindow.xaml.vb#GetUICode)]

ホスト アプリケーションでは、一般的な .NET Framework アドイン モデル コードを使用して、アドインをアクティブ化し、このアドインは、ホスト ビューをホスト アプリケーションに暗黙的に返します。 その後、ホスト アプリケーションはホスト ビュー (<xref:System.Windows.Controls.UserControl>) を <xref:System.Windows.Controls.Grid> から表示します。  
  
 アドイン UI との対話を処理するコードは、アドインのアプリケーション ドメインで実行します。 このような対話には、次のようなものがあります。  
  
- <xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントの処理。  
  
- <xref:System.Windows.MessageBox> の表示。  
  
 このアクティビティは、ホスト アプリケーションから完全に分離されています。  
  
## <a name="see-also"></a>関連項目

- [アドインおよび拡張機能](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))
- [WPF のアドインの概要](wpf-add-ins-overview.md)
