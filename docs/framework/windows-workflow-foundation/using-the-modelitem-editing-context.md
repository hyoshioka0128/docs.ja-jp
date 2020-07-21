---
title: ModelItem 編集コンテキストの使用
ms.date: 03/30/2017
ms.assetid: 7f9f1ea5-0147-4079-8eca-be94f00d3aa1
ms.openlocfilehash: e1481d96e39f837d72834222d2839c520e880cc6
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142515"
---
# <a name="using-the-modelitem-editing-context"></a>ModelItem 編集コンテキストの使用
<xref:System.Activities.Presentation.Model.ModelItem> 編集コンテキストは、ホスト アプリケーションがデザイナーとの通信に使用するオブジェクトです。 <xref:System.Activities.Presentation.EditingContext> は使用できる 2 つのメソッド <xref:System.Activities.Presentation.EditingContext.Items%2A> と <xref:System.Activities.Presentation.EditingContext.Services%2A> を公開します。  
  
## <a name="the-items-collection"></a>Items コレクション  
 <xref:System.Activities.Presentation.EditingContext.Items%2A> コレクションは、ホストとデザイナー間で共有されるデータ、またはすべてのデザイナーで使用可能なデータへのアクセスに使用されます。 このコレクションには、<xref:System.Activities.Presentation.ContextItemManager> クラスを介してアクセスされる次の機能があります。  
  
1. <xref:System.Activities.Presentation.ContextItemManager.GetValue%2A>  
  
2. <xref:System.Activities.Presentation.ContextItemManager.Subscribe%2A>  
  
3. <xref:System.Activities.Presentation.ContextItemManager.Unsubscribe%2A>  
  
4. <xref:System.Activities.Presentation.ContextItemManager.SetValue%2A>  
  
## <a name="the-services-collection"></a>Services コレクション  
 <xref:System.Activities.Presentation.EditingContext.Services%2A> コレクションは、デザイナーとホスト間の対話に使用されるサービス、またはすべてのデザイナーで使用されるサービスへのアクセスに使用されます。 このコレクションには、重要な次のメソッドがあります。  
  
1. <xref:System.Activities.Presentation.ServiceManager.Publish%2A>  
  
2. <xref:System.Activities.Presentation.ServiceManager.Subscribe%2A>  
  
3. <xref:System.Activities.Presentation.ServiceManager.Unsubscribe%2A>  
  
4. <xref:System.Activities.Presentation.ServiceManager.GetService%2A>  
  
## <a name="assigning-a-designer-an-activity"></a>デザイナーへのアクティビティの割り当て  
 アクティビティで使用されるデザイナーを指定するには、Designer 属性が使用されます。  
  
```csharp  
[Designer(typeof(MyClassDesigner))]  
public sealed class MyClass : CodeActivity  
{
}
```  
  
## <a name="creating-a-service"></a>サービスの作成  
 デザイナーとホスト間の情報のコンジットとして機能するサービスを作成するには、インターフェイスと実装を作成する必要があります。 インターフェイスはサービスのメンバーを定義するために <xref:System.Activities.Presentation.ServiceManager.Publish%2A> メソッドによって使用され、実装にはサービスのロジックが含まれます。 次のコード例では、サービス インターフェイスと実装が作成されます。  
  
```csharp  
public interface IMyService  
    {  
        IEnumerable<string> GetValues(string DisplayName);  
    }  
  
    public class MyServiceImpl : IMyService  
    {  
        public IEnumerable<string> GetValues(string DisplayName)  
        {  
            return new string[]  {
                DisplayName + " One",
                DisplayName + " Two",  
                "Three " + DisplayName  
            } ;  
        }  
    }  
```  
  
## <a name="publishing-a-service"></a>サービスの公開  
 デザイナーでサービスを使用するには、最初に <xref:System.Activities.Presentation.ServiceManager.Publish%2A> メソッドを使用してホストで公開する必要があります。  
  
```csharp  
this.Context.Services.Publish<IMyService>(new MyServiceImpl);  
```  
  
## <a name="subscribing-to-a-service"></a>サービスの定期受信  
 デザイナーは、<xref:System.Activities.Presentation.ServiceManager.Subscribe%2A> メソッドの <xref:System.Activities.Presentation.WorkflowViewElement.OnModelItemChanged%2A> メソッドを使用してサービスにアクセスします。 次のコード スニペットは、サービスを定期受信する方法を示しています。  
  
