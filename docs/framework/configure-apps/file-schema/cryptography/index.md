---
title: 暗号設定スキーマ
ms.date: 03/30/2017
helpviewer_keywords:
- configuration schema [.NET Framework], cryptography
- elements [.NET Framework], cryptography
- schema configuration settings
- cryptography, settings schema
- cryptography, mapping algorithm names
- configuration sections [.NET Framework]
- configuration settings [.NET Framework], cryptography
ms.assetid: 1f55050a-b2a3-4868-a3c0-da20826150f3
ms.openlocfilehash: 474c3274bfba6803ebb17289f138251d755250e4
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71699804"
---
# <a name="cryptography-settings-schema"></a>暗号設定スキーマ
暗号設定スキーマには、アルゴリズムの表示名を、暗号化アルゴリズムを実装するクラスに割り当てる方法を指定する要素が含まれます。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **\<mscorlib >** ](mscorlib-element-for-cryptography-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t-3[ **\<cryptographySettings >** ](cryptographysettings-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5[ **\<cryptoNameMapping >** を行います。](cryptonamemapping-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5 @ no__t-6 @ no__t-7[ **&nbsp;0cryptoClasses (10) >** ](cryptoclasses-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5 @ no__t @ no__t @ no__t-7 @ no__t-8 @-9[ **&nbsp;2cryptoClass** (&) >](cryptoclass-element.md)  
&nbsp; @ no__t @ no__t @ no__t @ no__t @ no__t @ no__t-6 @-7[ **&nbsp;0nameEntry > を入力**します。](nameentry-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5[ **\<oidMap >** を行います。](oidmap-element.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5 @ no__t-6[ **\<oidEntry >** します。](oidentry-element.md)  
  
|要素|説明|  
|-------------|-----------------|  
|[ **\<cryptoClasses**>](cryptoclasses-element.md)|**\<nameEntry>** 要素内の表示名へのマッピングを持つ暗号化クラスのリストを含みます。|  
|[ **\<cryptoClass**>](cryptoclass-element.md)|**\<nameEntry>** 要素内の表示名へのマッピングを持つ暗号化クラスを含みます。|  
|[ **\<cryptographySettings**>](cryptographysettings-element.md)|暗号設定を含みます。|  
|[ **\<cryptoNameMapping**>](cryptonamemapping-element.md)|表示名へのクラスのマッピングを含みます。|  
|[ **\<mscorlib>** 要素、暗号化設定用](mscorlib-element-for-cryptography-settings.md)|**\<cryptographySettings >** 要素を含みます。|  
|[ **\<nameEntry>** ](nameentry-element.md)|アルゴリズムの表示名にクラス名をマップして、1 つのクラスが多くの表示名を持つことを許可します。|  
|[ **\<oidEntry>** ](oidentry-element.md)|ASN.1 オブジェクト識別子 (OID) を表示名にマップします。|  
|[ **\<oidMap>** ](oidmap-element.md)|クラスへの ASN.1 OID マッピングを含みます。|  
  
## <a name="see-also"></a>関連項目

- [構成ファイル スキーマ](../index.md)
- [Cryptographic Services](../../../../standard/security/cryptographic-services.md)
