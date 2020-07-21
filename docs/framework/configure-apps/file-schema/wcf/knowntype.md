---
title: <knownType>
ms.date: 03/30/2017
ms.assetid: ee2b7be3-7148-4a3a-b861-48e7330615e5
ms.openlocfilehash: 61f51b2ecd572ba254317a01e0f514503c7cc9e4
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70397874"
---
# \<knownType>
逆シリアル化中に <xref:System.Runtime.Serialization.DataContractSerializer> によって使用される型を指定します。 この要素には、"宣言型" のフィールドまたはプロパティによって返される "既知の型" を指定します。 詳細については、「[データコントラクトの既知の型](../../../wcf/feature-details/data-contract-known-types.md)」を参照してください。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.serialization>**](system-runtime-serialization.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<dataContractSerializer>**](datacontractserializer.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<declaredTypes>**](declaredtypes.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<add>**](add-of-declaredtypes-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<knownType>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<knownType type="String">
  <parameter index="Integer"
             type="String" />
</knownType>
```  
  
## <a name="type"></a>Type  
 `string`  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|type|型 (名前空間を含む)、アセンブリ名、バージョン、カルチャ、および公開キー トークンを指定します。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<parameter>](parameter.md)|宣言型がジェネリック型である場合に、パラメーター インデックスを指定します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|Description|  
|-------------|-----------------|  
|[\<add>](add-of-declaredtypes-element.md)|宣言されたタイプのコレクションに、宣言されたタイプを追加します。|  
  
## <a name="remarks"></a>解説  
 既知の型の詳細については、「[データコントラクトの既知の型](../../../wcf/feature-details/data-contract-known-types.md)」と「」を参照してください <xref:System.Runtime.Serialization.DataContractSerializer> 。  
  
 [\<dataContractSerializer>](datacontractserializer-element.md)この要素の使用例については、「」を参照してください。  
  
## <a name="example"></a>例  
  
```xml  
<add type="MyCompany.Library.Shape,
           MyAssembly, Version=2.0.0.0, Culture=neutral,
           PublicKeyToken=XXXXXX, processorArchitecture=MSIL">
  <knownType type="MyCompany.Library.Circle,
                   MyAssembly, Version=2.0.0.0, Culture=neutral,
                   PublicKeyToken=XXXXXX,
                   processorArchitecture=MSIL"/>
</add>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- [既知のデータ コントラクト型](../../../wcf/feature-details/data-contract-known-types.md)
- [\<dataContractSerializer>](datacontractserializer-element.md)
- [\<add>](add-of-declaredtypes-element.md)
