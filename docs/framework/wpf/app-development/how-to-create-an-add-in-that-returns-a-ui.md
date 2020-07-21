---
title: '方法: UI を返すアドインを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- creating an add-in that returns a UI [WPF]
- implementing add-in pipeline segments [WPF]
- add-in [WPF], returns a UI
ms.assetid: 57f274b7-4c66-4b72-92eb-81939a393776
ms.openlocfilehash: f8323fe35555a56d39c1efed649c2aa3fcf17e43
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174590"
---
# <a name="how-to-create-an-add-in-that-returns-a-ui"></a>方法: UI を返すアドインを作成する
この例では、ホスト WPF スタンドアロン アプリケーションに Windows Presentation Foundation (WPF) を返すアドインの作成方法を示します。  
  
 このアドインは、WPF ユーザー コントロールである UI を返します。 ユーザー コントロールの中身は 1 つのボタンであり、クリックすると、メッセージ ボックスを表示します。 WPF スタンドアロン アプリケーションは、アドインをホストし、(アドインによって返された) ユーザー コントロールをメイン アプリケーション ウィンドウのコンテンツとして表示します。  
  
 **必須コンポーネント**  
  
 この例では、このシナリオを実現する .NET Framework アドイン モデルの WPF 拡張機能に焦点を当てます。前提条件は、次のとおりです。  
  
- パイプライン、アドイン、ホスト環境など、.NET Framework アドイン モデルの知識。 これらの概念については、「[アドインおよび拡張機能](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))」を参照してください。 パイプライン、アドイン、およびホスト アプリケーションの実装例を示すチュートリアルについては、「[チュートリアル: 拡張性のあるアプリケーションの作成](/previous-versions/dotnet/netframework-4.0/bb788290(v%3dvs.100))」を参照してください。  
  
- .NET Framework アドイン モデルの WPF 拡張機能については、「[WPF アドインの概要](wpf-add-ins-overview.md)」を参照してください。  
  
## <a name="example"></a>例  
 WPF UI を返すアドインを作成するには、各パイプライン セグメント、アドイン、およびホスト アプリケーションに特定のコードが必要です。  

