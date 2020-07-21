---
title: モデル アイテム ツリーのプログラミング
ms.date: 03/30/2017
ms.assetid: 0229efde-19ac-4bdc-a187-c6227a7bd1a5
ms.openlocfilehash: f14b140fdac95f3763cc5625841a725793876fa4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142694"
---
# <a name="programming-model-item-tree"></a>モデル アイテム ツリーのプログラミング
このサンプルでは、Windows プレゼンテーションファン<xref:System.Activities.Presentation.Model.ModelItem>デーション (WPF) ツリー ビューから宣言型データ バインディングを使用してツリーを移動する方法を示します。

## <a name="sample-details"></a>サンプルの詳細
 ツリー<xref:System.Activities.Presentation.Model.ModelItem>は、Windows ワークフロー デザイナー インフラストラクチャで使用される抽象化で、編集対象の基になるインスタンスに関するデータを公開します。 次の図は、ワークフロー デザイナー内のさまざまなインフラストラクチャ 層を示しています。

 ![ワークフロー デザイナーのアーキテクチャを示す図。](./media/programming-model-item-tree/workflow-designer-architecture.jpg)

 <xref:System.Activities.Presentation.Model.ModelItem> は、基になる値へのポインターと、<xref:System.Activities.Presentation.Model.ModelProperty> オブジェクトのコレクションで構成されています。 <xref:System.Activities.Presentation.Model.ModelProperty> オブジェクトはさらに、プロパティの名前や型などのデータと、また別の <xref:System.Activities.Presentation.Model.ModelItem> である値へのポインターで構成されています。 <xref:System.Activities.Presentation.Model.ModelItem> から返される一部の <xref:System.Activities.Presentation.Model.ModelProperty> に対しては、ツリー ビューに正しく表示されるように操作するために値コンバーターが使用されます。 このサンプルでは、次の例のような命令構文を使用して <xref:System.Activities.Presentation.Model.ModelItem> ツリーを命令型プログラミングで操作する方法を示します。

```csharp
ModelItem mi = wd.Context.Services.GetService<ModelService>().Root;
ModelProperty mp = mi.Properties["Activities"];
mp.Collection.Add(new Persist());
ModelItem justAdded = mp.Collection.Last();
justAdded.Properties["DisplayName"].SetValue("new name");
```

#### <a name="to-use-this-sample"></a>このサンプルを使用するには

1. 2010 年にプログラムモデルアイテムツリー.sln ソリューションを開きます。

2. [ビルド] メニューの [**ソリューションのビルド**] を選択してソリューションを**ビルド**します。

3. F5 キーを押してアプリケーションを実行します。 その後、WPF フォームが表示されます。

4. [WF**のロード**] ボタン<xref:System.Activities.Presentation.Model.ModelItem>をクリックして、 をロードし、ツリー ビューにバインドします。

5. [**モデル アイテム ツリーの変更]** ボタンをクリックすると、上記のコードが実行され、ツリーに項目が追加され、プロパティが設定されます。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Designer\ProgrammingModelItemTree`  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Data.IValueConverter>
