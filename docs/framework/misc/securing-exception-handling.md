---
title: 例外処理の保護
description: 「.NET コードで例外処理をセキュリティで保護する方法」を参照してください。 Try、except、catch、および finally ステートメントがある場合は、コードが実行される順序を確認します。
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- code security, exception handling
- security [.NET Framework], exception handling
- secure coding, exception handling
- exception handling, security
ms.assetid: 1f3da743-9742-47ff-96e6-d0dd1e9e1c19
ms.openlocfilehash: 73597f83d7236cd48a18a891c987b4f5d7e1723d
ms.sourcegitcommit: 0fa2b7b658bf137e813a7f4d09589d64c148ebf5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/14/2020
ms.locfileid: "86309041"
---
# <a name="securing-exception-handling"></a>例外処理の保護
Visual C++ と Visual Basic では、スタックの上位にあるフィルター式は、ステートメントの前に実行さ `finally` れます。 そのフィルターに関連付けられている**catch**ブロックは、ステートメントの後に実行され `finally` ます。 詳細については、「[ユーザーフィルター例外の使用](../../standard/exceptions/using-user-filtered-exception-handlers.md)」を参照してください。 このセクションでは、この順序のセキュリティへの影響について説明します。 フィルターステートメントとステートメントの実行順序を示す、次の擬似コード例を考えてみましょう `finally` 。  
  
```cpp  
void Main()
{  
    try
    {  
        Sub();  
    }
    except (Filter())
    {  
        Console.WriteLine("catch");  
    }  
}  
bool Filter () {  
    Console.WriteLine("filter");  
    return true;  
}  
void Sub()
{  
    try
    {  
        Console.WriteLine("throw");  
        throw new Exception();  
    }
    finally
    {  
        Console.WriteLine("finally");  
    }  
}
```  
  
 このコードは、次を出力します。  
  
```output
Throw  
Filter  
Finally  
Catch  
```  
  
 このフィルターは、ステートメントの前に実行されるので `finally` 、他のコードの実行によって発生する可能性がある状態変更を行うすべてのものによって、セキュリティの問題が発生する可能性があります。 次に例を示します。  
  
```cpp  
try
{  
    Alter_Security_State();  
    // This means changing anything (state variables,  
    // switching unmanaged context, impersonation, and
    // so on) that could be exploited if malicious
    // code ran before state is restored.  
    Do_some_work();  
}
finally
{  
    Restore_Security_State();  
    // This simply restores the state change above.  
}  
```  
  
 この擬似コードを使用すると、スタックの上位にあるフィルターで任意のコードを実行できます。 その他の操作の例としては、別の id の一時的な偽装、セキュリティチェックをバイパスする内部フラグの設定、またはスレッドに関連付けられているカルチャの変更などがあります。 推奨される解決方法は、コードの変更を呼び出し元のフィルターブロックからスレッド状態に分離する例外ハンドラーを導入することです。 ただし、例外ハンドラーを適切に導入することが重要です。この問題は修正されません。 次の例では、UI カルチャを切り替えますが、あらゆる種類のスレッド状態変更が同様に公開される可能性があります。  
  
```cpp  
YourObject.YourMethod()  
{  
   CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
   try {  
      Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
      // Do something that throws an exception.  
}  
   finally {  
      Thread.CurrentThread.CurrentUICulture = saveCulture;  
   }  
}  
```  
  
```vb  
Public Class UserCode  
   Public Shared Sub Main()  
      Try  
         Dim obj As YourObject = new YourObject  
         obj.YourMethod()  
      Catch e As Exception When FilterFunc  
         Console.WriteLine("An error occurred: '{0}'", e)  
         Console.WriteLine("Current Culture: {0}",
Thread.CurrentThread.CurrentUICulture)  
      End Try  
   End Sub  
  
   Public Function FilterFunc As Boolean  
      Console.WriteLine("Current Culture: {0}", Thread.CurrentThread.CurrentUICulture)  
      Return True  
   End Sub  
  
End Class  
```  
  
 この場合の適切な修正は、 **try** / **try**catch ブロックで既存の try**finally**ブロックをラップすることです / **catch** 。 次の例に示すように、 **catch throw**句を既存の**try**finally ブロックに導入するだけで / **finally**は問題は解決されません。  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
  
    try
    {  
        Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
        // Do something that throws an exception.  
    }  
    catch { throw; }  
    finally
    {  
        Thread.CurrentThread.CurrentUICulture = saveCulture;  
    }  
}  
```  
  
 この操作では `finally` 、が `FilterFunc` 制御を取得する前にステートメントが実行されていないため、問題は解決されません。  
  
 次の例では、 `finally` 呼び出し元の例外フィルターブロックを例外として使用する前に、句が実行されたことを確認して問題を修正します。  
  
```cpp  
YourObject.YourMethod()  
{  
    CultureInfo saveCulture = Thread.CurrentThread.CurrentUICulture;  
    try
    {  
        try
        {  
            Thread.CurrentThread.CurrentUICulture = new CultureInfo("de-DE");  
            // Do something that throws an exception.  
        }  
        finally
        {  
            Thread.CurrentThread.CurrentUICulture = saveCulture;  
        }  
    }  
    catch { throw; }  
}  
```  
  
## <a name="see-also"></a>関連項目

- [安全なコーディングのガイドライン](../../standard/security/secure-coding-guidelines.md)
