---
title: アクティビティ検証の呼び出し
ms.date: 03/30/2017
ms.assetid: 22bef766-c505-4fd4-ac0f-7b363b238969
ms.openlocfilehash: 1241e6445cde20a192581e8132e563e0f7ca8d93
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182885"
---
# <a name="invoking-activity-validation"></a>アクティビティ検証の呼び出し
アクティビティの検証は、アクティビティを実行する前にアクティビティの構成エラーを特定および報告する手段です。 検証が発生するのは、ワークフローがワークフロー デザイナーで修正され、検証エラーまたは警告がワークフロー デザイナーに表示されたときです。 ワーク フローの呼び出し時に検証も行われます。検証エラーが発生すると、既定の検証ロジックによって <xref:System.Activities.InvalidWorkflowException> がスローされます。 Windows ワークフロー基盤 (WF)<xref:System.Activities.Validation.ActivityValidationServices>には、ワークフロー アプリケーションと、アクティビティを明示的に検証する開発者が使用できるクラスが用意されています。 このトピックでは、<xref:System.Activities.Validation.ActivityValidationServices> を使用してアクティビティの検証を実行する方法を説明します。  
  
## <a name="using-activityvalidationservices"></a>ActivityValidationServices の使用  
 <xref:System.Activities.Validation.ActivityValidationServices> には、アクティビティの検証ロジックの呼び出しに使用される 2 つの <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> オーバーロードがあります。 1 つ目のオーバーロードは、検証されるルート アクティビティを受け取り、一連の検証エラーと警告を返します。 次の例では、2 つの必須引数を持つカスタムの `Add` アクティビティが使用されています。  
  
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
  
 `Add` アクティビティが <xref:System.Activities.Statements.Sequence> 内で使用されていますが、次の例に示すように、その 2 つの必須引数はバインドされていません。  
  
```csharp  
Variable<int> Operand1 = new Variable<int>{ Default = 10 };  
Variable<int> Operand2 = new Variable<int>{ Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 このワーク フローは、<xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> を呼び出して検証できます。 <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> は、次の例に示すように、アクティビティと子に含まれる一連の検証エラーと警告を返します。  
  
```csharp  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 このサンプル ワークフローで <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> が呼び出されると、次の 2 つの検証エラーが返されます。  
  
 **エラー: 必須のアクティビティ引数 'Operand2' の値が指定されませんでした。**  
**エラー: 必要なアクティビティ引数 'Operand1' の値が指定されませんでした。**  このワークフローが呼び出された場合、次の例に示すように、<xref:System.Activities.InvalidWorkflowException> がスローされることになります。  
  
```csharp  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 **System.Activities.InvalidWorkflowException:**  
**ワークフロー ツリーの処理中に次のエラーが発生しました:**
 **'Add': 必要なアクティビティ引数 'Operand2' の値が指定されていません。**
 **'Add': 必要なアクティビティ引数 'Operand1' の値が指定されませんでした。**  このサンプル ワークフローを有効にするには、`Add` アクティビティの 2 つの必須引数をバインドする必要があります。 次の例では、2 つの必須引数と結果値がワークフロー変数にバインドされています。 この例では、2 つの必須変数に加え、<xref:System.Activities.Activity%601.Result%2A> 引数がバインドされています。 <xref:System.Activities.Activity%601.Result%2A> 引数はバインドする必要がなく、バインドされていなくても検証エラーは発生しません。 <xref:System.Activities.Activity%601.Result%2A> の値がワークフローの別の場所で使用される場合、この引数のバインドはワークフローの作成者が行う必要があります。  
  
```csharp  
new Add  
{  
    Operand1 = Operand1,  
    Operand2 = Operand2,  
    Result = Result  
}  
```  
  
### <a name="validating-required-arguments-on-the-root-activity"></a>ルート アクティビティでの必須引数の検証  
 ワーク フローのルート アクティビティに引数がある場合、ワーク フローが呼び出され、パラメーターがワーク フローに渡されるまでこれらの引数はバインドされません。 次のワーク フローは検証を渡しますが、次の例に示すように、ワーク フローが必要な引数に渡されずに呼び出されると、例外がスローされます。  
  
```csharp  
Activity wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, but when the workflow  
// is invoked, an InvalidWorkflowException is thrown.  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 **System.ArgumentException: ルート アクティビティの引数の設定が正しくありません。**  
**ワークフロー定義を修正するか、入力値を指定してこれらのエラーを修正します:**
 **'Add': 必要なアクティビティ引数 'Operand2' の値が指定されていません。**
 **'Add': 必要なアクティビティ引数 'Operand1' の値が指定されませんでした。**  正しい引数が渡された後、次の例に示すように、ワークフローは正常に完了します。  
  
