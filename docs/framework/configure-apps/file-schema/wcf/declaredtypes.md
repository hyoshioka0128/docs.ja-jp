---
title: <declaredTypes>
ms.date: 03/30/2017
helpviewer_keywords:
- dataContractSerializer element
- declaredTypes element
- DataContractSerializer
- KnownTypes
- <declaredTypes> element
ms.assetid: f35184e4-9d9e-4d37-8fb4-d5b58220eb3e
ms.openlocfilehash: c45a4e67d0a2d98c0e9c1a91e07f25b81370244c
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "70398060"
---
# \<declaredTypes>
逆シリアル化時に <xref:System.Runtime.Serialization.DataContractSerializer> が使用する既知の型が含まれています。  
  
 データコントラクトと既知の型の詳細については、「[データコントラクトの既知の型](../../../wcf/feature-details/data-contract-known-types.md)」を参照してください。  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.runtime.serialization>**](system-runtime-serialization.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<dataContractSerializer>**](datacontractserializer.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<declaredTypes>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<configuration>
  <system.runtime.serialization>
    <dataContractSerializer>
      <declaredTypes>
        <add type="String ">
          <knownType type="String">
            <parameter index="Integer"/>
          </knownType>
        </add>
      </declaredTypes>
    <dataContractSerializer>
  </system.runtime.serialization>
</configuration>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<add>](add-of-declaredtypes-element.md)|既知の型を必要とする型を追加します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<dataContractSerializer>](datacontractserializer-of-system-runtime-serialization.md)|<xref:System.Runtime.Serialization.DataContractSerializer> 用の設定データが含まれています。|  
  
## <a name="remarks"></a>解説  
 既知の型の詳細については、「[データコントラクトの既知の型](../../../wcf/feature-details/data-contract-known-types.md)」と「」を参照してください <xref:System.Runtime.Serialization.DataContractSerializer> 。  
  
## <a name="example"></a>例  
 次の XML コードは、要素に追加された宣言型と既知の型を示して `DataContractSerializer` います。 この例は、追加された 3 つの型を示しています。 最初の型は、"Item" という既知の型を使用する "Orders" という名前のカスタム型です。 2 つ目の宣言型は、既知の型として <xref:System.Collections.Generic.List%601> を使用する `Item` です。 最後の 3 つ目の宣言型は、<xref:System.Collections.Generic.Dictionary%602> です。 <xref:System.Collections.Generic.Dictionary%602> クラスの型は、2 種類のパラメーターを持つジェネリック型です。 最初のパラメーターはキーを表し、2 番目のパラメーターは値を表します。 次の例は、2 番目の型 (値) の <xref:System.Collections.Generic.List%601> を既知の型の一覧に追加します。 `index` 属性を使用して、既知の型で使用する型パラメーターを指定する必要があります。 この場合には、"1" に設定された index 属性 (コレクションは 0 から始まる) によって値型が示されます。  
  
```xml  
<configuration>
  <system.runtime.serialization>
    <dataContractSerializer>
      <declaredTypes>
        <add type="Examples.Types.Orders, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">
          <knownType type="Examples.Types.Item, SerializationTypes, Version=2.0.0.0, Culture=neutral, PublicKey=null" />
        </add>
        <add type="System.Collections.Generic.List`1, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">
          <knownType type="Examples.Types.Item, SerializationTypes, Version=2.0.0.0, Culture=neutral, PublicKey=null" />
        </add>
        <add type="System.Collections.Generic.Dictionary`2, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">
          <knownType type="System.Collections.Generic.List`1, SerializationTypes, Version = 2.0.0.0, Culture = neutral, PublicKeyToken=null">
            <parameter index="1"/>
          </knownType>
        </add>
      </declaredTypes>
    <dataContractSerializer>
  </system.runtime.serialization>
</configuration>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- [\<dataContractSerializer>](datacontractserializer-element.md)
- [既知のデータ コントラクト型](../../../wcf/feature-details/data-contract-known-types.md)
- [\<add>](add-of-declaredtypes-element.md)
