---
title: <cryptographySettings> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings
- http://schemas.microsoft.com/.NetConfiguration/v2.0#cryptographySettings
helpviewer_keywords:
- cryptographySettings element
- <cryptographySettings> element
ms.assetid: 6201b7da-bcb7-49f7-b9f5-ba1fe05573b9
ms.openlocfilehash: fe6de09213c6f980e8eb205a318aae50033b2a84
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155233"
---
# <a name="cryptographysettings-element"></a>\<cryptographySettings> 要素
暗号設定を含みます。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<mscorlib>**](mscorlib-element-for-cryptography-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<cryptographySettings>**

## <a name="syntax"></a>構文  
  
```xml  
      <cryptographySettings>
</cryptographySettings>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<cryptoNameMapping>](cryptonamemapping-element.md)|表示名へのクラスのマッピングを含みます。|  
|[\<oidMap>](oidmap-element.md)|クラスに対する asn.1 オブジェクト識別子 (OID) マッピングが含まれています。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`mscorlib`|要素が含まれてい `cryptographySettings` ます。|  
  
## <a name="example"></a>例  
 次の例では、要素を使用して、 **\<cryptographySettings>** 暗号化名マッピングと OID マッピングを格納する方法を示します。 この例では、がオブジェクトを返すようにランタイムを構成 <xref:System.Security.Cryptography.HashAlgorithm.Create%2A?displayProperty=nameWithType> `MyHashClass` し、クラスを `MyCryptoClass` オブジェクト識別子1.3.36.2.1 にマップします。  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyHash="MyHashClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
               <cryptoClass   MyCrypto="MyCryptoClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="System.Security.Cryptography.HashAlgorithm"  
                       class="MyHash"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.36.3.2.1"   name="MyCryptoClass"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [構成ファイル スキーマ](../index.md)
- [暗号設定スキーマ](index.md)
- [暗号化サービス](../../../../standard/security/cryptographic-services.md)
