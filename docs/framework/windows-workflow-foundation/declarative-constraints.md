---
title: 宣言の制約
ms.date: 03/30/2017
ms.assetid: 67001ed1-7f4d-4ada-ae57-a31176901a53
ms.openlocfilehash: 321021e3d73daecae07268f33807c992414a7b4c
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182959"
---
# <a name="declarative-constraints"></a>宣言の制約
宣言の制約には、アクティビティ、およびそのアクティビティと他のアクティビティとの関係に関する検証の強力なメソッドが用意されています。 アクティビティに関する制約はプロセスの作成中に構成されますが、ワークフロー ホストによって追加の制約を指定することもできます。 ここでは、宣言の制約を使用してアクティビティを検証する方法の概要について説明します。  
  
## <a name="using-declarative-constraints"></a>宣言の制約の使用  
 制約とは、検証ロジックを含むアクティビティです。 この制約アクティビティは、コードまたは XAML で作成できます。 制約アクティビティを作成したら、アクティビティの作成者はアクティビティの <xref:System.Activities.Activity.Constraints%2A> プロパティにこの制約を追加して検証を実行します。またはこの制約を使用して、<xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> インスタンスの <xref:System.Activities.Validation.ValidationSettings> プロパティを使った追加の検証を実行します。 検証ロジックは、アクティビティのメタデータの検証など、単純な検証で構成されますが、親アクティビティ、子アクティビティ、および兄弟アクティビティに対する現在のアクティビティの関係を考慮した検証を実行することもできます。 制約は、<xref:System.Activities.Validation.Constraint%601> アクティビティを使用して作成されます。また、検証のエラーと警告の作成を補助し、ワークフロー内の関連するアクティビティに関する情報を提供する追加の検証アクティビティがいくつか用意されています。  
  
### <a name="assertvalidation-and-addvalidationerror"></a>AssertValidation と AddValidationError  
 <xref:System.Activities.Validation.AssertValidation> アクティビティは、その <xref:System.Activities.Validation.AssertValidation.Assertion%2A> プロパティから参照される式を評価します。また、式が `false` に評価されると、検証のエラーまたは警告が <xref:System.Activities.Validation.ValidationResults> に追加されます。 <xref:System.Activities.Validation.AssertValidation.Message%2A> プロパティは検証エラーを示し、<xref:System.Activities.Validation.AssertValidation.IsWarning%2A> は検証の失敗がエラーか警告かを指定します。 <xref:System.Activities.Validation.AssertValidation.IsWarning%2A> の既定値は `false` です。  
  
 次の例では、検証対象のアクティビティの <xref:System.Activities.Activity.DisplayName%2A> が 2 文字以下の場合、検証の警告を返す制約を宣言します。 <xref:System.Activities.Validation.Constraint%601> に使用されるジェネリック型パラメーターには、この制約によって検証されるアクティビティの型を指定します。 この制約では、ジェネリック型として <xref:System.Activities.Activity> を使用します。この制約はすべての種類のアクティビティに使用できます。  
  
```csharp  
public static Constraint ActivityDisplayNameIsNotSetWarning()  
{  
    DelegateInArgument<Activity> element = new DelegateInArgument<Activity>();  
  
    return new Constraint<Activity>  
    {  
        Body = new ActivityAction<Activity, ValidationContext>  
        {  
            Argument1 = element,  
            Handler = new AssertValidation  
            {  
                IsWarning = true,  
                Assertion = new InArgument<bool>(env => (element.Get(env).DisplayName.Length > 2)),  
                Message = new InArgument<string>("It is a best practice to have a DisplayName of more than 2 characters."),  
            }  
        }  
    };  
}  
```  
  
 あるアクティビティに対してこの制約を指定するには、次のコード例のように、アクティビティの <xref:System.Activities.Activity.Constraints%2A> に追加します。  
  
```csharp  
public sealed class SampleActivity : CodeActivity  
{  
    public SampleActivity()  
    {  
        base.Constraints.Add(ActivityDisplayNameIsNotSetWarning());  
    }  
  
    // Activity implementation omitted.  
}  
```  
  
 また、ホストは <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> を使用してワークフローでアクティビティの制約を指定することもできます。この方法については、次のセクションで説明します。  
  
 <xref:System.Activities.Validation.AddValidationError> アクティビティは、式を評価せずに、検証のエラーまたは警告を生成するために使用されます。 このプロパティは <xref:System.Activities.Validation.AssertValidation> に似ており、<xref:System.Activities.Statements.If> アクティビティなど、制約のフロー コントロール アクティビティと併用できます。
  
### <a name="workflow-relationship-activities"></a>ワークフロー関係のアクティビティ

