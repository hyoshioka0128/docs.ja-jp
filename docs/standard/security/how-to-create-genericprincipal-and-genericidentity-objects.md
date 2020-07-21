---
title: '方法: GenericPrincipal オブジェクトと GenericIdentity オブジェクトを作成する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Creating Generic Identity Objects
- GenericPrincipal Objects
- Creating GenericPrincipal Objects
- GenericIdentity Objects
ms.assetid: 465694cf-258b-4747-9dae-35b01a5bcdbb
ms.openlocfilehash: 10a71185db3359cda1c3bf7a12f5698929c98296
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290864"
---
# <a name="how-to-create-genericprincipal-and-genericidentity-objects"></a>方法: GenericPrincipal オブジェクトと GenericIdentity オブジェクトを作成する

クラスをクラスと共に使用して、 <xref:System.Security.Principal.GenericIdentity> <xref:System.Security.Principal.GenericPrincipal> Windows ドメインに依存しない認証スキームを作成することができます。

### <a name="to-create-a-genericprincipal-object"></a>GenericPrincipal オブジェクトを作成するには

1. ID クラスの新しいインスタンスを作成し、インスタンスに付ける名前で初期化します。 新しい **GenericIdentity** オブジェクトを作成し、名前 `MyUser` で初期化するコードを次に示します。

    ```vb
    Dim myIdentity As New GenericIdentity("MyUser")
    ```

    ```csharp
    GenericIdentity myIdentity = new GenericIdentity("MyUser");
    ```

2. **GenericPrincipal** クラスの新しいインスタンスを作成し、前に作成した **GenericIdentity** オブジェクトと、プリンシパルに関連付けるロールを表す文字列の配列で、このインスタンスを初期化します。 管理者のロールとユーザーのロールを表す文字列の配列を指定するコード例を次に示します。 **GenericPrincipal** は、前の **GenericIdentity** と文字列配列で初期化されます。

    ```vb
    Dim myStringArray As String() = {"Manager", "Teller"}
    DIm myPrincipal As New GenericPrincipal(myIdentity, myStringArray)
    ```

    ```csharp
    String[] myStringArray = {"Manager", "Teller"};
    GenericPrincipal myPrincipal = new GenericPrincipal(myIdentity, myStringArray);
    ```

3. 次のコードを使用して、プリンシパルを現在のスレッドに結合します。 これは、プリンシパルを複数回検証する必要がある場合、アプリケーションで実行されている他のコードによって検証する必要がある場合、またはオブジェクトによって検証する必要がある場合に役立ち <xref:System.Security.Permissions.PrincipalPermission> ます。 このような場合でも、プリンシパル オブジェクトをスレッドに結合せずにロール ベースの検証を行うことができます。 詳細については、「[プリンシパル オブジェクトの置き換え](replacing-a-principal-object.md)」を参照してください。

    ```vb
    Thread.CurrentPrincipal = myPrincipal
    ```

    ```csharp
    Thread.CurrentPrincipal = myPrincipal;
    ```

## <a name="example"></a>例

次のコード例では、**GenericPrincipal** と **GenericIdentity** のインスタンスを作成する方法を示します。 このコードは、各オブジェクトの値をコンソールに表示します。

```vb
Imports System.Security.Principal
Imports System.Threading

Public Class Class1

    Public Shared Sub Main()
        ' Create generic identity.
        Dim myIdentity As New GenericIdentity("MyIdentity")

        ' Create generic principal.
        Dim myStringArray As String() =  {"Manager", "Teller"}
        Dim myPrincipal As New GenericPrincipal(myIdentity, myStringArray)

        ' Attach the principal to the current thread.
        ' This is not required unless repeated validation must occur,
        ' other code in your application must validate, or the
        ' PrincipalPermission object is used.
        Thread.CurrentPrincipal = myPrincipal

        ' Print values to the console.
        Dim name As String = myPrincipal.Identity.Name
        Dim auth As Boolean = myPrincipal.Identity.IsAuthenticated
        Dim isInRole As Boolean = myPrincipal.IsInRole("Manager")

        Console.WriteLine("The name is: {0}", name)
        Console.WriteLine("The isAuthenticated is: {0}", auth)
        Console.WriteLine("Is this a Manager? {0}", isInRole)

    End Sub

End Class
```

```csharp
using System;
using System.Security.Principal;
using System.Threading;

public class Class1
{
    public static int Main(string[] args)
    {
    // Create generic identity.
    GenericIdentity myIdentity = new GenericIdentity("MyIdentity");

    // Create generic principal.
    String[] myStringArray = {"Manager", "Teller"};
    GenericPrincipal myPrincipal =
        new GenericPrincipal(myIdentity, myStringArray);

    // Attach the principal to the current thread.
    // This is not required unless repeated validation must occur,
    // other code in your application must validate, or the
    // PrincipalPermission object is used.
    Thread.CurrentPrincipal = myPrincipal;

    // Print values to the console.
    String name =  myPrincipal.Identity.Name;
    bool auth =  myPrincipal.Identity.IsAuthenticated;
    bool isInRole =  myPrincipal.IsInRole("Manager");

    Console.WriteLine("The name is: {0}", name);
    Console.WriteLine("The isAuthenticated is: {0}", auth);
    Console.WriteLine("Is this a Manager? {0}", isInRole);

    return 0;
    }
}
```

実行されると、アプリケーションの出力は次のようになります。

```console
The Name is: MyIdentity
The IsAuthenticated is: True
Is this a Manager? True
```

## <a name="see-also"></a>関連項目

- <xref:System.Security.Principal.GenericIdentity>
- <xref:System.Security.Principal.GenericPrincipal>
- <xref:System.Security.Permissions.PrincipalPermission>
- [プリンシパル オブジェクトの置き換え](replacing-a-principal-object.md)
- [プリンシパル オブジェクトと ID オブジェクト](principal-and-identity-objects.md)
