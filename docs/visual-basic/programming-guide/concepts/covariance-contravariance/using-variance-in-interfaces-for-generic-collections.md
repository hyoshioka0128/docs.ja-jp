---
title: ジェネリック コレクションに対するインターフェイスでの分散の使用
ms.date: 07/20/2015
ms.assetid: c867fcea-7462-4995-b9c5-542feec74036
ms.openlocfilehash: b762ce42215f9b24371313446637e95962677bfb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84375642"
---
# <a name="using-variance-in-interfaces-for-generic-collections-visual-basic"></a>ジェネリック コレクションに対するインターフェイスでの変性の使用 (Visual Basic)

共変のインターフェイスのメソッドでは、そのインターフェイスで指定された型よりも強い派生型を返すことができます。 反変のインターフェイスのメソッドでは、そのインターフェイスで指定された型よりも弱い派生型のパラメーターを受け取ることができます。

.NET Framework 4 では、既存のいくつかのインターフェイスが共変および反変になります。 その中には、<xref:System.Collections.Generic.IEnumerable%601> や <xref:System.IComparable%601> があります。 これにより、派生型のコレクションに対して、基本型のジェネリック コレクションを操作するメソッドを再利用できます。

.NET Framework のバリアント インターフェイスの一覧については、「[ジェネリック インターフェイスの変性 (Visual Basic)](variance-in-generic-interfaces.md)」を参照してください。

## <a name="converting-generic-collections"></a>ジェネリック コレクションの変換

次の例は、<xref:System.Collections.Generic.IEnumerable%601> インターフェイスにおける共変性のサポートの利点を示しています。 `PrintFullName` メソッドは、パラメーターとして `IEnumerable(Of Person)` 型のコレクションを受け取ります。 ただし、`Employee` は `Person` を継承しているため、`IEnumerable(Of Person)` 型のコレクションで再利用できます。

```vb
' Simple hierarchy of classes.
Public Class Person
    Public Property FirstName As String
    Public Property LastName As String
End Class

Public Class Employee
    Inherits Person
End Class

' The method has a parameter of the IEnumerable(Of Person) type.
Public Sub PrintFullName(ByVal persons As IEnumerable(Of Person))
    For Each person As Person In persons
        Console.WriteLine(
            "Name: " & person.FirstName & " " & person.LastName)
    Next
End Sub

Sub Main()
    Dim employees As IEnumerable(Of Employee) = New List(Of Employee)

    ' You can pass IEnumerable(Of Employee),
    ' although the method expects IEnumerable(Of Person).

    PrintFullName(employees)

End Sub
```

## <a name="comparing-generic-collections"></a>ジェネリック コレクションの比較

次の例は、<xref:System.Collections.Generic.IComparer%601> インターフェイスにおける反変性のサポートの利点を示しています。 `PersonComparer` クラスは、`IComparer(Of Person)` インターフェイスを実装します。 ただし、`Employee` は `Person` を継承しているため、`Employee` 型の一連のオブジェクトを比較するためにこのクラスを再利用できます。

```vb
' Simple hierarchy of classes.
Public Class Person
    Public Property FirstName As String
    Public Property LastName As String
End Class

Public Class Employee
    Inherits Person
End Class
' The custom comparer for the Person type
' with standard implementations of Equals()
' and GetHashCode() methods.
Class PersonComparer
    Implements IEqualityComparer(Of Person)

    Public Function Equals1(
        ByVal x As Person,
        ByVal y As Person) As Boolean _
        Implements IEqualityComparer(Of Person).Equals

        If x Is y Then Return True
        If x Is Nothing OrElse y Is Nothing Then Return False
        Return (x.FirstName = y.FirstName) AndAlso
            (x.LastName = y.LastName)
    End Function
    Public Function GetHashCode1(
        ByVal person As Person) As Integer _
        Implements IEqualityComparer(Of Person).GetHashCode

        If person Is Nothing Then Return 0
        Dim hashFirstName =
            If(person.FirstName Is Nothing,
            0, person.FirstName.GetHashCode())
        Dim hashLastName = person.LastName.GetHashCode()
        Return hashFirstName Xor hashLastName
    End Function
End Class

Sub Main()
    Dim employees = New List(Of Employee) From {
        New Employee With {.FirstName = "Michael", .LastName = "Alexander"},
        New Employee With {.FirstName = "Jeff", .LastName = "Price"}
    }

    ' You can pass PersonComparer,
    ' which implements IEqualityComparer(Of Person),
    ' although the method expects IEqualityComparer(Of Employee)

    Dim noduplicates As IEnumerable(Of Employee) = employees.Distinct(New PersonComparer())

    For Each employee In noduplicates
        Console.WriteLine(employee.FirstName & " " & employee.LastName)
    Next
End Sub
```

## <a name="see-also"></a>参照

- [ジェネリック インターフェイスの分散 (Visual Basic)](variance-in-generic-interfaces.md)