```csharp  
Add wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, and the workflow completes  
// successfully because the required arguments were passed.  
try  
{  
    Dictionary<string, object> wfparams = new Dictionary<string, object>  
    {  
        { "Operand1", 10 },  
        { "Operand2", 15 }  
    };  
  
    int result = WorkflowInvoker.Invoke(wf, wfparams);  
    Console.WriteLine("Result: {0}", result);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
> [!NOTE]
> この例では、前の例の `Add` とは異なり、ルート アクティビティは `Activity` として宣言されています。 このため、`WorkflowInvoker.Invoke` メソッドは、`Add` 引数のディクショナリではなく、`out` アクティビティの結果を表す 1 つの整数を返すことができます。 また、変数 `wf` は `Activity<int>` として宣言することも可能です。  
  
 ルート引数を検証する場合、ワークフローが呼び出されたときにすべての必須変数が渡されたことを確認するのはホスト アプリケーションが担当します。  
  
### <a name="invoking-imperative-code-based-validation"></a>命令型コードに基づく検証の呼び出し

命令型コードに基づく検証は、アクティビティでアクティビティ自身に関する検証を可能にする簡単な方法を提供し、<xref:System.Activities.CodeActivity>、<xref:System.Activities.AsyncCodeActivity>、および <xref:System.Activities.NativeActivity> から派生するアクティビティで使用できます。 検証のエラーまたは警告を判断する検証コードがアクティビティに追加されます。 検証がアクティビティで呼び出されると、これらの警告またはエラーは、<xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> への呼び出しで返されるコレクションに格納されます。 次の例では、 `CreateProduct` アクティビティを定義します。 `Cost` が `Price` よりも高い場合、検証エラーが <xref:System.Activities.CodeActivity.CacheMetadata%2A> オーバーライドのメタデータに追加されます。  
  
```csharp  
public sealed class CreateProduct : CodeActivity  
{  
    public double Price { get; set; }  
    public double Cost { get; set; }  
  
    // [RequiredArgument] attribute will generate a validation error
    // if the Description argument is not set.  
    [RequiredArgument]  
    public InArgument<string> Description { get; set; }  
  
    protected override void CacheMetadata(CodeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        // Determine when the activity has been configured in an invalid way.  
        if (this.Cost > this.Price)  
        {  
            // Add a validation error with a custom message.  
            metadata.AddValidationError("The Cost must be less than or equal to the Price.");  
        }  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // Not needed for the sample.  
    }  
}  
```  
  
 この例では、ワーク フローは `CreateProduct` のアクティビティを使用して構成されます。 このワーク フローで、`Cost` は `Price` より大きく、必須の `Description` 引数は設定されません。 検証を呼び出すと、次のエラーが返されます。  
  
```csharp  
Activity wf = new Sequence  
{  
    Activities =
    {  
        new CreateProduct  
        {  
            Cost = 75.00,  
            Price = 55.00  
            // Cost > Price and required Description argument not set.  
        },  
        new WriteLine  
        {  
            Text = "Product added."  
        }  
    }  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 **エラー: コストを価格以下する必要があります。**  
**エラー: 必須のアクティビティ引数 'Description' の値が指定されませんでした。**
> [!NOTE]
> カスタム アクティビティの作成者は、アクティビティの <xref:System.Activities.CodeActivity.CacheMetadata%2A> オーバーライドに検証ロジックを指定できます。 <xref:System.Activities.CodeActivity.CacheMetadata%2A> からスローされる例外は、検証エラーとして処理されません。 これらの例外は、<xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> への呼び出しからエスケープされ、呼び出し元によって処理される必要があります。  
  
## <a name="using-validationsettings"></a>ValidationSettings の使用  
 既定では、アクティビティ ツリー内のすべてのアクティビティは、検証が <xref:System.Activities.Validation.ActivityValidationServices> に呼び出されたときに評価されます。 <xref:System.Activities.Validation.ValidationSettings> を使用すると、その 3 つのプロパティを構成することによって、さまざまな方法で検証をカスタマイズできます。 <xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> は、バリデーターがアクティビティ ツリー全体を調べるか、指定したアクティビティにのみ検証ロジックを適用するかを指定します。 この値の既定値は、`false` です。 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> は、型から制約のリストへの追加の制約マッピングを指定します。 検証されているアクティビティ ツリーの各アクティビティの基本型について、<xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> への参照が行われます。 一致する制約リストが見つかると、アクティビティについて、リストのすべての制約が評価されます。 <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> は、バリデーターがすべての制約を評価するか、<xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> で指定された制約のみを評価するかを指定します。 既定値は `false` です。 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> および <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> は、FxCop のようなツールのポリシーの制約など、ワークフローの検証をワークフロー ホストの作成者がさらに追加する場合に便利です。 制約の詳細については、「[宣言型制約](declarative-constraints.md)」を参照してください。  
  
 <xref:System.Activities.Validation.ValidationSettings> を使用するには、必要なプロパティを構成し、<xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> の呼び出しで渡します。 この例では、カスタムの <xref:System.Activities.Statements.Sequence> アクティビティを持つ `Add` で構成されるワークフローが検証されます。 この `Add` アクティビティには必須引数が 2 つあります。  
  
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
  
 次の `Add` アクティビティは <xref:System.Activities.Statements.Sequence> で使用されますが、その 2 つの必須変数はバインドされていません。  
  
```csharp  
Variable<int> Operand1 = new Variable<int> { Default = 10 };  
Variable<int> Operand2 = new Variable<int> { Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 次の例では、<xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> が `true` に設定されて検証が実行されるため、ルート アクティビティ <xref:System.Activities.Statements.Sequence> のみが検証されます。  
  
```csharp  
ValidationSettings settings = new ValidationSettings  
{  
    SingleLevel = true  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf, settings);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 このコードを実行すると、次の出力が表示されます。  
  
 **警告またはエラーなし**アクティビティに`Add`バインドされていない必須引数があっても、ルート アクティビティのみが評価されるため、検証は成功します。 このタイプの検証は、デザイナーで 1 つのアクティビティのプロパティの変更を検証するなど、アクティビティ ツリーの特定の要素のみを検証する場合に便利です。 このワークフローが呼び出された場合、ワークフローで構成された完全な検証が評価され、<xref:System.Activities.InvalidWorkflowException> がスローされます。 <xref:System.Activities.Validation.ActivityValidationServices> および <xref:System.Activities.Validation.ValidationSettings> で構成されるのは、ホストによって明示的に呼び出される検証だけであり、ワークフローが呼び出されたときに発生する検証ではありません。
