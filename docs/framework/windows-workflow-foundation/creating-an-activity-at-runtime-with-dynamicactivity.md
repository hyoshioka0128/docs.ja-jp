---
title: 実行時における DynamicActivity を使用したアクティビティの作成
description: DynamicActivity は、パブリックコンストラクターを持つ具象クラスであり、シールされています。 アクティビティ DOM を使用して、実行時にアクティビティ機能をアセンブルするには、クラスを使用します。
ms.date: 03/30/2017
ms.assetid: 1af85cc6-912d-449e-90c5-c5db3eca5ace
ms.openlocfilehash: 17ee14be7df4801018c7afd2e91f1fb07c34e8e1
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421541"
---
# <a name="creating-an-activity-at-runtime-with-dynamicactivity"></a>実行時における DynamicActivity を使用したアクティビティの作成
<xref:System.Activities.DynamicActivity> は、パブリック コンストラクターを持つ、具体的なシール クラスです。 <xref:System.Activities.DynamicActivity> は、実行時にアクティビティ DOM を使用してアクティビティの機能を構築するために使用できます。  
  
## <a name="dynamicactivity-features"></a>DynamicActivity の機能  
 <xref:System.Activities.DynamicActivity> は、実行プロパティ、引数、変数にアクセスできますが、子アクティビティのスケジュール設定や追跡などのランタイム サービスにはアクセスできません。  
  
 最上位のプロパティは、ワークフローの <xref:System.Activities.Argument> オブジェクトを使用して設定できます。 命令型コードでは、これらの引数は新しい型で CLR プロパティを使用して作成されます。 XAML では `x:Class` タグおよび `x:Member` タグを使用して、これらの引数が宣言されます。  
  
 <xref:System.Activities.DynamicActivity> を使用して構築されたアクティビティは、<xref:System.ComponentModel.ICustomTypeDescriptor> を使用してデザイナーとやり取りします。 デザイナーで作成されたアクティビティは、次の手順に示すように、<xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> を使用して動的に読み込むことができます。  
  
#### <a name="to-create-an-activity-at-runtime-using-imperative-code"></a>命令型コードを使用して実行時にアクティビティを作成するには  
  
1. OpenVisual Studio 2010。  
  
2. [**ファイル**]、[**新規作成**]、[**プロジェクト**] を選択します。 [**プロジェクトの種類**] ウィンドウの [ **Visual C#** ] で [**ワークフロー 4.0** ] を選択し、[ **v2010** ] ノードを選択します。 [**テンプレート**] ウィンドウで [**シーケンシャルワークフローコンソールアプリケーション**] を選択します。 新しいプロジェクトに DynamicActivitySample という名前を付けます。  
  
3. HelloActivity プロジェクトで Workflow1.xaml を右クリックし、[**削除**] を選択します。  
  
4. Program.cs を開きます。 次のディレクティブをファイルの先頭に追加します。  
  
    ```csharp  
    using System.Collections.Generic;  
    ```  
  
5. 1 つの `Main` アクティビティを含む <xref:System.Activities.Statements.Sequence> アクティビティを作成する次のコードで <xref:System.Activities.Statements.WriteLine> メソッドの内容を置き換え、新しい動的アクティビティの <xref:System.Activities.DynamicActivity.Implementation%2A> プロパティに割り当てます。  
  
    ```csharp  
    //Define the input argument for the activity  
    var textOut = new InArgument<string>();  
    //Create the activity, property, and implementation  
                Activity dynamicWorkflow = new DynamicActivity()  
                {  
                    Properties =
                    {  
                        new DynamicActivityProperty  
                        {  
                            Name = "Text",  
                            Type = typeof(InArgument<String>),  
                            Value = textOut  
                        }  
                    },  
                    Implementation = () => new Sequence()  
                    {  
                        Activities =
                        {  
                            new WriteLine()  
                            {  
                                Text = new InArgument<string>(env => textOut.Get(env))  
                            }  
                        }  
                    }  
                };  
    //Execute the activity with a parameter dictionary  
                WorkflowInvoker.Invoke(dynamicWorkflow, new Dictionary<string, object> { { "Text", "Hello World!" } });  
                Console.ReadLine();  
    ```  
  
6. アプリケーションを実行します。 "Hello World!" というテキストが表示されたコンソールウィンドウ ヲ.  
  
#### <a name="to-create-an-activity-at-runtime-using-xaml"></a>XAML を使用して実行時にアクティビティを作成するには  
  
1. Visual Studio 2010 を開きます。  
  
2. [**ファイル**]、[**新規作成**]、[**プロジェクト**] を選択します。 [**プロジェクトの種類**] ウィンドウの [ **Visual C#** ] で [**ワークフロー 4.0** ] を選択し、[ **v2010** ] ノードを選択します。 [**テンプレート**] ウィンドウで [**ワークフローコンソールアプリケーション**] を選択します。 新しいプロジェクトに DynamicActivitySample という名前を付けます。  
  
3. HelloActivity プロジェクトの Workflow1.xaml を開きます。 デザイナーの下部にある [**引数**] オプションをクリックします。 `String` 型の `TextToWrite` という新しい `In` 引数を作成します。  
  
4. ツールボックスの [**プリミティブ**] セクションから、 **WriteLine**アクティビティをデザイナー画面にドラッグします。 `TextToWrite`アクティビティの**Text**プロパティに値を割り当てます。  
  
5. Program.cs を開きます。 次のディレクティブをファイルの先頭に追加します。  
  
    ```csharp  
    using System.Activities.XamlIntegration;  
    ```  
  
6. `Main` メソッドの内容を次のコードに置き換えます。  
  
    ```csharp  
    Activity act2 = ActivityXamlServices.Load(@"Workflow1.xaml");  
                    results = WorkflowInvoker.Invoke(act2, new Dictionary<string, object> { { "TextToWrite", "HelloWorld!" } });  
    Console.ReadLine();  
    ```  
  
7. アプリケーションを実行します。 "Hello World!" というテキストが表示されたコンソールウィンドウ  が表示されます。  
  
8. **ソリューションエクスプローラー**で workflow1.xaml ファイルを右クリックし、[**コードの表示**] を選択します。 アクティビティ クラスが `x:Class` を使用して作成され、プロパティが `x:Property` を使用して作成されています。  
  
## <a name="see-also"></a>関連項目

- [命令型コードを使用してワークフロー、アクティビティ、および式を作成する方法](authoring-workflows-activities-and-expressions-using-imperative-code.md)
