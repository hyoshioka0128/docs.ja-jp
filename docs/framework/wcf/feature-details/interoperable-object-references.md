---
title: 相互運用可能なオブジェクト参照
ms.date: 04/15/2019
ms.assetid: cb8da4c8-08ca-4220-a16b-e04c8f527f1b
ms.openlocfilehash: 0927f217a1666f8f27ca9c3e68f80a96b9c0f2b1
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184702"
---
# <a name="interoperable-object-references"></a>相互運用可能なオブジェクト参照
既定では、<xref:System.Runtime.Serialization.DataContractSerializer>オブジェクトを値でシリアル化します。 このプロパティを<xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A>使用すると、オブジェクトをシリアル化するときにオブジェクト参照を保持するようにデータ コントラクト シリアライザーに指示できます。  
  
## <a name="generated-xml"></a>生成される XML  
 例として、次のオブジェクトを考えます。  
  
```csharp  
[DataContract]  
public class X  
{  
    SomeClass someInstance = new SomeClass();  
    [DataMember]  
    public SomeClass A = someInstance;  
    [DataMember]  
    public SomeClass B = someInstance;  
}  
  
public class SomeClass
{  
}  
```  
  
 <xref:System.Runtime.Serialization.DataContractSerializer.PreserveObjectReferences%2A> を `false` (既定値) に設定すると、次の XML が生成されます。  
  
```xml  
<X>  
   <A>contents of someInstance</A>  
   <B>contents of someInstance</B>  
</X>  
```  
  
 <xref:System.Runtime.Serialization.DataContractSerializer.PreserveObjectReferences%2A> を `true` に設定すると、次の XML が生成されます。  
  
```xml  
<X>  
   <A id="1">contents of someInstance</A>  
   <B ref="1"></B>  
</X>  
```  
  
 ただし、<xref:System.Runtime.Serialization.XsdDataContractExporter>プロパティ`id`が`ref``true`に設定されている場合でも、スキーマの属性と`preserveObjectReferences`属性は記述しません。  
  
## <a name="using-isreference"></a>IsReference の使用  
 スキーマに従って有効なオブジェクト参照情報を生成するには、<xref:System.Runtime.Serialization.DataContractAttribute>属性を型に適用し、<xref:System.Runtime.Serialization.DataContractAttribute.IsReference%2A>フラグを に`true`設定します。 次の例では、前`X`の例のクラスを追加`IsReference`して変更します。  
  
```csharp
[DataContract(IsReference=true)]
public class X
{  
     SomeClass someInstance = new SomeClass();
     [DataMember]
     public SomeClass A = someInstance;
     [DataMember]
     public SomeClass B = someInstance;
}
  
public class SomeClass
{
}  
````

 次のような XML が生成されます。  

```xml
<X>  
    <A id="1">
        <Value>contents of A</Value>  
    </A>
    <B ref="1"></B>  
</X>
```  
  
 `IsReference` を使用すると、メッセージのラウンド トリップに対応できます。 この機能を使用しない場合、型がスキーマから生成される場合、その型の XML 出力は、当初想定されていたスキーマと必ずしも互換性があるとは限りません。 つまり、`id` 属性と `ref` 属性がシリアル化されたとしても、元のスキーマによってこれらの属性 (またはすべての属性) が拒否される可能性があります。 データ`IsReference`メンバーに適用すると、ラウンド トリップ時にメンバーが*参照可能*であると認識され続けます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.CollectionDataContractAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute.IsReference?displayProperty=nameWithType>
- <xref:System.Runtime.Serialization.CollectionDataContractAttribute.IsReference?displayProperty=nameWithType>
