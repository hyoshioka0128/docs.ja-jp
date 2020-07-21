---
title: <system.codedom> 要素
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.codedom
- http://schemas.microsoft.com/.NetConfiguration/v2.0#system.codedom
helpviewer_keywords:
- compiler configuration elements, <system.codedom> element
- system.codedom element
- <system.codedom> element
ms.assetid: 672a68f7-e69f-4479-ac30-e980085ec4fe
ms.openlocfilehash: 40a3c84e1deed4d215383670176623a6a79ac41d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155389"
---
# <a name="systemcodedom-element"></a>\<system.codedom> 要素
使用可能な言語プロバイダーのコンパイラ構成設定を指定します。  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;**\<system.codedom>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.codedom>  
  <compilers> ... </compilers>  
</system.codedom>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<compilers>](compilers-element.md)|コンパイラ構成要素のコンテナー。0個以上の要素が含まれてい [\<compiler>](compiler-element.md) ます。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[\<configuration>](../configuration-element.md)|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|  
  
## <a name="remarks"></a>解説  
  
## <a name="net-framework-version-20"></a>.NET Framework バージョン2.0  
 要素には、およびなど、 [\<system.codedom>](system-codedom-element.md) .NET Framework と共にインストールされる既定のプロバイダーに加えて、コンピューターにインストールされている言語プロバイダーのコンパイラ構成設定が含まれてい <xref:Microsoft.CSharp.CSharpCodeProvider> <xref:Microsoft.VisualBasic.VBCodeProvider> ます。 [\<compilers>](compilers-element.md)要素に0個以上の要素が含まれてい [\<compiler>](compiler-element.md) ます。 各 [\<compiler>](compiler-element.md) 要素は、特定の言語プロバイダーのコンパイラ構成属性を指定します。  
  
 開発者やコンパイラベンダーは、新しい実装のために構成設定をマシン構成ファイル (machine.config) に追加でき <xref:System.CodeDom.Compiler.CodeDomProvider> ます。 メソッドを使用して、 <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=nameWithType> コンピューター上のコンパイラ構成設定によって識別される既定の言語プロバイダーと言語プロバイダーの両方をプログラムによって列挙します。  
  
> [!NOTE]
> .NET Framework バージョン1.0 および1.1 では、.NET Framework によって提供される既定の言語プロバイダーが要素で識別され [\<compilers>](compilers-element.md) ます。 .NET Framework バージョン2.0 では、既定の言語プロバイダーは要素で識別されません [\<compilers>](compilers-element.md) が、メソッドを使用して列挙でき <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A> ます。  
  
## <a name="net-framework-versions-10-and-11"></a>.NET Framework バージョン1.0 および1.1  
 要素には、 [\<system.codedom>](system-codedom-element.md) コンピューター上の言語プロバイダーのコンパイラ構成設定が含まれています。 [\<compilers>](compilers-element.md)要素に0個以上の要素が含まれてい [\<compiler>](compiler-element.md) ます。 各 [\<compiler>](compiler-element.md) 要素は、特定の言語プロバイダーのコンパイラ構成属性を指定します。  
  
 .NET Framework は、マシン構成ファイル (Machine.config) 内でコンパイラの初期設定を定義します。 開発者やコンパイラ ベンダーは、新しい <xref:System.CodeDom.Compiler.CodeDomProvider> の実装のために構成設定を追加することができます。 <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=nameWithType> メソッドを使用して、プログラムによってコンピューターの言語プロバイダーとコンパイラ構成の設定を列挙します。  
  
## <a name="configuration-file"></a>構成ファイル  
 この要素は、マシン構成ファイルおよびアプリケーション構成ファイルで使用できます。  
  
## <a name="example"></a>例  
 次の例は、一般的なコンパイラ構成を示しています。  
  
```xml  
<configuration>  
  <system.codedom>  
    <compilers>  
      <!-- zero or more compiler elements -->  
      <compiler
        language="c#;cs;csharp"  
        extension=".cs"  
        type="Microsoft.CSharp.CSharpCodeProvider, System,
          Version=1.0.5000.0, Culture=neutral,
          PublicKeyToken=b77a5c561934e089"  
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
