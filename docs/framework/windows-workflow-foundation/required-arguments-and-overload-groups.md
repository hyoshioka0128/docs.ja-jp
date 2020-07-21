---
title: 必須の引数とオーバーロード グループ
ms.date: 03/30/2017
ms.assetid: 4ca3ed06-b9af-4b85-8b70-88c2186aefa3
ms.openlocfilehash: 4eb62306f52b8ff890d5a5333c3789bd84ad7f60
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142941"
---
# <a name="required-arguments-and-overload-groups"></a>必須の引数とオーバーロード グループ
アクティビティは、アクティビティの実行を有効にするためには特定の引数をバインドする必要があるように構成できます。 `RequiredArgument` 属性は、アクティビティの特定の引数が必須であることを示す場合に使用します。また、`OverloadGroup` 属性は、必須の引数のカテゴリをグループ化する場合に使用します。 これらの属性を使用することで、アクティビティ作成者は、単純なアクティビティ検証の構成も複雑な構成も適用できます。  
  
## <a name="using-required-arguments"></a>必須の引数の使用  
 アクティビティで `RequiredArgument` 属性を使用するためには、<xref:System.Activities.RequiredArgumentAttribute> を使用して目的の引数を指定します。 次の例では、2 つの必須引数がある `Add` アクティビティが定義されています。  
  
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
  
 また、XAML では、必須引数の指定に <xref:System.Activities.RequiredArgumentAttribute> も使用されます。 この例では、3 つの引数を使用して `Add` アクティビティを定義し、<xref:System.Activities.Statements.Assign%601> アクティビティを使用して追加操作を実行します。  
  
```xaml  
<Activity x:Class="ValidationDemo.Add" ...>  
  <x:Members>  
    <x:Property Name="Operand1" Type="InArgument(x:Int32)">  
      <x:Property.Attributes>  
        <RequiredArgumentAttribute />  
      </x:Property.Attributes>  
    </x:Property>  
    <x:Property Name="Operand2" Type="InArgument(x:Int32)">  
      <x:Property.Attributes>  
        <RequiredArgumentAttribute />  
      </x:Property.Attributes>  
    </x:Property>  
    <x:Property Name="Result" Type="OutArgument(x:Int32)" />  
  </x:Members>  
  <Assign>  
    <Assign.To>  
      <OutArgument x:TypeArguments="x:Int32">[Result]</OutArgument>  
    </Assign.To>  
    <Assign.Value>  
      <InArgument x:TypeArguments="x:Int32">[Operand1 + Operand2]</InArgument>  
    </Assign.Value>  
  </Assign>  
</Activity>  
```  
  
 アクティビティが使用され、いずれかの必須引数がバインドされていない場合は、次の検証エラーが返されます。  
  
 **必須のアクティビティ引数 'Operand1' の値が指定されませんでした。**  
> [!NOTE]
> 検証エラーと警告のチェックと処理の詳細については、「[アクティビティ検証の呼び出し](invoking-activity-validation.md)」を参照してください。  
  
## <a name="using-overload-groups"></a>オーバーロード グループの使用

オーバーロード グループには、あるアクティビティ内で有効である引数の組み合わせを示すメソッドが用意されています。 引数は <xref:System.Activities.OverloadGroupAttribute> を使用してグループ化されます。 各グループには、 で指定された名前が<xref:System.Activities.OverloadGroupAttribute>付けられます。 このアクティビティは、オーバーロード グループ内の引数のセットが 1 つだけバインドされている場合に有効です。 次の例では、`CreateLocation` クラスを定義します。  
  
```csharp  
class CreateLocation: Activity  
{  
    [RequiredArgument]  
    public InArgument<string> Name { get; set; }  
  
    public InArgument<string> Description { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G1")]  
    public InArgument<int> Latitude { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G1")]  
    public InArgument<int> Longitude { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    [OverloadGroup("G3")]  
    public InArgument<string> Street { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    public InArgument<string> City { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    public InArgument<string> State { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G3")]  
    public InArgument<int> Zip { get; set; }
}  
```  
  
 このアクティビティの目的は、米国内の場所を指定することです。 これを行うために、アクティビティのユーザーは、3 つある引数グループの 1 つを使用して場所を指定できます。 有効な組み合わせで引数を指定するために、3 種類のオーバーロード グループを定義しています。 `G1` 含む、 `Latitude` と `Longitude` 引数。 `G2` には `Street`、`City`、および `State` が含まれます。 `G3` には `Street` および `Zip` が含まれます。 `Name` も必要な引数ですが、オーバーロード グループの一部ではありません。 このアクティビティが有効であるためには、`Name` が、1 つのオーバーロード グループのみに含まれるすべての引数とバインドされている必要があります。  
  
 次の例では、[データベース アクセス アクティビティ](./samples/database-access-activities.md)のサンプルから取得したオーバーロード グループと`ConnectionString``ConfigFileSectionName`の 2 つのオーバーロード グループがあります。 このアクティビティが有効であるためには、引数 `ProviderName` および `ConnectionString` がバインドされているか、または引数 `ConfigName` がバインドされている必要があります。両方がバインドされている場合は無効です。  
  
```csharp  
public class DbUpdate: AsyncCodeActivity  
{  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DefaultValue(null)]  
    public InArgument<string> ProviderName { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DependsOn("ProviderName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConnectionString { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConfigFileSectionName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConfigName { get; set; }  
  
    [DefaultValue(null)]  
    public CommandType CommandType { get; set; }  
  
    [RequiredArgument]  
    public InArgument<string> Sql { get; set; }  
  
    [DependsOn("Sql")]  
    [DefaultValue(null)]  
    public IDictionary<string, Argument> Parameters { get; }  
  
    [DependsOn("Parameters")]  
    public OutArgument<int> AffectedRecords { get; set; }
}  
```  
  
 オーバーロード グループを定義するときは次の点に注意してください。  
  
- オーバーロード グループを別のオーバーロード グループのサブセットまたは等価セットにすることはできません。  
  
    > [!NOTE]
    > この規則には例外が 1 つあります。 オーバーロード グループが別のオーバーロード グループのサブセットであり、サブセットに `RequiredArgument` が `false` である引数のみが含まれている場合、オーバーロード グループは有効です。  
  
- 複数のオーバーロード グループが重なり合うように定義することは可能です。ただし、グループの共通部分には、一方または両方のオーバーロード グループの必須引数すべてを含めることはできません。 前の例では、オーバーロード グループ `G2` および `G3` が重なり合っていますが、共通部分に一方または両方のグループの引数すべてを含めてはいないため、有効です。  
  
 オーバーロード グループの引数をバインドするときは次の点に注意してください。  
  
- オーバーロード グループ内の `RequiredArgument` 引数すべてがバインドされている場合、そのグループはバインドされていると見なされます。  
  
- グループに `RequiredArgument` 引数がなく、1 つ以上の引数がバインドされている場合、そのグループはバインドされていると見なされます。  
  
- バインドされているオーバーロード グループが 1 つもない状態は、検証エラーになります。ただし、`RequiredArgument` 引数を 1 つも含まないオーバーロード グループが 1 つある場合は有効です。  
  
- 複数のオーバーロード グループをバインドすることはできません。つまり、1 つのオーバーロード グループの必須引数すべてをバインドしているのに加えて、別のオーバーロード グループのいずれかの引数もバインドしている場合は、エラーになります。
