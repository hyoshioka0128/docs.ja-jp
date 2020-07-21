---
title: <add><declaredTypes>要素の
ms.date: 03/30/2017
helpviewer_keywords:
- data contracts
- dataContractSerializer element
- DataContractSerializer
- DataContractAttribute
ms.assetid: c3d37ae4-8f1c-463f-b195-658c5a7e90a1
ms.openlocfilehash: a001e8743b2c24f68b1b23cbccf3e5ac162c4e71
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70400658"
---
# <a name="add-of-declaredtypes-element"></a>\<add>\<declaredTypes>要素の
逆シリアル化中に、<xref:System.Runtime.Serialization.DataContractSerializer> で使用される型を追加します。 各宣言型は、宣言型のフィールドまたはプロパティとして返される既知の型を含みます。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.serialization>**](system-runtime-serialization.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<dataContractSerializer>**](datacontractserializer.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<declaredTypes>**](declaredtypes.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<add type="String">
  <knownType type="String">
    <parameter index="Integer"
               type="String" />
  </knownType>
</add>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|type|必須の文字列属性です。<br /><br /> 型名 (名前空間を含む)、アセンブリ名、バージョン番号、カルチャ、および公開キー トークンを指定します。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<knownType>](knowntype.md)|追加される宣言型の既知の型を指定します。 宣言型がジェネリック型の場合は、既知の型を返すために使用されるジェネリック パラメーターを指定するために、`<knownType>` にパラメーター要素も追加する必要があります。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<declaredTypes>](declaredtypes.md)|<xref:System.Runtime.Serialization.DataContractSerializer> による逆シリアル化中に既知のタイプを必要とするタイプが含まれています。|  
  
## <a name="remarks"></a>解説  
 既知の型の詳細については、「[データコントラクトの既知の型](../../../wcf/feature-details/data-contract-known-types.md)」と「」を参照してください <xref:System.Runtime.Serialization.DataContractSerializer> 。  
  
 [\<dataContractSerializer>](datacontractserializer-element.md)この要素の使用例については、「」を参照してください。  
  
> [!NOTE]
> <xref:System.Object> 型を `<declaredType>` として追加すると、<xref:System.Configuration.ConfigurationErrorsException> がスローされます。 これは、構成で <xref:System.Object> 型を宣言型として使用できないためです。  
  
## <a name="example"></a>例  
  
```xml  
<add type="MyCompany.Library.Shape,
           MyAssembly, Version=2.0.0.0, Culture=neutral,
           PublicKeyToken=XXXXXX, processorArchitecture=MSIL">
  <knownType type="MyCompany.Library.Circle,
                   MyAssembly, Version=2.0.0.0, Culture=neutral,
                   PublicKeyToken=XXXXXX,
                   processorArchitecture=MSIL" />
</add>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- [既知のデータ コントラクト型](../../../wcf/feature-details/data-contract-known-types.md)
- [\<dataContractSerializer>](datacontractserializer-element.md)
- [\<add>の\<declaredTypes>](add-of-declaredtypes-element.md)
