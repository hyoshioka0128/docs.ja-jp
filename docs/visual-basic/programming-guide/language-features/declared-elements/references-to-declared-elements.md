---
title: 宣言された要素の参照
ms.date: 07/20/2015
helpviewer_keywords:
- declared elements [Visual Basic]
- references [Visual Basic], declared elements
- qualified names [Visual Basic]
ms.assetid: d6301709-f4cc-4b7a-b8ba-80898f14ab46
ms.openlocfilehash: 23bff2eb098982f67ecb1b709e59096d5259a644
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405184"
---
# <a name="references-to-declared-elements-visual-basic"></a>宣言された要素の参照 (Visual Basic)
コードが宣言された要素を参照すると、Visual Basic コンパイラは、参照内の名前と、その名前の適切な宣言を照合します。 同じ名前の複数の要素が宣言されている場合は、その名前を*修飾*することで、それらの要素のうちどれが参照されるかを制御できます。  
  
 コンパイラは、名前宣言への名前参照を*最も狭いスコープ*と照合しようとします。 これは、参照を行うコードから始まり、コンテナー要素のレベルの外側に向かって機能することを意味します。  
  
 次の例では、同じ名前を持つ 2 つの変数への参照を示します。 この例では、それぞれが `totalCount` という名前の 2 つの変数を、モジュール `container` の異なるレベルのスコープで宣言しています。 プロシージャ `showCount` により `totalCount` が修飾なしで表示される場合、Visual Basic コンパイラは、参照を最も狭いスコープ (つまり、`showCount` 内のローカル宣言) に解決します。 含まれているモジュール `container` で `totalCount` を修飾すると、コンパイラは、参照をより広いスコープの宣言に解決します。  
  
```vb  
' Assume these two modules are both in the same assembly.  
Module container  
    Public totalCount As Integer = 1  
    Public Sub showCount()  
        Dim totalCount As Integer = 6000  
        ' The following statement displays the local totalCount (6000).  
        MsgBox("Unqualified totalCount is " & CStr(totalCount))  
        ' The following statement displays the module's totalCount (1).  
        MsgBox("container.totalCount is " & CStr(container.totalCount))  
    End Sub  
End Module  
Module callingModule  
    Public Sub displayCount()  
        container.showCount()  
        ' The following statement displays the containing module's totalCount (1).  
        MsgBox("container.totalCount is " & CStr(container.totalCount))  
    End Sub  
End Module  
```  
  
## <a name="qualifying-an-element-name"></a>要素名の修飾  
 この検索プロセスをオーバーライドし、より広いスコープで宣言された名前を指定する場合は、より広いスコープのコンテナー要素で名前を*修飾*する必要があります。 場合によっては、コンテナー要素を修飾する必要がある場合もあります。  
  
 名前の修飾は、ターゲット要素が定義されている場所を識別する情報を、ソース ステートメント内で先に記述することを意味します。 この情報は、*修飾文字列*と呼ばれます。 1 つ以上の名前空間と、1 つのモジュール、クラス、または構造体を含めることができます。  
  
 修飾文字列では、ターゲット要素を含むモジュール、クラス、または構造体を明確に指定する必要があります。 コンテナーは、別のコンテナー要素 (通常は名前空間) に配置される場合があります。 修飾文字列に複数のコンテナー要素を含めることが必要になる場合があります。  
  
#### <a name="to-access-a-declared-element-by-qualifying-its-name"></a>名前を修飾することで宣言された要素にアクセスするには  
  
1. 要素が定義されている場所を確認します。 これには、名前空間、または名前空間の階層が含まれる場合があります。 最下位レベルの名前空間内では、要素はモジュール、クラス、または構造体に含まれている必要があります。  
  
    ```vb  
    ' Assume the following hierarchy exists outside your code.  
    Namespace outerSpace  
        Namespace innerSpace  
            Module holdsTotals  
                Public Structure totals  
                    Public thisTotal As Integer  
                    Public Shared grandTotal As Long  
                End Structure  
            End Module  
        End Namespace  
    End Namespace  
    ```  
  
2. ターゲット要素の場所に基づいて、修飾パスを確認します。 最上位レベルの名前空間から開始し、最下位レベルの名前空間に進み、ターゲット要素が含まれているモジュール、クラス、または構造体で終了します。 パス内の各要素には、その後に続く要素が含まれている必要があります。  
  
     `outerSpace` → `innerSpace` → `holdsTotals` → `totals`  
  
