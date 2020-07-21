---
title: テキスト ファイルを 1 行ずつ読み取る方法 - C# プログラミング ガイド
ms.date: 07/20/2015
helpviewer_keywords:
- ReadLine method [C#]
- reading text files, line by line
- text files [C#]
ms.assetid: d62e22c5-a13c-48db-af9b-f10c801b0cb1
ms.openlocfilehash: b54d072ce9837f9b15694f2d7100817de62e9762
ms.sourcegitcommit: a241301495a84cc8c64fe972330d16edd619868b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2020
ms.locfileid: "84241774"
---
# <a name="how-to-read-a-text-file-one-line-at-a-time-c-programming-guide"></a>テキスト ファイルを 1 行ずつ読み取る方法 (C# プログラミング ガイド)
次の例では、`StreamReader` クラスの `ReadLine` メソッドを使用して、テキスト ファイルの内容を一度に 1 行ずつ文字列に読み込みます。 各テキスト行は文字列 `line` に格納され、画面に表示されます。  
  
## <a name="example"></a>例  
  
```csharp
int counter = 0;  
string line;  
  
// Read the file and display it line by line.  
System.IO.StreamReader file =
    new System.IO.StreamReader(@"c:\test.txt");  
while((line = file.ReadLine()) != null)  
{  
    System.Console.WriteLine(line);  
    counter++;  
}  
  
file.Close();  
System.Console.WriteLine("There were {0} lines.", counter);  
// Suspend the screen.  
System.Console.ReadLine();  
```  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 コードをコピーし、コンソール アプリケーションの `Main` メソッドに貼り付けます。  
  
 `"c:\test.txt"` を実際のファイル名に置き換えます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 次の条件を満たす場合は、例外が発生する可能性があります。  
  
- ファイルが存在しない。  
  
## <a name="net-security"></a>.NET セキュリティ  
 ファイル名からファイルの内容を判断しないでください。 たとえば、`myFile.cs` ファイルが C# ソース ファイルとは限りません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.IO?displayProperty=nameWithType>
- [C# プログラミング ガイド](../index.md)
- [ファイル システムとレジストリ (C# プログラミング ガイド)](./index.md)
