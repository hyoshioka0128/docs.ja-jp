---
title: '方法: ファイルがアセンブリであるかどうかを確認する'
description: この記事では、ファイルが .NET アセンブリであるかどうかを手動およびプログラムによって確認する方法について説明します。
ms.date: 08/19/2019
ms.assetid: ea5186bb-5bff-4dcb-bde9-d6ba4e2edd00
dev_langs:
- csharp
- vb
ms.openlocfilehash: fb1bcfa50ec380f10ab67cc47331f91dc3e4b32d
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83380140"
---
# <a name="how-to-determine-if-a-file-is-an-assembly"></a>方法: ファイルがアセンブリであるかどうかを確認する

ファイルが管理されていて、ファイルのメタデータにアセンブリ エントリが含まれている場合、そのファイルはアセンブリです。 アセンブリとメタデータの詳細については、「[アセンブリ マニフェスト](manifest.md)」を参照してください。  
  
## <a name="how-to-manually-determine-if-a-file-is-an-assembly"></a>ファイルがアセンブリかどうかを手動で確認する方法  
  
1. [Ildasm.exe (IL 逆アセンブラー)](../../framework/tools/ildasm-exe-il-disassembler.md) を起動します。  
  
2. テストするファイルを読み込みます。  
  
3. **ILDASM** で、そのファイルが移植可能な実行可能 (PE) ファイルではないと報告された場合、そのファイルはアセンブリでありません。 詳細については、トピック「[方法: アセンブリの内容を表示する](view-contents.md)」を参照してください。  
  
## <a name="how-to-programmatically-determine-if-a-file-is-an-assembly"></a>ファイルがアセンブリかどうかをプログラムによって確認する方法  
  
1. テストするファイルの完全パスと名前を渡して、<xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=nameWithType> メソッドを呼び出します。  
  
2. <xref:System.BadImageFormatException> 例外がスローされた場合、ファイルはアセンブリでありません。  
  
## <a name="example"></a>例  
次の例では、DLL がアセンブリかどうかをテストして確認します。  

```csharp
class TestAssembly  
{  
    static void Main()  
    {  
  
        try  
        {  
            System.Reflection.AssemblyName testAssembly =  
                System.Reflection.AssemblyName.GetAssemblyName(@"C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll");  
  
            System.Console.WriteLine("Yes, the file is an assembly.");  
        }  
  
        catch (System.IO.FileNotFoundException)  
        {  
            System.Console.WriteLine("The file cannot be found.");  
        }  
  
        catch (System.BadImageFormatException)  
        {  
            System.Console.WriteLine("The file is not an assembly.");  
        }  
  
        catch (System.IO.FileLoadException)  
        {  
            System.Console.WriteLine("The assembly has already been loaded.");  
        }  
    }  
}  
/* Output (with .NET Framework 3.5 installed):  
    Yes, the file is an assembly.  
*/  
```  

```vb  
Module Module1  
    Sub Main()  
        Try  
            Dim testAssembly As Reflection.AssemblyName =  
                                Reflection.AssemblyName.GetAssemblyName("C:\Windows\Microsoft.NET\Framework\v3.5\System.Net.dll")  
            Console.WriteLine("Yes, the file is an Assembly.")  
        Catch ex As System.IO.FileNotFoundException  
            Console.WriteLine("The file cannot be found.")  
        Catch ex As System.BadImageFormatException  
            Console.WriteLine("The file is not an Assembly.")  
        Catch ex As System.IO.FileLoadException  
            Console.WriteLine("The Assembly has already been loaded.")  
        End Try  
        Console.ReadLine()  
    End Sub  
End Module  
' Output (with .NET Framework 3.5 installed):  
'        Yes, the file is an Assembly.  
```

<xref:System.Reflection.AssemblyName.GetAssemblyName%2A> メソッドはテスト ファイルを読み込み、情報が読み取られた時点で解放します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Reflection.AssemblyName>
- [C# プログラミング ガイド](../../csharp/programming-guide/index.md)
- [プログラミングの概念 (Visual Basic)](../../visual-basic/programming-guide/concepts/index.md)
- [.NET のアセンブリ](index.md)
