---
title: 式は、含んでいるプロパティ '<propertyname>' を再帰的に呼び出します。
ms.date: 07/20/2015
f1_keywords:
- vbc42026
- BC42026
helpviewer_keywords:
- BC42026
ms.assetid: 4fde9db6-3bf3-48dc-8e05-981bf08969da
ms.openlocfilehash: e3a9f4cf2f4105d2c449813bf0c593860df7d1f0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409531"
---
# <a name="expression-recursively-calls-the-containing-property-propertyname"></a>式は、含んでいるプロパティ '\<propertyname>' を再帰的に呼び出します。
プロパティ定義の `Set` プロシージャ内のステートメントは、プロパティの名前に値を格納します。  
  
 プロパティの値を保持するために推奨される方法は、プロパティのコンテナーで `Private` 変数を定義し、それを `Get` と `Set` の両方のプロシージャで使用することです。 `Set` プロシージャは、この `Private` 変数に受け取った値を格納する必要があります。  
  
 `Get` プロシージャは `Function` プロシージャと同じように動作するため、プロパティ名に値を代入し、`End Get` ステートメントに遭遇することで制御を返すことができます。 ただし、推奨される方法は、[Return ステートメント](../statements/return-statement.md)に値として `Private` 変数を含めることです。  
  
 `Set` プロシージャは、値を返さない `Sub` プロシージャと同じように動作します。 そのため、プロシージャまたはプロパティの名前は `Set` プロシージャ内で特別な意味を持たず、値を格納することはできません。  
  
 次の例では、このエラーの原因となる可能性がある方法と、その後に推奨される方法を示します。  
  
```vb  
Public Class illustrateProperties  
' The code in the following property causes this error.  
    Public Property badProp() As Char  
        Get  
            Dim charValue As Char  
            ' Insert code to update charValue.  
            badProp = charValue  
        End Get  
        Set(ByVal Value As Char)  
            ' The following statement causes this error.  
            badProp = Value  
            ' The value stored in the local variable badProp  
            ' is not used by the Get procedure in this property.  
        End Set  
    End Property  
' The following code uses the recommended approach.  
    Private propValue As Char  
    Public Property goodProp() As Char  
        Get  
            ' Insert code to update propValue.  
            Return propValue  
        End Get  
        Set(ByVal Value As Char)  
            propValue = Value  
        End Set  
    End Property  
End Class  
```  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」を参照してください。  
  
 **エラー ID:** BC42026  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 前の例に示されているように、推奨される方法を使用するようにプロパティ定義を書き直してください。  
  
## <a name="see-also"></a>関連項目

- [Property プロシージャ](../../programming-guide/language-features/procedures/property-procedures.md)
- [Property ステートメント](../statements/property-statement.md)
- [Set ステートメント](../statements/set-statement.md)