```csharp  
protected override void OnModelItemChanged(object newItem)  
{  
    if (!subscribed)  
    {  
        this.Context.Services.Subscribe<IMyService>(  
            servInstance =>  
            {  
                listBox1.ItemsSource = servInstance.GetValues(this.ModelItem.Properties["DisplayName"].ComputedValue.ToString());  
            }  
            );  
        subscribed = true;
    }  
}  
```  
  
## <a name="sharing-data-using-the-items-collection"></a>Items コレクションを使用したデータの共有  
 Items コレクションの使用は Services コレクションの使用と似ていますが、Publish の代わりに <xref:System.Activities.Presentation.ContextItemManager.SetValue%2A> が使用されます。 このコレクションは、複雑な機能よりも、デザイナーとホスト間での単純なデータの共有に適しています。  
  
## <a name="editingcontext-host-items-and-services"></a>EditingContext ホスト項目およびサービス  
 .NET Framework には、編集コンテキストを通じてアクセスされる組み込みの項目とサービスが多数用意されています。  
  
 項目:  
  
- <xref:System.Activities.Presentation.Hosting.AssemblyContextControlItem>: ワークフロー内でコントロール (式エディターなど) に使用される参照先ローカル アセンブリのリストを管理します。  
  
- <xref:System.Activities.Presentation.Hosting.ReadOnlyState>: デザイナーが読み取り専用状態かどうかを示します。  
  
- <xref:System.Activities.Presentation.View.Selection>: 現在選択されているオブジェクトのコレクションを定義します。  
  
- <xref:System.Activities.Presentation.Hosting.WorkflowCommandExtensionItem>:  
  
- <xref:System.Activities.Presentation.WorkflowFileItem>: 現在の編集セッションが基づくファイルに関する情報を提供します。  
  
 複数サービス:   
  
- <xref:System.Activities.Presentation.Model.AttachedPropertiesService>: <xref:System.Activities.Presentation.Model.AttachedPropertiesService.AddProperty%2A> を使用して現在のインスタンスにプロパティを追加できます。  
  
- <xref:System.Activities.Presentation.View.DesignerView>: デザイナー キャンバスのプロパティにアクセスできるようにします。  
  
- <xref:System.Activities.Presentation.IActivityToolboxService>: ツールボックスの内容を更新できるようにします。  
  
- <xref:System.Activities.Presentation.Hosting.ICommandService>: デザイナー コマンド (コンテキスト メニューなど) をカスタム提供サービスの実装と統合するために使用します。  
  
- <xref:System.Activities.Presentation.Debug.IDesignerDebugView>: デザイナー デバッガーの機能を提供します。  
  
- <xref:System.Activities.Presentation.View.IExpressionEditorService>: [式エディター] ダイアログへのアクセスを可能にします。  
  
- <xref:System.Activities.Presentation.IIntegratedHelpService>: デザイナーに統合ヘルプ機能を提供します。  
  
- <xref:System.Activities.Presentation.Validation.IValidationErrorService>:  <xref:System.Activities.Presentation.Validation.IValidationErrorService.ShowValidationErrors%2A> を使用した検証エラーへのアクセスを可能にします。  
  
- <xref:System.Activities.Presentation.IWorkflowDesignerStorageService>: データを格納および取得するための内部サービスを提供します。 このサービスは、.NET Framework によって内部的に使用され、外部での使用を目的としていません。  
  
- <xref:System.Activities.Presentation.IXamlLoadErrorService>:  <xref:System.Activities.Presentation.IXamlLoadErrorService.ShowXamlLoadErrors%2A> を使用した XAML 読み込みエラー コレクションへのアクセスを可能にします。  
  
- <xref:System.Activities.Presentation.Services.ModelService>: 編集されているワークフローのモデルと対話するためにデザイナーによって使用されます。  
  
- <xref:System.Activities.Presentation.Model.ModelTreeManager>:  <xref:System.Activities.Presentation.Model.ModelItem.Root%2A> を使用したモデル アイテム ツリーのルートへのアクセスを可能にします。  
  
- <xref:System.Activities.Presentation.UndoEngine>: 元に戻す機能とやり直し機能を提供します。  
  
- <xref:System.Activities.Presentation.Services.ViewService>: 基になるモデル アイテムにビジュアル要素をマップします。  
  
- <xref:System.Activities.Presentation.View.ViewStateService>: モデル アイテムのビュー ステートを格納します。  
  
- <xref:System.Activities.Presentation.View.VirtualizedContainerService>: 仮想コンテナーの UI 動作をカスタマイズするために使用します。  
  
- <xref:System.Activities.Presentation.Hosting.WindowHelperService>: イベント通知のデリゲートを登録および登録解除するために使用します。 ウィンドウ所有者も設定できます。
