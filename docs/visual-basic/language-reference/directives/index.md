---
title: ディレクティブ
ms.date: 07/20/2015
helpviewer_keywords:
- directives, Visual Basic compiler
- Visual Basic code, directives
- directives
ms.assetid: 20d5fe65-490a-4c23-88c2-ee4f490ed762
ms.openlocfilehash: b5fcf3cb8801bc99dd2096c28cc41ebefeb34592
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "85503815"
---
# <a name="directives-visual-basic"></a>ディレクティブ (Visual Basic)

このセクションのトピックでは、Visual Basic ソース コードのコンパイラ ディレクティブについて説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  

 [#Const ディレクティブ](const-directive.md) -- コンパイラ定数を定義します  
  
 [#ExternalSource ディレクティブ](externalsource-directive.md) -- ソース行とソース外部のテキストのマッピングを指定します  
  
 [#If...Then...#Else ディレクティブ](if-then-else-directives.md) -- 選択したコード ブロックをコンパイルします  
  
 [#Region ディレクティブ](region-directive.md) -- Visual Studio エディターでコードのセクションを折りたたんで非表示にします  
  
 **#Disable、#Enable** -- コードの領域に対して特定の警告を無効および有効にします。  
  
```vb  
#Disable Warning BC42356 ' suppress warning about no awaits in this method  
    Async Function TestAsync() As Task  
        Console.WriteLine("testing")  
    End Function  
#Enable Warning BC42356  
```  
  
 警告コードのコンマ区切りリストを無効および有効にすることもできます。  
  
## <a name="related-sections"></a>関連項目  

 [Visual Basic の言語リファレンス](../index.md)  
  