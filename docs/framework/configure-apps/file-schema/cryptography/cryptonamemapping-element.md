---
title: <cryptoNameMapping> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#cryptoNameMapping
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/cryptoNameMapping
helpviewer_keywords:
- <cryptoNameMapping> element
- cryptoNameMapping element
ms.assetid: c59c9494-149b-4ce6-b38d-371f896ae85c
ms.openlocfilehash: d31c5cd52ffe0e2a6eb5784735e76436d216444b
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155220"
---
# <a name="cryptonamemapping-element"></a>\<cryptoNameMapping> 要素
表示名へのクラスのマッピングを含みます。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<mscorlib>**](mscorlib-element-for-cryptography-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<cryptographySettings>**](cryptographysettings-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<cryptoNameMapping>**

## <a name="syntax"></a>構文  
  
```xml  
      <cryptoNameMapping>
</cryptoNameMapping>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|`cryptoClasses`|要素内の表示名へのマッピングを持つ暗号化クラスの一覧が含まれてい **\<nameEntry>** ます。|  
|`nameEntry`|アルゴリズムの表示名にクラス名をマップして、1 つのクラスが多くの表示名を持つことを許可します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|`configuration`|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|`cryptographySettings`|暗号設定を含みます。|  
|`cryptoNameMapping`|表示名へのクラスのマッピングを含みます。|  
|`mscorlib`|要素が含まれてい \<cryptographySettings> ます。|  
  
## <a name="example"></a>例  
 次の例は、要素を使用して **\<cryptoNameMapping>** 暗号化クラスを参照し、ランタイムを構成する方法を示しています。 その後、文字列 "RSA" をメソッドに渡し <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=nameWithType> 、メソッドを使用して <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create%2A> オブジェクトを返すことができ `MyCryptoRSAClass` ます。  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyCryptoRSA="MyCryptoRSAClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="RSA" class="MyCryptoRSA"/>  
            <nameEntry name="System.Security.Cryptography.AsymmetricAlgorithm"  
                       class="MyCryptoRSA"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [構成ファイル スキーマ](../index.md)
- [暗号設定スキーマ](index.md)
- [暗号化サービス](../../../../standard/security/cryptographic-services.md)
- [暗号化クラスの設定](../../configure-cryptography-classes.md)
