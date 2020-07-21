---
title: '方法: リフレクションを使用してアセンブリのメタデータをクエリする (LINQ)'
ms.date: 07/20/2015
ms.assetid: 53caa336-ab83-4181-b0f6-5c87c5f9e4ee
ms.openlocfilehash: a4f73bd2c8c01cbf92fac67991f01a1cb3dee932
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396455"
---
# <a name="how-to-query-an-assemblys-metadata-with-reflection-linq-visual-basic"></a>方法: リフレクションを使用してアセンブリのメタデータにクエリを実行する (LINQ) (Visual Basic)
次の例では、LINQ でリフレクションを使用して、指定した検索条件に一致するメソッドについてのメタデータを取得する方法を示します。 この例のクエリでは、配列などの列挙可能な型を返すすべてのメソッドの名前をアセンブリ内で検索します。  
  
## <a name="example"></a>例  
  
```vb
Imports System.Linq
Imports System.Reflection  

Module Module1  
    Sub Main()  
        Dim asmbly As Assembly =
            Assembly.Load("System.Core, Version=3.5.0.0, Culture=neutral, PublicKeyToken= b77a5c561934e089")  
  
        Dim pubTypesQuery = From type In asmbly.GetTypes()
                            Where type.IsPublic
                            From method In type.GetMethods()
                            Where method.ReturnType.IsArray = True
                            Let name = method.ToString()
                            Let typeName = type.ToString()
                            Group name By typeName Into methodNames = Group  
  
        Console.WriteLine("Getting ready to iterate")  
        For Each item In pubTypesQuery  
            Console.WriteLine(item.methodNames)  
  
            For Each type In item.methodNames  
                Console.WriteLine(" " & type)  
            Next  
        Next  
        Console.WriteLine("Press any key to exit... ")  
        Console.ReadKey()  
    End Sub  
End Module  
```  
  
この例では、<xref:System.Reflection.Assembly.GetTypes%2A?displayProperty=nameWithType> メソッドを使用して、指定したアセンブリ内の型の配列を返します。 パブリック型のみが返されるように、[Where 句](../../../language-reference/queries/where-clause.md)フィルターが適用されています。 パブリック型ごとに、<xref:System.Type.GetMethods%2A?displayProperty=nameWithType> 呼び出しから返される <xref:System.Reflection.MethodInfo> 配列を使用してサブクエリが生成されます。 これらの結果はフィルター処理され、戻り値の型が配列か、<xref:System.Collections.Generic.IEnumerable%601> を実装する型であるメソッドのみが返されます。 最後に、型名をキーとして使用して、これらの結果がグループ化されます。  
  
## <a name="see-also"></a>関連項目

- [LINQ to Objects (Visual Basic)](linq-to-objects.md)