3. ターゲット要素の修飾文字列を準備します。 パス内のすべての要素の後にピリオド (`.`) を配置します。 アプリケーションは、修飾文字列内のすべての要素にアクセスできる必要があります。  
  
    ```vb  
    outerSpace.innerSpace.holdsTotals.totals.  
    ```  
  
4. 通常の方法で、ターゲット要素を参照する式または代入ステートメントを記述します。  
  
    ```vb  
    grandTotal = 9000  
    ```  
  
5. ターゲット要素名の前に修飾文字列を指定します。 名前は、要素が含まれているモジュール、クラス、または構造体の後のピリオド (`.`) の直後に記述する必要があります。  
  
    ```vb  
    ' Assume the following module is part of your code.  
    Module accessGrandTotal  
        Public Sub setGrandTotal()  
            outerSpace.innerSpace.holdsTotals.totals.grandTotal = 9000  
        End Sub  
    End Module  
    ```  
  
6. コンパイラは、修飾文字列を使用して、ターゲット要素参照と照合できる、明確で、あいまいでない宣言を検索します。  
  
 また、アプリケーションが同じ名前を持つ複数のプログラミング要素にアクセスできる場合は、名前参照の修飾が必要な場合もあります。 たとえば、<xref:System.Windows.Forms> と <xref:System.Web.UI.WebControls> の名前空間のどちらにも、`Label` クラス (<xref:System.Windows.Forms.Label?displayProperty=nameWithType> および <xref:System.Web.UI.WebControls.Label?displayProperty=nameWithType>) が含まれています。 アプリケーションで両方を使用する場合、または独自の `Label` クラスを定義する場合は、異なる `Label` オブジェクトを区別する必要があります。 変数宣言に、名前空間またはインポートの別名を含めます。 次の例では、インポートの別名を使用します。  
  
```vb  
' The following statement must precede all your declarations.  
Imports win = System.Windows.Forms, web = System.Web.UI.WebControls  
' The following statement references the Windows.Forms.Label class.  
Dim winLabel As New win.Label()  
```  
  
## <a name="members-of-other-containing-elements"></a>他のコンテナー要素のメンバー  
 別のクラスまたは構造体の非共有メンバーを使用する場合は、まず、クラスまたは構造体のインスタンスを指す変数または式を使用して、メンバー名を修飾する必要があります。 次の例では、`demoClass` は `class1` という名前のクラスのインスタンスです。  
  
```vb  
Dim demoClass As class1 = New class1()  
demoClass.someSub[(argumentlist)]  
```  
  
 [Shared](../../../language-reference/modifiers/shared.md) ではないメンバーを修飾するために、クラス名自体を使用することはできません。 まず、オブジェクト変数にインスタンスを作成してから (この場合は `demoClass`)、変数名によって参照する必要があります。  
  
 クラスまたは構造体に `Shared` メンバーが含まれている場合は、クラスまたは構造体の名前を使用して、またはインスタンスを指す変数または式を使用して、そのメンバーを修飾できます。  
  
 モジュールには個別のインスタンスはなく、そのすべてのメンバーは既定で `Shared` です。 そのため、モジュール名を持つモジュール メンバーを修飾します。  
  
 次の例では、モジュール メンバー プロシージャへの修飾参照を示します。 この例では、プロジェクト内の異なるモジュールに、両方とも `perform` という名前の 2 つの `Sub` プロシージャを宣言しています。 それぞれをその独自のモジュール内に修飾なしで指定できますが、他の場所から参照されている場合は修飾する必要があります。 `module3` の最後の参照は `perform` を修飾しないため、コンパイラはその参照を解決できません。  
  
```vb  
' Assume these three modules are all in the same assembly.  
Module module1  
    Public Sub perform()  
        MsgBox("module1.perform() now returning")  
    End Sub  
End Module  
Module module2  
    Public Sub perform()  
        MsgBox("module2.perform() now returning")  
    End Sub  
    Public Sub doSomething()  
        ' The following statement calls perform in module2, the active module.  
        perform()  
        ' The following statement calls perform in module1.  
        module1.perform()  
    End Sub  
End Module  
Module module3  
    Public Sub callPerform()  
        ' The following statement calls perform in module1.  
        module1.perform()  
        ' The following statement makes an unresolvable name reference  
        ' and therefore generates a COMPILER ERROR.  
        perform() ' INVALID statement  
    End Sub  
End Module  
```  
  
