---
title: <compilers> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#compilers
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom/compilers
helpviewer_keywords:
- compiler configuration elements, <compilers> element
- <compilers> element
- compilers element
ms.assetid: d40fba59-98f9-4783-ae0c-2ebea27ce77b
ms.openlocfilehash: 09b1efe321c39402c9280eda0e9def9112462470
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155415"
---
# <a name="compilers-element"></a>\<compilers> 要素
コンパイラ構成要素のコンテナー。0個以上の要素が含まれてい [\<compiler>](compiler-element.md) ます。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.codedom>**](system-codedom-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<compilers>**

## <a name="syntax"></a>構文  
  
```xml  
<compilers>  
  <compiler ... />  
</compilers>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<compiler>Element](compiler-element.md)|言語プロバイダーのコンパイラ構成属性を指定します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<configuration>Element](../configuration-element.md)|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
|[\<system.codedom>Element](system-codedom-element.md)|使用可能な言語プロバイダーのコンパイラ構成設定を指定します。|  
  
## <a name="remarks"></a>解説  
 要素には、 [\<compilers>](compilers-element.md) コンピューター上の言語プロバイダーのコンパイラ構成設定が含まれています。 各 [\<compiler>](compiler-element.md) 要素は、特定の言語プロバイダーのコンパイラ構成属性を指定します。  
  
 .NET Framework は、マシン構成ファイル (machine.config) の初期コンパイラおよび言語プロバイダー設定を定義します。 開発者やコンパイラ ベンダーは、新しい <xref:System.CodeDom.Compiler.CodeDomProvider?displayProperty=nameWithType> の実装のために構成設定を追加することができます。 <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=nameWithType> メソッドを使用して、プログラムによってコンピューターの言語プロバイダーとコンパイラ構成の設定を列挙します。  
  
## <a name="configuration-file"></a>構成ファイル  
 この要素は、マシン構成ファイルおよびアプリケーション構成ファイルで使用できます。  
  
## <a name="example"></a>例  
 次の例は、一般的なコンパイラ構成要素を示しています。  
  
```xml  
<configuration>  
   <system.codedom>  
     <compilers>  
       <!-- zero or more compiler elements -->  
       <compiler
          language="c#;cs;csharp"
          extension=".cs"  
          type="Microsoft.CSharp.CSharpCodeProvider, System, Version=1.0.5000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
          compilerOptions=""
          warningLevel="1" />  
     </compilers>  
   </system.codedom>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.CodeDom.Compiler.CompilerInfo>
- <xref:System.CodeDom.Compiler.CodeDomProvider>
- [構成ファイル スキーマ](../index.md)
- [コンパイラおよび言語プロバイダー設定のスキーマ](index.md)
- [\<compiler>Element](compiler-element.md)
