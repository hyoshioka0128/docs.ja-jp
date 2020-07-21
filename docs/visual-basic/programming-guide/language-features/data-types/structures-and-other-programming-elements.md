---
title: 構造体とその他のプログラミング要素
ms.date: 07/20/2015
helpviewer_keywords:
- structures [Visual Basic], arrays
- procedures [Visual Basic], structures as arguments to
- objects [Visual Basic], structure elements
- arrays [Visual Basic], structure elements
- nested structures [Visual Basic]
ms.assetid: 0f849313-ccd2-4c9a-acb9-69de6751c088
ms.openlocfilehash: dbd24065a954e5611663963371d5a9f4bbbaea68
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84393495"
---
# <a name="structures-and-other-programming-elements-visual-basic"></a>構造体およびその他のプログラミング要素 (Visual Basic)
構造体は、配列、オブジェクト、およびプロシージャと組み合わせて使用したり、相互に使用し合ったりすることができます。 この相互作用には、これらの要素で個別に使用されるものと同じ構文が使用されます。  
  
> [!NOTE]
> 構造体宣言で構造体の要素を初期化することはできません。 構造型であると宣言されている変数の要素にのみ、値を割り当てることができます。  
  
## <a name="structures-and-arrays"></a>構造体と配列  
 構造体には、配列を 1 つ以上の要素として含めることができます。 次の例を使って説明します。  
  
```vb  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public diskDrives() As String  
    Public purchaseDate As Date  
End Structure
```  
  
 構造体内の配列の値には、オブジェクトのプロパティにアクセスする場合と同じ方法でアクセスします。 次の例を使って説明します。  
  
```vb  
Dim mySystem As systemInfo  
ReDim mySystem.diskDrives(3)  
mySystem.diskDrives(0) = "1.44 MB"  
```  
  
 構造体の配列を宣言することもできます。 次の例を使って説明します。  
  
```vb  
Dim allSystems(100) As systemInfo  
```  
  
 同じ規則に従って、このデータ アーキテクチャのコンポーネントにアクセスします。 次の例を使って説明します。  
  
```vb  
ReDim allSystems(5).diskDrives(3)  
allSystems(5).CPU = "386SX"  
allSystems(5).diskDrives(2) = "100M SCSI"  
```  
  
## <a name="structures-and-objects"></a>構造体とオブジェクト  
 構造体には、オブジェクトを 1 つ以上の要素として含めることができます。 次の例を使って説明します。  
  
```vb  
Protected Structure userInput  
    Public userName As String  
    Public inputForm As System.Windows.Forms.Form  
    Public userFileNumber As Integer  
End Structure  
```  
  
 このような宣言では、`Object` ではなく特定のオブジェクト クラスを使用する必要があります。  
  
## <a name="structures-and-procedures"></a>構造体とプロシージャ  
 プロシージャ引数として構造体を渡すことができます。 次の例を使って説明します。  
  
```vb  
Public currentCPUName As String = "700MHz Pentium compatible"  
Public currentMemorySize As Long = 256  
Public Sub fillSystem(ByRef someSystem As systemInfo)  
    someSystem.cPU = currentCPUName  
    someSystem.memory = currentMemorySize  
    someSystem.purchaseDate = Now  
End Sub  
```  
  
 前の例では、"*参照渡し*" で構造体を渡しています。こうすることで、呼び出し元のコードで変更が有効になるように、プロシージャでその要素を変更できます。 このような変更から構造体を保護する場合は、値で渡します。  
  
 `Function` プロシージャから構造体を返すこともできます。 次の例を使って説明します。  
  
```vb  
Dim allSystems(100) As systemInfo  
Function findByDate(ByVal searchDate As Date) As systemInfo  
    Dim i As Integer  
    For i = 1 To 100  
        If allSystems(i).purchaseDate = searchDate Then Return allSystems(i)  
    Next i  
   ' Process error: system with desired purchase date not found.  
End Function  
```  
  
## <a name="structures-within-structures"></a>構造体内の構造体  
 構造体には他の構造体を含めることができます。 次の例を使って説明します。  
  
```vb  
Public Structure driveInfo  
    Public type As String  
    Public size As Long  
End Structure  
Public Structure systemInfo  
    Public cPU As String  
    Public memory As Long  
    Public diskDrives() As driveInfo  
    Public purchaseDate As Date  
End Structure  
```  
  
```vb  
Dim allSystems(100) As systemInfo  
ReDim allSystems(1).diskDrives(3)  
allSystems(1).diskDrives(0).type = "Floppy"  
```  
  
 この手法を使用して、あるモジュールで定義された構造体を別のモジュールで定義された構造体内にカプセル化することもできます。  
  
 構造体には、任意の深さで他の構造体を含めることができます。  
  
## <a name="see-also"></a>関連項目

- [データの種類](index.md)
- [基本データ型](elementary-data-types.md)
- [複合データ型](composite-data-types.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [構造体](structures.md)
- [トラブルシューティング (データ型)](troubleshooting-data-types.md)
- [方法: 構造体を宣言する](how-to-declare-a-structure.md)
- [構造体変数](structure-variables.md)
- [構造体とクラス](structures-and-classes.md)
- [Structure ステートメント](../../../language-reference/statements/structure-statement.md)
