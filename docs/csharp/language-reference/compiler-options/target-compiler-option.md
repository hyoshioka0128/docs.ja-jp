---
title: -target (C# コンパイラ オプション)
ms.date: 07/20/2015
f1_keywords:
- /target
helpviewer_keywords:
- target compiler options [C#]
- /target compiler options [C#]
- assemblies [C#], compiling
- -target compiler options [C#]
ms.assetid: a18bbd8e-bbf7-49e7-992c-717d0eb1f76f
ms.openlocfilehash: ea5481810e629d911c4d5aba62e60c98d0783f34
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81644355"
---
# <a name="-target-c-compiler-options"></a>-target (C# コンパイラ オプション)
**-target** コンパイラ オプションは、次の 6 つの形式のいずれかで指定できます。  
  
 [/target:appcontainerexe](./target-appcontainerexe-compiler-option.md)  
 Windows 8.x Store アプリの .exe ファイルを作成する場合。  
  
 [/target:exe](./target-exe-compiler-option.md)  
 .exe ファイルを作成する場合。  
  
 [/target:library](./target-library-compiler-option.md)  
 コード ライブラリを作成する場合。  
  
 [/target:module](./target-module-compiler-option.md)  
 モジュールを作成する場合。  
  
 [/target:winexe](./target-winexe-compiler-option.md)  
 Windows プログラムを作成する場合。  
  
 [/target:winmdobj](./target-winmdobj-compiler-option.md)  
 .winmdobj 中間ファイルを作成する場合。  
  
 **-target:module** を指定しない限り、 **-target** を使用すると、.NET Framework のアセンブリ マニフェストが出力ファイルに配置されます。 詳細については、「[.NET のアセンブリ](../../../standard/assembly/index.md)」と「[共通の属性](../attributes/global.md)」を参照してください。  
  
 アセンブリ マニフェストは、コンパイル中の最初の .exe 出力ファイルに配置されます。 .exe 出力ファイルがない場合には、最初の DLL ファイルに配置されます。 たとえば、次のコマンド ラインでは、マニフェストは `1.exe` に配置されます。  
  
```console  
csc -out:1.exe t1.cs -out:2.netmodule t2.cs  
```  
  
 コンパイラの 1 回のコンパイルで作成されるアセンブリ マニフェストは 1 つだけです。 コンパイルにおけるすべてのファイルの情報は、アセンブリ マニフェストに含まれます。 **-target:module** で作成されたもの以外のすべての出力ファイルには、アセンブリ マニフェストを含めることができます。 コマンド ラインで複数の出力ファイルを生成する場合は、アセンブリ マニフェストを 1 つだけ作成できます。このアセンブリ マニフェストは、コマンド ラインで指定した最初の出力ファイルに含める必要があります。 最初の出力ファイル ( **-target:exe**、 **-target:winexe**、 **-target:library**、 **-target:module**) にかかわらず、同じコンパイルで生成された他の出力ファイルはすべてモジュール ( **-target:module**) でなければなりません。  
  
 アセンブリを作成する場合は、<xref:System.CLSCompliantAttribute> 属性を使用して、コードのすべてまたは一部が CLS 準拠であることを指定できます。  
  
```csharp  
// target_clscompliant.cs  
[assembly:System.CLSCompliant(true)]   // specify assembly compliance  
  
[System.CLSCompliant(false)]   // specify compliance for an element  
public class TestClass  
{  
    public static void Main() {}  
}  
```  
  
 このコンパイラ オプションのプログラムによる設定の詳細については、「<xref:VSLangProj80.ProjectProperties3.OutputType%2A>」を参照してください。  
  
## <a name="see-also"></a>参照

- [C# コンパイラ オプション](./index.md)
- [プロジェクトおよびソリューションのプロパティの管理](/visualstudio/ide/managing-project-and-solution-properties)
- [-subsystemversion (C# コンパイラ オプション)](./subsystemversion-compiler-option.md)
