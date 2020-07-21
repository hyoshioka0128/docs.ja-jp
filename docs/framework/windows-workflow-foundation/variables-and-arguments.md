---
title: 変数と引数
description: この記事では、データの格納を表す変数と、Workflow Foundation のアクティビティとの間のデータフローを表す引数について説明します。
ms.date: 03/30/2017
ms.assetid: d03dbe34-5b2e-4f21-8b57-693ee49611b8
ms.openlocfilehash: 5cce9931e9b0a37d5fafbfb84527ffd543a0a50f
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84201957"
---
# <a name="variables-and-arguments"></a>変数と引数
Windows Workflow Foundation (WF) では、変数はデータのストレージを表し、引数はアクティビティとの間のデータフローを表します。 アクティビティには一連の引数があり、その引数はアクティビティの署名を構成します。 また、アクティビティは開発者がワークフローの設計時に変数を追加または削除できる変数のリストを保持しています。 引数は、値を返す式を使用してバインドされます。  
  
## <a name="variables"></a>変数  
 変数はデータを保存する場所です。 変数はワークフロー定義の一部として宣言されます。 変数は実行時に値を受け取ります。これらの値はワークフロー インスタンスの状態の一部として保存されます。 変数の定義では、変数の型を指定します。オプションで名前を指定する場合もあります。 変数を宣言し、<xref:System.Activities.Statements.Assign%601> アクティビティを使用して変数に値を代入し、その値を <xref:System.Activities.Statements.WriteLine> アクティビティを使用してコンソールに表示する方法を次のコードに示します。  
  
```csharp  
// Define a variable named "str" of type string.  
Variable<string> var = new Variable<string>  
{  
    Name = "str"  
};  
  
// Declare the variable within a Sequence, assign  
// a value to it, and then display it.  
Activity wf = new Sequence()  
{  
    Variables = { var },  
    Activities =  
    {  
        new Assign<string>  
        {  
            To = var,  
            Value = "Hello World."  
        },  
        new WriteLine  
        {  
            Text = var  
        }  
    }  
};  
  
WorkflowInvoker.Invoke(wf);  
```  
  
 オプションで、変数宣言の一部として既定値の式を指定できます。 また、変数は修飾子を使用することもできます。 たとえば変数が読み取り専用の場合は、読み取り専用の <xref:System.Activities.VariableModifiers> 修飾子を適用できます。 次の例では、既定値を代入した読み取り専用の変数を作成します。  
  
```csharp  
// Define a read-only variable with a default value.  
Variable<string> var = new Variable<string>  
{  
    Default = "Hello World.",  
    Modifiers = VariableModifiers.ReadOnly  
};  
```  
  
## <a name="variable-scoping"></a>変数のスコープ  
 実行時の変数の有効期間は、変数を宣言したアクティビティの有効期間と同じです。 アクティビティが完了すると、その変数はクリーンアップされ、その後は参照できません。  
  
## <a name="arguments"></a>引数  
 アクティビティの作成者は、引数を使用してアクティビティとのデータ フローの方法を定義します。 各引数には <xref:System.Activities.ArgumentDirection.In>、<xref:System.Activities.ArgumentDirection.Out>、<xref:System.Activities.ArgumentDirection.InOut> などの方向が指定されます。  
  
 ワークフロー ランタイムでは、アクティビティへのデータ移動のタイミングについて次のように保証しています。  
  
1. アクティビティが実行を開始すると、すべての入力および入出力引数の値が計算されます。 たとえば、<xref:System.Activities.Argument.Get%2A> が呼び出されるタイミングにかかわらず、返される値は `Execute` が呼び出される前にランタイムによって計算された値になります。  
  
2. <xref:System.Activities.InOutArgument%601.Set%2A> が呼び出されると、ランタイムはすぐにその値を設定します。  
  
3. 必要に応じて、引数に <xref:System.Activities.Argument.EvaluationOrder%2A> を指定できます。 <xref:System.Activities.Argument.EvaluationOrder%2A> は引数の評価順序を指定するゼロベースの値です。 既定では引数の評価順序は指定されておらず、<xref:System.Activities.Argument.UnspecifiedEvaluationOrder> の値と同じです。 <xref:System.Activities.Argument.EvaluationOrder%2A> に 0 以上の値を設定して、この引数の評価順序を指定します。 Windows Workflow Foundation は、指定された評価順序で引数を昇順で評価します。 評価順序が指定されていない引数は、評価順序が指定されている引数の前に評価されることに注意してください。  
  
 アクティビティの作成者は、厳密に型指定された機構を使用して引数を公開できます。 これを行うには、<xref:System.Activities.InArgument%601>、<xref:System.Activities.OutArgument%601>、および <xref:System.Activities.InOutArgument%601> の型のプロパティを宣言します。 これにより、アクティビティの作成者は、アクティビティに受け渡しするデータの特定のコントラクトを確立できます。  
  
