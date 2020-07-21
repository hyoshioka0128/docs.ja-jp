---
title: XAML との間のワークフローおよびアクティビティのシリアル化
description: この記事では、ワークフロー定義のシリアル化の概要と、Workflow Foundation での XAML ワークフロー定義の使用について説明します。
ms.date: 03/30/2017
ms.assetid: 37685b32-24e3-4d72-88d8-45d5fcc49ec2
ms.openlocfilehash: 168dbc9a36cfa80c15fddc7481e986d1ce383adb
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83421346"
---
# <a name="serialize-workflows-and-activities-to-and-from-xaml"></a>XAML との間でワークフローとアクティビティをシリアル化する

ワークフロー定義は、アセンブリに含まれる型にコンパイルされるほか、XAML にシリアル化することもできます。 これらのシリアル化された定義は、編集や検査のために再度読み込んだり、コンパイルのためにビルド システムに渡したり、読み込んで呼び出したりすることができます。 このトピックでは、ワークフロー定義のシリアル化と XAML ワークフロー定義の使用に関する概要について説明します。

## <a name="work-with-xaml-workflow-definitions"></a>XAML ワークフロー定義の操作

シリアル化するワークフロー定義を作成するには、<xref:System.Activities.ActivityBuilder> クラスを使用します。 <xref:System.Activities.ActivityBuilder> の作成は、<xref:System.Activities.DynamicActivity> の作成とほとんど同じです。 目的の引数を指定し、動作を構成するアクティビティを構成します。 次の例では、2 つの入力引数を受け取り、それらを加算して結果を返す `Add` アクティビティを作成しています。 このアクティビティは結果を返すため、ジェネリック <xref:System.Activities.ActivityBuilder%601> クラスが使用されています。

