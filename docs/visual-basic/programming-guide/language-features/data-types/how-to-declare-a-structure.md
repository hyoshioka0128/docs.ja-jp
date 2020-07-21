---
title: '方法: 構造体を宣言する'
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [Visual Basic], structures
- structure statements [Visual Basic]
- statements [Visual Basic], structure
- structures [Visual Basic], declaring
ms.assetid: d5e98381-eb81-47d4-af83-48cc534a2572
ms.openlocfilehash: a6b70d0973e92db90e35e61b7fed2279c5b0bac3
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393975"
---
# <a name="how-to-declare-a-structure-visual-basic"></a>方法: 構造体を宣言する (Visual Basic)
構造体宣言は、[Structure ステートメント](../../../language-reference/statements/structure-statement.md)で始まり、`End Structure` ステートメントで終了します。 これら 2 つのステートメントの間には、少なくとも 1 つの "*要素*" を宣言する必要があります。 要素は任意のデータ型にすることができますが、少なくとも 1 つは非共有変数または非共有非カスタム イベントのいずれかである必要があります。  
  
 構造体宣言で構造体の要素を初期化することはできません。 変数を構造体型として宣言するときは、変数を使用して値にアクセスすることによって、要素に値を代入します。  
  
 構造体とクラスの違いについては、「[構造体とクラス](structures-and-classes.md)」を参照してください。  
  
 デモンストレーションとして、従業員の名前、内線電話番号、給与を追跡するケースについて考えてみましょう。 構造体を使用すると、1 つの変数でこれを行うことができます。  
  
### <a name="to-declare-a-structure"></a>構造体を宣言するには  
  
1. 構造体の開始と終了のステートメントを作成します。  
  
     構造体のアクセス レベルを、[Public](../../../language-reference/modifiers/public.md)、[Protected](../../../language-reference/modifiers/protected.md)、[Friend](../../../language-reference/modifiers/friend.md)、または [Private](../../../language-reference/modifiers/private.md) キーワードを使用して指定できます。あるいは、既定で `Public` にすることもできます。  
  
    ```vb  
    Private Structure employee  
    End Structure  
    ```  
  
2. 構造体の本体に要素を追加します。  
  
     構造体には要素が少なくとも 1 つ必要です。 すべての要素を宣言し、そのアクセス レベルを指定する必要があります。 キーワードを指定せずに [Dim ステートメント](../../../language-reference/statements/dim-statement.md)を使用すると、アクセシビリティは既定の `Public` になります。  
  
    ```vb  
    Private Structure employee  
        Public givenName As String  
        Public familyName As String  
        Public phoneExtension As Long  
        Private salary As Decimal  
        Public Sub giveRaise(raise As Double)  
            salary *= raise  
        End Sub  
        Public Event salaryReviewTime()  
    End Structure  
    ```  
  
     前の例の `salary` フィールドは `Private` です。つまり、構造体の外部からはアクセスできないことを意味します。それが含まれているクラスからでもできません。 ただし、`giveRaise` プロシージャは `Public` であるため、構造体の外部から呼び出すことができます。 同様に、構造体の外部から `salaryReviewTime` イベントを発生させることもできます。  
  
     変数、`Sub` プロシージャ、およびイベントに加えて、構造体に定数、`Function` プロシージャ、およびプロパティを定義することもできます。 最大 1 つのプロパティを "*既定プロパティ*" として指定できます (そのプロパティが少なくとも 1 つの引数を取る場合)。 [共有](../../../language-reference/modifiers/shared.md) `Sub` プロシージャを使用してイベントを処理できます。 詳細については、「[方法:既定のプロパティを宣言して呼び出す (Visual Basic)](../procedures/how-to-declare-and-call-a-default-property.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [データの種類](index.md)
- [基本データ型](elementary-data-types.md)
- [複合データ型](composite-data-types.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [構造体](structures.md)
- [トラブルシューティング (データ型)](troubleshooting-data-types.md)
- [構造体変数](structure-variables.md)
- [構造体とその他のプログラミング要素](structures-and-other-programming-elements.md)
- [構造体とクラス](structures-and-classes.md)
- [ユーザー定義型](../../../language-reference/data-types/user-defined-data-type.md)