### <a name="defining-the-arguments-on-an-activity"></a>アクティビティの引数の定義  
 <xref:System.Activities.InArgument%601>、<xref:System.Activities.OutArgument%601>、および <xref:System.Activities.InOutArgument%601> 型のプロパティを指定することで、アクティビティに引数を定義できます。 次のコードでは、ユーザーに表示する文字列を受け取り、ユーザーの応答を含む文字列を返す `Prompt` アクティビティの引数を定義する方法を示します。  
  
```csharp  
public class Prompt : Activity  
{  
    public InArgument<string> Text { get; set; }  
    public OutArgument<string> Response { get; set; }  
    // Rest of activity definition omitted.  
}  
```  
  
> [!NOTE]
> 1 つの値を返すアクティビティは、<xref:System.Activities.Activity%601>、<xref:System.Activities.NativeActivity%601>、または <xref:System.Activities.CodeActivity%601> から派生させることができます。 これらのアクティビティは、アクティビティの戻り値を含む <xref:System.Activities.OutArgument%601> という名前の適切に定義された <xref:System.Activities.Activity%601.Result%2A> を持っています。  
  
### <a name="using-variables-and-arguments-in-workflows"></a>ワークフローでの変数と引数の使用  
 次の例は、ワークフローで変数と引数を使用する方法を示しています。 このワークフローは、3 つの変数 `var1`、`var2`、`var3` を宣言するシーケンスです。 このワークフローの最初のアクティビティは `Assign` アクティビティで、変数 `var1` の値を変数 `var2` に代入します。 これに `WriteLine` アクティビティが続き、変数 `var2` の値を出力します。 その次はもう 1 つの `Assign` アクティビティで、変数 `var2` の値を変数 `var3` に代入します。 最後にもう 1 つの `WriteLine` アクティビティがあり、変数 `var3` の値を出力します。 最初の `Assign` アクティビティは、アクティビティの引数のバインドを明示的に表す `InArgument<string>` オブジェクトと `OutArgument<string>` オブジェクトを使用します。 `InArgument<string>` は、値が <xref:System.Activities.Statements.Assign.Value%2A> アクティビティにその <xref:System.Activities.Statements.Assign%601> 引数を通ってフローするので、<xref:System.Activities.Statements.Assign.Value%2A> に使用されます。`OutArgument<string>` は、値が <xref:System.Activities.Statements.Assign.To%2A> 引数から変数へフローするので、<xref:System.Activities.Statements.Assign.To%2A> に使用されます。 2 番目の `Assign` アクティビティは、より少ないコードで暗黙的なキャストを使用する同等の構文を使用して同じ内容を実行します。 `WriteLine` アクティビティも少ないコードの構文を使用します。  
  
```csharp  
// Declare three variables; the first one is given an initial value.  
Variable<string> var1 = new Variable<string>()  
{  
    Default = "one"  
};  
Variable<string> var2 = new Variable<string>();  
Variable<string> var3 = new Variable<string>();  
  
// Define the workflow  
Activity wf = new Sequence  
{  
    Variables = { var1, var2, var3 },  
    Activities =
    {  
        new Assign<string>()  
        {  
            Value = new InArgument<string>(var1),  
            To = new OutArgument<string>(var2)  
        },  
        new WriteLine() { Text = var2 },  
        new Assign<string>()  
        {  
            Value = var2,  
            To = var3  
        },  
        new WriteLine() { Text = var3 }  
    }  
};  
  
WorkflowInvoker.Invoke(wf);  
```  
  
### <a name="using-variables-and-arguments-in-code-based-activities"></a>コードに基づいたアクティビティでの変数と引数の使用  
 前の例は、ワークフローの引数と変数、および宣言型のアクティビティを使用する方法を示しています。 引数と変数は、コードに基づくアクティビティでも使用されます。 概念上は、使用法は非常に似ています。 変数はアクティビティ内のデータ ストレージを表し、引数はアクティビティへのデータ フローを表し、ワークフロー作成者によってワークフローでデータの受け渡しを行う場所を示す他の変数または引数にバインドされます。 アクティビティの変数または引数の値を取得または設定するには、アクティビティの現在の実行環境を表すアクティビティ コンテキストを使用する必要があります。 これは、ワークフロー ランタイムによってアクティビティの <xref:System.Activities.CodeActivity%601.Execute%2A> メソッドに渡されます。 次の例では、2 つの `Add` 引数を持つカスタムの <xref:System.Activities.ArgumentDirection.In> アクティビティが定義されています。 この引数の値にアクセスするために <xref:System.Activities.Argument.Get%2A> メソッドが使用され、ワークフロー ランタイムによって渡されたコンテキストが使用されます。  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 コードで引数、変数、および式を使用する方法の詳細については、「命令型コードと[必須の引数およびオーバーロードグループ](required-arguments-and-overload-groups.md)[を使用したワークフロー、アクティビティ、および式の作成](authoring-workflows-activities-and-expressions-using-imperative-code.md)」を参照してください。