複数の検証アクティビティが使用できます。これにより検証されるアクティビティに関連してワークフロー内の他のアクティビティに関する情報が提供されます。 <xref:System.Activities.Validation.GetParentChain> は現在のアクティビティとルート アクティビティ間のすべてのアクティビティを含むアクティビティのコレクションを返します。 <xref:System.Activities.Validation.GetChildSubtree> は再帰パターンで子アクティビティを含むアクティビティのコレクションを提供し、<xref:System.Activities.Validation.GetWorkflowTree> はワークフロー中のすべてのアクティビティを取得します。  
  
次の例では、 `CreateState` アクティビティを定義します。 `CreateState` アクティビティは `CreateCountry` アクティビティ内に含まれる必要があり、`GetParent` メソッドはこの要件を強制する制約を返します。 `GetParent` は <xref:System.Activities.Validation.GetParentChain> アクティビティを <xref:System.Activities.Statements.ForEach%601> アクティビティと組み合わせて使用し、`CreateState` のアクティビティの親アクティビティを確認し、要件を満たしているかどうか判断します。  
  
```csharp  
public sealed class CreateState : CodeActivity  
{  
    public CreateState()  
    {  
        base.Constraints.Add(CheckParent());  
        this.Cities = new List<Activity>();
    }  
  
    public List<Activity> Cities { get; set; }  
  
    public string Name { get; set; }
  
    static Constraint CheckParent()  
    {  
        DelegateInArgument<CreateState> element = new DelegateInArgument<CreateState>();  
        DelegateInArgument<ValidationContext> context = new DelegateInArgument<ValidationContext>();
        Variable<bool> result = new Variable<bool>();  
        DelegateInArgument<Activity> parent = new DelegateInArgument<Activity>();  
  
        return new Constraint<CreateState>  
        {
            Body = new ActivityAction<CreateState,ValidationContext>  
            {
                Argument1 = element,  
                Argument2 = context,  
                Handler = new Sequence  
                {  
                    Variables =  
                    {  
                        result
                    },  
                    Activities =  
                    {  
                        new ForEach<Activity>  
                        {
                            Values = new GetParentChain  
                            {  
                                ValidationContext = context
                            },  
                            Body = new ActivityAction<Activity>  
                            {
                                Argument = parent,
                                Handler = new If()  
                                {
                                    Condition = new InArgument<bool>((env) => object.Equals(parent.Get(env).GetType(),typeof(CreateCountry))),
                                    Then = new Assign<bool>  
                                    {  
                                        Value = true,  
                                        To = result  
                                    }  
                                }  
                            }
                        },  
                        new AssertValidation  
                        {  
                            Assertion = new InArgument<bool>(result),  
                            Message = new InArgument<string> ("CreateState has to be inside a CreateCountry activity"),
                        }  
                    }  
                }  
            }  
        };  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // not needed for the sample  
    }  
}  
```
  
## <a name="additional-constraints"></a>追加の制約  
 ワークフロー ホスト作成者は、ワークフロー内のアクティビティに追加の検証の制約を指定できます。この場合、制約を作成し、それを <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> インスタンスの <xref:System.Activities.Validation.ValidationSettings> ディクショナリに追加します。 <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> の各アイテムには、制約の適用対象であるアクティビティの種類と、その種類のアクティビティに対する追加の制約一覧が含まれます。 ワークフローで検証が呼び出されると、派生クラスを含め、指定した種類の各アクティビティは制約を評価します。 この例では、前のセクションの `ActivityDisplayNameIsNotSetWarning` 制約は、ワークフロー内のすべてのアクティビティに適用されます。  
  
```csharp  
Activity wf = new Sequence  
{  
    // Workflow Details Omitted.  
};  
  
ValidationSettings settings = new ValidationSettings()  
{  
  
    AdditionalConstraints =  
    {  
        {typeof(Activity), new List<Constraint> {ActivityDisplayNameIsNotSetWarning()}},
    }  
};  
  
// Validate the workflow.  
ValidationResults results = ActivityValidationServices.Validate(wf, settings);  
  
// Evaluate the results.  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error in " + error.Source.DisplayName + ": " + error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning in " + warning.Source.DisplayName + ": " + warning.Message);  
    }  
}  
```  
  
 <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> の <xref:System.Activities.Validation.ValidationSettings> プロパティが `true` の場合、<xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> を呼び出すことで検証が開始されると、指定した追加の制約のみが評価されます。 これは、特定の検証の構成についてワークフローを調べる場合に役立ちます。 ただし、ワークフローを呼び出すときに、ワークフロー内で構成されている検証ロジックが評価され、ワークフローが正常に開始するようにこれに合格する必要があります。 検証の呼び出しの詳細については、「[アクティビティ検証の呼び出し](invoking-activity-validation.md)」を参照してください。
