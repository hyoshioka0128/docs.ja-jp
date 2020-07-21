---
title: ワークフロー実行プロパティ
ms.date: 03/30/2017
ms.assetid: a50e088e-3a45-4267-bd51-1a3e6c2d246d
ms.openlocfilehash: 0f958e7e112bfddc2740c2605d446493f2d49010
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182664"
---
# <a name="workflow-execution-properties"></a>ワークフロー実行プロパティ
CLR は、スレッド ローカル ストレージ (TLS) を介して各スレッドの実行コンテキストを維持します。 この実行コンテキストは、スレッド ID、アンビエント トランザクション、現在のアクセス許可セットなど、既知のスレッド プロパティに加えて、名前付きスロットのようなユーザー定義のスレッド プロパティを制御します。  
  
 CLR を直接対象にするプログラムとは異なり、ワークフロー プログラムは、スレッド非依存環境で実行されるアクティビティのツリーへ階層的にスコープ設定されます。 つまり、特定の作業項目のスコープに含まれるコンテキストを判断するために、標準の TLS 機構を直接使用することはできません。 たとえば、2 つの並行する実行の分岐で異なるトランザクションを使用していても、スケジューラは同じ CLR スレッド上でそれらの実行をインターリーブすることがあります。  
  
 ワークフローの実行プロパティには、アクティビティの環境にコンテキスト特有のプロパティを追加する機構が用意されています。 そのため、サブツリーのスコープに含まれるプロパティをアクティビティで宣言することができ、CLR オブジェクトと適切に相互作用するように TLS の設定および設定解除を行うフックの実現もできます。  
  
## <a name="creating-and-using-workflow-execution-properties"></a>ワークフロー実行プロパティの作成と使用  
 ワークフロー実行プロパティは、通常、<xref:System.Activities.IExecutionProperty> インターフェイスを実装します。ただし、メッセージングに重点を置いたプロパティが代わりに <xref:System.ServiceModel.Activities.ISendMessageCallback> と <xref:System.ServiceModel.Activities.IReceiveMessageCallback> を実装することもあります。 ワークフロー実行プロパティを作成するには、<xref:System.Activities.IExecutionProperty> インターフェイスを実装するクラスを作成し、メンバーの <xref:System.Activities.IExecutionProperty.SetupWorkflowThread%2A> および <xref:System.Activities.IExecutionProperty.CleanupWorkflowThread%2A> を実装します。 これらのメンバーには、プロパティを含むアクティビティ (すべての子アクティビティを含む) の作業の各パルス中に、スレッド ローカル ストレージを適切に設定および設定解除できる実行プロパティがあります。 この例では、`ConsoleColorProperty` を設定する `Console.ForegroundColor` を作成します。  
  
```csharp  
class ConsoleColorProperty : IExecutionProperty  
{  
    public const string Name = "ConsoleColorProperty";  
  
    ConsoleColor original;  
    ConsoleColor color;  
  
    public ConsoleColorProperty(ConsoleColor color)  
    {  
        this.color = color;  
    }  
  
    void IExecutionProperty.SetupWorkflowThread()  
    {  
        original = Console.ForegroundColor;  
        Console.ForegroundColor = color;  
    }  
  
    void IExecutionProperty.CleanupWorkflowThread()  
    {  
        Console.ForegroundColor = original;  
    }  
}  
```  
  
 アクティビティ作成者がこのプロパティを使用するには、アクティビティの実行オーバーライドに登録します。 この例では、現在の <xref:System.Activities.NativeActivityContext> の <xref:System.Activities.NativeActivityContext.Properties%2A> コレクションに追加することで、`ConsoleColorProperty` を登録する `ConsoleColorScope` アクティビティが定義されています。  
  
```csharp  
public sealed class ConsoleColorScope : NativeActivity  
{  
    public ConsoleColorScope()  
        : base()  
    {  
    }  
  
    public ConsoleColor Color { get; set; }  
    public Activity Body { get; set; }  
  
    protected override void Execute(NativeActivityContext context)  
    {  
        context.Properties.Add(ConsoleColorProperty.Name, new ConsoleColorProperty(this.Color));  
  
        if (this.Body != null)  
        {  
            context.ScheduleActivity(this.Body);  
        }  
    }  
}  
```  
  
 アクティビティの本体が作業のパルスを開始すると、プロパティの <xref:System.Activities.IExecutionProperty.SetupWorkflowThread%2A> メソッドが呼び出されます。作業のパルスが完了すると、<xref:System.Activities.IExecutionProperty.CleanupWorkflowThread%2A> が呼び出されます。 この例では、3 つの分岐がある <xref:System.Activities.Statements.Parallel> アクティビティを使用するワークフローが作成されます。 最初の 2 つの分岐では `ConsoleColorScope` アクティビティを使用しますが、3 つ目の分岐は使用しません。 3 つの分岐にはいずれも 2 つの <xref:System.Activities.Statements.WriteLine> アクティビティと 1 つの <xref:System.Activities.Statements.Delay> アクティビティが含まれます。 <xref:System.Activities.Statements.Parallel> アクティビティが実行されると、その分岐に含まれるアクティビティはインターリーブ形式で実行されますが、それぞれの子アクティビティが実行されるため、`ConsoleColorProperty` によって適切なコンソールの色が適用されます。  
  
```csharp  
Activity wf = new Parallel  
{  
    Branches =
    {  
        new ConsoleColorScope  
        {  
            Color = ConsoleColor.Blue,  
            Body = new Sequence  
            {  
                Activities =
                {  
                    new WriteLine  
                    {  
                        Text = "Start blue text."  
                    },  
                    new Delay  
                    {  
                        Duration = TimeSpan.FromSeconds(1)  
                    },  
                    new WriteLine  
                    {  
                        Text = "End blue text."  
                    }  
                }  
            }  
        },  
        new ConsoleColorScope  
        {  
            Color = ConsoleColor.Red,  
            Body = new Sequence  
            {  
                Activities =
                {  
                    new WriteLine  
                    {  
                        Text = "Start red text."  
                    },  
                    new Delay  
                    {  
                        Duration = TimeSpan.FromSeconds(1)  
                    },  
                    new WriteLine  
                    {  
                        Text = "End red text."  
                    }  
                }  
            }  
        },  
        new Sequence  
        {  
            Activities =
            {  
                new WriteLine  
                {  
                    Text = "Start default text."  
                },  
                new Delay  
                {  
                    Duration = TimeSpan.FromSeconds(1)  
                },  
                new WriteLine  
                {  
                    Text = "End default text."  
                }  
            }  
        }  
    }  
};  
  
WorkflowInvoker.Invoke(wf);  
```  
  
 このワークフローを呼び出すと、次の出力がコンソール ウィンドウに書き込まれます。  
  
```console  
Start blue text.  
Start red text.  
Start default text.  
End blue text.  
End red text.  
End default text.  
```  
  
> [!NOTE]
> 前の出力には示していませんが、コンソール ウィンドウの各テキスト行は、指定した色で表示されます。  
  
 ワークフロー実行プロパティは、カスタム アクティビティ作成者が使用できます。また、このプロパティには、<xref:System.ServiceModel.Activities.CorrelationScope> や <xref:System.Activities.Statements.TransactionScope> などのアクティビティ向けにハンドル管理の機構も用意されています。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Activities.IExecutionProperty>
- <xref:System.Activities.IPropertyRegistrationCallback>
- <xref:System.Activities.RegistrationContext>
