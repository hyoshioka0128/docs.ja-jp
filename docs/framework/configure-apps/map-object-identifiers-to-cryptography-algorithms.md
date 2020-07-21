---
title: 暗号化アルゴリズムへのオブジェクト ID の割り当て
description: XML 構成ファイルの oidEntry および nameEntry 要素を使用して、.NET で暗号化アルゴリズムにオブジェクト識別子 (OID) をマップする方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- digital signatures
- identifiers, mapping object identifiers
- cryptographic algorithms
- mapping object identifiers
- cryptography, mapping object identifiers
ms.assetid: c9673f81-bf9e-47fd-bc6f-6bc1c1c4c15e
ms.openlocfilehash: e22510014071455b83ba28cd82690b5ecdce9bc9
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2020
ms.locfileid: "85142005"
---
# <a name="mapping-object-identifiers-to-cryptography-algorithms"></a>暗号化アルゴリズムへのオブジェクト ID の割り当て
デジタル署名は、あるプログラムから別のプログラムに送信されるときに、データが改ざんされないようにします。 通常、デジタル署名は、署名されるデータのハッシュに数学関数を適用することによって計算されます。 署名するハッシュ値の書式を設定すると、一部のデジタル署名アルゴリズムでは、書式設定操作の一部として asn.1 オブジェクト識別子 (OID) が追加されます。 OID は、ハッシュの計算に使用されたアルゴリズムを識別します。 アルゴリズムをオブジェクト識別子にマップして、カスタムアルゴリズムを使用するように暗号化メカニズムを拡張することができます。 次の例では、オブジェクト識別子を新しいハッシュアルゴリズムにマップする方法を示します。  
  
```xml  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MyNewHash="MyNewHashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="NewHash" class="MyNewHash"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.14.33.42.46"  name="NewHash"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 [ \<oidEntry> 要素](./file-schema/cryptography/oidentry-element.md)には、2つの属性が含まれています。 **OID**属性は、オブジェクトの識別子番号です。 **Name**属性は、 [ \<nameEntry> 要素](./file-schema/cryptography/nameentry-element.md)の**name**属性の値です。 オブジェクト識別子を簡易名にマップする前に、アルゴリズム名からクラスへのマッピングが必要です。  
  
## <a name="see-also"></a>関連項目

- [暗号化クラスの設定](configure-cryptography-classes.md)
- [Cryptographic Services](../../standard/security/cryptographic-services.md)