[!code-csharp[CFX_WorkflowApplicationExample#41](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#41)]

それぞれの <xref:System.Activities.DynamicActivityProperty> インスタンスでワークフローへの入力引数を 1 つずつ表し、<xref:System.Activities.ActivityBuilder.Implementation%2A> にワークフローのロジックを構成するアクティビティが格納されています。 この例では、右辺値の式が Visual Basic 式であることに注意してください。 <xref:System.Activities.Expressions.ExpressionServices.Convert%2A> を使用しないと、ラムダ式は XAML 形式にシリアル化できません。 ワークフローデザイナーでシリアル化されたワークフローを開いたり編集したりする場合は、Visual Basic 式を使用する必要があります。 詳細については、「[命令型コードを使用したワークフロー、アクティビティ、および式の作成](authoring-workflows-activities-and-expressions-using-imperative-code.md)」を参照してください。

XAML への <xref:System.Activities.ActivityBuilder> インスタンスで表されるワークフロー定義を XAML 形式にシリアル化するには、<xref:System.Activities.XamlIntegration.ActivityXamlServices> を使用して <xref:System.Xaml.XamlWriter> を作成した後、その <xref:System.Xaml.XamlServices> を使用することで、<xref:System.Xaml.XamlWriter> を使用してワークフロー定義をシリアル化します。 <xref:System.Activities.XamlIntegration.ActivityXamlServices>には、 <xref:System.Activities.ActivityBuilder> xaml との間でインスタンスをマップし、xaml ワークフローを読み込んで、呼び出すことができるを返すメソッドが用意されてい <xref:System.Activities.DynamicActivity> ます。 次の例では、 <xref:System.Activities.ActivityBuilder> 前の例のインスタンスを文字列にシリアル化し、ファイルに保存しています。

```csharp
// Serialize the workflow to XAML and store it in a string.
StringBuilder sb = new StringBuilder();
StringWriter tw = new StringWriter(sb);
XamlWriter xw = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(tw, new XamlSchemaContext()));
XamlServices.Save(xw, ab);
string serializedAB = sb.ToString();

// Display the XAML to the console.
Console.WriteLine(serializedAB);

// Serialize the workflow to XAML and save it to a file.
StreamWriter sw = File.CreateText(@"C:\Workflows\add.xaml");
XamlWriter xw2 = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(sw, new XamlSchemaContext()));
XamlServices.Save(xw2, ab);
sw.Close();
```

シリアル化されたワークフローの例を次に示します。

```xaml
<Activity
  x:TypeArguments="x:Int32"
  x:Class="Add"
  xmlns="http://schemas.microsoft.com/netfx/2009/xaml/activities"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
  <x:Members>
    <x:Property Name="Operand1" Type="InArgument(x:Int32)" />
    <x:Property Name="Operand2" Type="InArgument(x:Int32)" />
  </x:Members>
  <Sequence>
    <WriteLine Text="[Operand1.ToString() + " + " + Operand2.ToString()]" />
    <Assign x:TypeArguments="x:Int32" Value="[Operand1 + Operand2]">
      <Assign.To>
        <OutArgument x:TypeArguments="x:Int32">
          <ArgumentReference x:TypeArguments="x:Int32" ArgumentName="Result" />
          </OutArgument>
      </Assign.To>
    </Assign>
  </Sequence>
</Activity>
```

シリアル化されたワークフローを読み込むには、メソッドを使用し <xref:System.Activities.XamlIntegration.ActivityXamlServices> <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A> ます。 このメソッドは、シリアル化されたワークフロー定義を受け取り、ワークフロー定義を表す <xref:System.Activities.DynamicActivity> を返します。 検証プロセス中に <xref:System.Activities.Activity.CacheMetadata%2A> の本体で <xref:System.Activities.DynamicActivity> が呼び出されるまでは、XAML は逆シリアル化されないことに注意してください。 検証が明示的に呼び出されていない場合は、ワークフローが呼び出されたときに実行されます。 XAML ワークフロー定義が無効な場合、<xref:System.ArgumentException> 例外がスローされます。 <xref:System.Activities.Activity.CacheMetadata%2A> からスローされる例外は、<xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> への呼び出しからエスケープされ、呼び出し元によって処理される必要があります。 次の例では、前の例のシリアル化されたワークフローを読み込み、<xref:System.Activities.WorkflowInvoker> を使用して呼び出しています。

[!code-csharp[CFX_WorkflowApplicationExample#43](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#43)]

このワークフローが呼び出されると、次の出力がコンソールに表示されます。

**25 + 15**\
**40**

> [!NOTE]
> 入力引数と出力引数を使用してワークフローを呼び出す方法の詳細については、「 [WorkflowInvoker 元と WorkflowApplication の使用](using-workflowinvoker-and-workflowapplication.md)」および「」を参照してください <xref:System.Activities.WorkflowInvoker.Invoke%2A> 。

シリアル化されたワークフローに C# の式が含まれている場合、 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings> そのプロパティがに設定されたインスタンスは、 <xref:System.Activities.XamlIntegration.ActivityXamlServicesSettings.CompileExpressions%2A> `true` にパラメーターとして渡す必要があります。 <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A?displayProperty=nameWithType> そうしないと、が <xref:System.NotSupportedException> スローされ、次のようなメッセージが表示されます。 **Expression アクティビティの型 ' CSharpValue ' 1 ' は、実行するためにコンパイルが必要です ワークフローがコンパイルされていることを確認してください。**

```csharp
ActivityXamlServicesSettings settings = new ActivityXamlServicesSettings
{
    CompileExpressions = true
};

DynamicActivity<int> wf = ActivityXamlServices.Load(new StringReader(serializedAB), settings) as DynamicActivity<int>;
```

詳細については、「 [C# の式](csharp-expressions.md)」を参照してください。

シリアル化されたワークフロー定義は、メソッドを使用してインスタンスに読み込むこともでき <xref:System.Activities.ActivityBuilder> <xref:System.Activities.XamlIntegration.ActivityXamlServices> <xref:System.Activities.XamlIntegration.ActivityXamlServices.CreateBuilderReader%2A> ます。 シリアル化されたワークフローをインスタンスに読み込む <xref:System.Activities.ActivityBuilder> と、そのワークフローを検査および変更できるようになります。 これにより、デザイン プロセス中にワークフロー定義を保存したり再度読み込んだりするためのメカニズムが提供され、カスタム ワークフロー デザイナーを作成するときに役立ちます。 次の例では、前の例のシリアル化されたワークフロー定義を読み込み、そのプロパティを検査しています。

[!code-csharp[CFX_WorkflowApplicationExample#44](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#44)]
