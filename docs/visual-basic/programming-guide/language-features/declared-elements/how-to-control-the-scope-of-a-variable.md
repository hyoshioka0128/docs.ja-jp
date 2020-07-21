---
title: '方法: 変数のスコープを制御する'
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], scope
- declared elements [Visual Basic], scope
- visibility [Visual Basic], declared elements
- variables [Visual Basic], visibility
- scope [Visual Basic], declared elements
- scope [Visual Basic], variables
- scope [Visual Basic], Visual Basic
- declared elements [Visual Basic], visibility
- visibility [Visual Basic], variables
ms.assetid: 44b7f62a-cb5c-4d50-bce9-60ae68f87072
ms.openlocfilehash: 8b21f22edea84448e3f2969c3e4b07c08a17a338
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84357349"
---
# <a name="how-to-control-the-scope-of-a-variable-visual-basic"></a>方法: 変数のスコープを制御する (Visual Basic)
通常、変数は、*スコープ*内にあります。つまり、それを宣言した領域全体で可視になり参照できます。 場合によって、変数の*アクセス レベル*がそのスコープに影響を与えることがあります。  
  
 詳細については、「 [Scope in Visual Basic](scope.md)」を参照してください。  
  
## <a name="scope-at-block-or-procedure-level"></a>ブロック レベルまたはプロシージャ レベルのスコープ  
  
#### <a name="to-make-a-variable-visible-only-within-a-block"></a>変数をブロック内でのみ可視にするには  
  
- 変数の [Dim ステートメント](../../../language-reference/statements/dim-statement.md)を、そのブロックの開始と終了の宣言ステートメントの間、たとえば `For` ループの `For` ステートメントと `Next` ステートメントの間などに配置します。  
  
     変数は、ブロック内からのみ参照できます。  
  
#### <a name="to-make-a-variable-visible-only-within-a-procedure"></a>変数をプロシージャ内でのみ可視にするには  
  
- 変数の `Dim` ステートメントをプロシージャ内、ただし、ブロック (`With`...`End With` ブロックなど) の外部に配置します。  
  
     プロシージャに含まれている任意のブロック内など、プロシージャ内からのみ変数を参照できます。  
  
## <a name="scope-at-module-or-namespace-level"></a>モジュールまたは名前空間レベルのスコープ  
 便宜上、*モジュール レベル*という 1 つの用語は、モジュール、クラス、および構造体に等しく適用されます。 モジュール レベル変数のアクセスレベルによってそのスコープが決まります。 モジュール、クラス、または構造体を含む名前空間もスコープに影響します。  
  
#### <a name="to-make-a-variable-visible-throughout-a-module-class-or-structure"></a>変数をモジュール、クラス、または構造体全体で可視にするには  
  
1. モジュール、クラス、または構造体の内部で、ただしプロシージャの外部に、変数の `Dim` ステートメントを配置します。  
  
2. `Dim` ステートメントに [Private](../../../language-reference/modifiers/private.md) キーワードを含めます。  
  
3. 変数は、モジュール、クラス、または構造体内のどこからでも参照できますが、その外部から参照することはできません。  
  
#### <a name="to-make-a-variable-visible-throughout-a-namespace"></a>変数を名前空間全体で可視にするには  
  
1. モジュール、クラス、または構造体の内部で、ただしプロシージャの外部に、変数の `Dim` ステートメントを配置します。  
  
2. `Dim` ステートメントに [Friend](../../../language-reference/modifiers/friend.md) または [Public](../../../language-reference/modifiers/public.md) キーワードを含めます。  
  
3. 変数は、モジュール、クラス、または構造体を含む名前空間内のどこからでも参照できます。  
  
## <a name="example"></a>例  
 次の例では、モジュール レベルで変数を宣言し、その可視性をモジュール内のコードに制限しています。  
  
```vb  
Module demonstrateScope  
    Private strMsg As String  
    Sub initializePrivateVariable()  
        strMsg = "This variable cannot be used outside this module."  
    End Sub  
    Sub usePrivateVariable()  
        MsgBox(strMsg)  
    End Sub  
End Module  
```  
  
 前の例では、モジュール `demonstrateScope` に定義されているすべてのプロシージャで、`String` 変数 `strMsg` を参照できます。 `strMsg` プロシージャを呼び出すと、文字列変数 `usePrivateVariable` の内容がダイアログ ボックスに表示されます。  
  
 前の例を次のように変更すると、文字列変数 `strMsg` は、その宣言の名前空間内のどこでもコードによって参照できます。  
  
```vb  
Public strMsg As String  
```  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 変数のスコープを狭めるほど、同じ名前を持つ別の変数の代わりに、誤ってそれを参照してしまう可能性が低くなります。 参照マッチングに関する問題を最小限に抑えることもできます。  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 変数のスコープを狭めるほど、悪意のあるコードによってそれが不正使用される可能性が低くなります。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic におけるスコープ](scope.md)
- [Visual Basic における有効期間](lifetime.md)
- [Visual Basic でのアクセス レベル](access-levels.md)
- [変数](../variables/index.md)
- [変数宣言](../variables/variable-declaration.md)
- [Dim ステートメント](../../../language-reference/statements/dim-statement.md)