## <a name="references-to-projects"></a>プロジェクトへの参照  
 別のプロジェクトで定義されている [Public](../../../language-reference/modifiers/public.md) 要素を使用するには、まず、そのプロジェクトのアセンブリまたは型ライブラリへの*参照*を設定する必要があります。 参照を設定するには、 **[プロジェクト]** メニューで **[参照の追加]** をクリックするか、[-reference (Visual Basic)](../../../reference/command-line-compiler/reference.md) コマンドライン コンパイラ オプションを使用します。  
  
 たとえば、.NET Framework の XML オブジェクト モデルを使用できます。 <xref:System.Xml> 名前空間への参照を設定する場合は、<xref:System.Xml.XmlDocument> など、そのクラスのいずれかを宣言して使用できます。 <xref:System.Xml.XmlDocument> の使用例を次に示します。  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As System.Xml.XmlDocument  
```  
  
## <a name="importing-containing-elements"></a>コンテナー要素のインポート  
 [Imports ステートメント (.NET 名前空間と型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md) を使用すると、使用するモジュールまたはクラスを含む名前空間を*インポート*できます。 これにより、インポートされた名前空間で定義されている要素を、その名前を完全修飾せずに参照できます。 次の例では、前の例を記述し直して、<xref:System.Xml> 名前空間をインポートします。  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement must precede all your declarations.  
Imports System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As XmlDocument  
```  
  
 さらに、`Imports` ステートメントでは、インポートされた名前空間ごとに*インポートの別名*を定義できます。 これにより、ソース コードを短くして、読みやすくすることができます。 次の例では、前の例を記述し直して、`xD` 名前空間の別名として <xref:System.Xml> を使用します。  
  
```vb  
' Assume this project has a reference to System.Xml  
' The following statement must precede all your declarations.  
Imports xD = System.Xml  
' The following statement creates xDoc as an XML document object.  
Dim xDoc As xD.XmlDocument  
```  
  
 `Imports` ステートメントによって、他のプロジェクトの要素をアプリケーションで使用できなくなります。 つまり、参照の設定の代わりになりません。 名前空間をインポートすると、その名前空間で定義されている名前を修飾する必要がなくなります。  
  
 また、`Imports` ステートメントを使用して、モジュール、クラス、構造体、および列挙型をインポートすることもできます。 その後、このようなインポートされた要素のメンバーを修飾なしで使用できます。 ただし、クラスや構造体の非共有メンバーは、常に、クラスまたは構造体のインスタンスに評価される変数または式を使用して修飾する必要があります。  
  
## <a name="naming-guidelines"></a>名前付けのガイドライン  
 同じ名前を持つ複数のプログラミング要素を定義すると、コンパイラがその名前への参照を解決しようとしたときに、*名前のあいまいさ*が発生する可能性があります。 スコープ内に複数の定義が含まれている場合、またはスコープ内に定義が存在しない場合、参照は解決不可能です。 例については、このヘルプ ページの「修飾参照の例」を参照してください。  
  
 すべての要素に一意の名前を付けることで、名前のあいまいさを回避できます。 その後、名前を名前空間、モジュール、またはクラスで修飾しなくても、任意の要素を参照できるようになります。 また、間違った要素が誤って参照される可能性を低くすることもできます。  
  
## <a name="shadowing"></a>シャドウ  
 2 つのプログラミング要素が同じ名前を共有している場合、それらのうちの 1 つで他方を非表示にしたり、*シャドウ*したりすることができます。 シャドウされた要素を参照することはできません。代わりに、シャドウされた要素名を使用するコードでは、Visual Basic コンパイラによってシャドウ要素に解決されます。 例の詳細については、「[Visual Basic におけるシャドウ](shadowing.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [宣言された要素の名前](declared-element-names.md)
- [宣言された要素の特性](declared-element-characteristics.md)
- [プロジェクトおよびソリューションのプロパティの管理](/visualstudio/ide/managing-project-and-solution-properties)
- [変数](../variables/index.md)
- [Imports ステートメント (.NET 名前空間および型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)
- [New 演算子](../../../language-reference/operators/new-operator.md)
- [Public](../../../language-reference/modifiers/public.md)