<a name="Contract"></a>
## <a name="implementing-the-contract-pipeline-segment"></a>コントラクト パイプライン セグメントの実装  
 メソッドは、UI を返すようにコントラクトによって定義する必要があり、その戻り値は <xref:System.AddIn.Contract.INativeHandleContract> 型でなければなりません。 これは、次のコードの `IWPFAddInContract` コントラクトの `GetAddInUI` メソッドによって示されています。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#ContractCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/Contracts/IWPFAddInContract.cs#contractcode)]
 [!code-vb[SimpleAddInReturnsAUISample#ContractCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/Contracts/IWPFAddInContract.vb#contractcode)]  
  
<a name="AddInView"></a>
## <a name="implementing-the-add-in-view-pipeline-segment"></a>アドイン ビュー パイプライン セグメントの実装  
 アドインでは UI が実装されていて、それが <xref:System.Windows.FrameworkElement> のサブクラスとして提供されるため、`IWPFAddInView.GetAddInUI` に関連するアドイン ビューのメソッドは、<xref:System.Windows.FrameworkElement> 型の値を返す必要があります。 次のコードは、コントラクトのアドイン ビューがインターフェイスとして実装されることを示しています。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInViewCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/AddInViews/IWPFAddInView.cs#addinviewcode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInViewCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/AddInViews/IWPFAddInView.vb#addinviewcode)]  
  
<a name="AddInSideAdapter"></a>
## <a name="implementing-the-add-in-side-adapter-pipeline-segment"></a>アドイン側アダプター パイプライン セグメントの実装  
 コントラクト メソッドでは <xref:System.AddIn.Contract.INativeHandleContract> が返されますが、アドインでは <xref:System.Windows.FrameworkElement> が返されます (アドイン ビューによって指定されたように)。 したがって、<xref:System.Windows.FrameworkElement> は、分離境界を越える前に <xref:System.AddIn.Contract.INativeHandleContract> に変換される必要があります。 この作業は、次のコードで示されているように、アドイン側のアダプターで <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> を呼び出すことによって行われます。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInSideAdapterCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.cs#addinsideadaptercode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInSideAdapterCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/AddInSideAdapters/WPFAddIn_ViewToContractAddInSideAdapter.vb#addinsideadaptercode)]  
  
<a name="HostView"></a>
## <a name="implementing-the-host-view-pipeline-segment"></a>ホスト ビュー パイプライン セグメントの実装  
 ホスト アプリケーションでは <xref:System.Windows.FrameworkElement> が表示されるため、`IWPFAddInHostView.GetAddInUI` に関連するホスト ビューのメソッドでは、<xref:System.Windows.FrameworkElement> 型の値を返す必要があります。 次のコードは、コントラクトのホスト ビューがインターフェイスとして実装されることを示しています。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#HostViewCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/HostViews/IWPFAddInHostView.cs#hostviewcode)]
 [!code-vb[SimpleAddInReturnsAUISample#HostViewCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/HostViews/IWPFAddInHostView.vb#hostviewcode)]  
  
<a name="HostSideAdapter"></a>
## <a name="implementing-the-host-side-adapter-pipeline-segment"></a>ホスト側アダプター パイプライン セグメントの実装  
 コントラクト メソッドでは <xref:System.AddIn.Contract.INativeHandleContract> が返されますが、ホスト アプリケーションでは <xref:System.Windows.FrameworkElement> が必要です (ホスト ビューによって指定されたように)。 したがって、<xref:System.AddIn.Contract.INativeHandleContract> は、分離境界を越えた後で、<xref:System.Windows.FrameworkElement> に変換される必要があります。 この作業は、次のコードで示されているように、ホスト側のアダプターで <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> を呼び出すことによって行われます。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#HostSideAdapterCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.cs#hostsideadaptercode)]
 [!code-vb[SimpleAddInReturnsAUISample#HostSideAdapterCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/HostSideAdapters/WPFAddIn_ContractToViewHostSideAdapter.vb#hostsideadaptercode)]  
  
<a name="AddIn"></a>
## <a name="implementing-the-add-in"></a>アドインの実装  
 アドイン側アダプターとアドイン ビューが作成されたら、アドイン (`WPFAddIn1.AddIn`) では、<xref:System.Windows.FrameworkElement> オブジェクト (この例では、<xref:System.Windows.Controls.UserControl>) を返すために `IWPFAddInView.GetAddInUI` メソッドを実装する必要があります。 <xref:System.Windows.Controls.UserControl> (`AddInUI`) の実装を次のコードに示します。  
  
 [!code-xaml[SimpleAddInReturnsAUISample#AddInUIMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddInUI.xaml#addinuimarkup)]  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInUICodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddInUI.xaml.cs#addinuicodebehind)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInUICodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/WPFAddIn1/AddInUI.xaml.vb#addinuicodebehind)]  
  
 アドインによる `IWPFAddInView.GetAddInUI` の実装は、次のコードに示されているように、`AddInUI` の新しいインスタンスだけを返す必要があります。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#AddInCode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/WPFAddIn1/AddIn.cs#addincode)]
 [!code-vb[SimpleAddInReturnsAUISample#AddInCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/WPFAddIn1/AddIn.vb#addincode)]  
  
<a name="App"></a>
## <a name="implementing-the-host-application"></a>ホスト アプリケーションの実装  
 ホスト側のアダプターとホスト ビューが作成されると、ホスト アプリケーションは .NET Framework アドイン モデルを使用して、パイプラインを開き、アドインのホスト ビューを取得し、`IWPFAddInHostView.GetAddInUI` メソッドを呼び出すことができます。 これらの手順を次のコードに示します。  
  
 [!code-csharp[SimpleAddInReturnsAUISample#GetUICode](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/CSharp/Host/MainWindow.xaml.cs#getuicode)]
 [!code-vb[SimpleAddInReturnsAUISample#GetUICode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleAddInReturnsAUISample/VisualBasic/Host/MainWindow.xaml.vb#getuicode)]  
  
## <a name="see-also"></a>関連項目

- [アドインおよび拡張機能](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))
- [WPF のアドインの概要](wpf-add-ins-overview.md)
