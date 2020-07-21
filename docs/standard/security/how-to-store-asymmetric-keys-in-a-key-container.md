---
title: '方法: キーコンテナーに非対称キーを格納する'
description: .NET のキーコンテナーに非対称キーを格納する方法について説明します。 非対称キーを作成し、キーコンテナーに保存し、キーを取得して削除する方法について説明します。
ms.date: 05/26/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptography [.NET Framework], asymmetric keys
- storing asymmetric keys
- keys, asymmetric
- encryption keys
- keys, storing in key containers
- asymmetric keys [.NET Framework]
- encryption [.NET Framework], asymmetric keys
- decryption keys
ms.assetid: 0dbcbd8d-0dcf-40e9-9f0c-e3f162d35ccc
ms.openlocfilehash: a0fbde37491043cc1aab71e9733087bf410b997d
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84769030"
---
# <a name="store-asymmetric-keys-in-a-key-container"></a>キーコンテナーに非対称キーを格納する

非対称秘密キーは、ローカル コンピューターにそのまま平文として保存しないでください。 秘密キーを保存する必要がある場合は、キーコンテナーを使用します。 キーコンテナーの詳細については、「[コンピューターレベルおよびユーザーレベルの RSA キーコンテナー](https://docs.microsoft.com/previous-versions/aspnet/f5cs0acs(v=vs.100))について」を参照してください。

## <a name="create-an-asymmetric-key-and-save-it-in-a-key-container"></a>非対称キーを作成してキーコンテナーに保存する

1. クラスの新しいインスタンスを作成 <xref:System.Security.Cryptography.CspParameters> し、キーコンテナーを呼び出す名前をフィールドに渡し <xref:System.Security.Cryptography.CspParameters.KeyContainerName?displayProperty=nameWithType> ます。

1. クラス (通常はまたは) から派生したクラスの新しいインスタンスを作成 <xref:System.Security.Cryptography.AsymmetricAlgorithm> <xref:System.Security.Cryptography.RSACryptoServiceProvider> し、 <xref:System.Security.Cryptography.DSACryptoServiceProvider> 以前に作成したオブジェクトを `CspParameters` そのコンストラクターに渡します。

> [!NOTE]
> 非対称キーの作成と取得は1つの操作です。 キーがコンテナーにまだ存在しない場合は、返される前に作成されます。
>
> - <xref:System.Security.Cryptography.RSA.ToXmlString%2A?displayProperty=nameWithType>
> - <xref:System.Security.Cryptography.DSA.ToXmlString%2A?displayProperty=nameWithType>

## <a name="delete-the-key-from-the-key-container"></a>キーコンテナーからキーを削除します。

1. クラスの新しいインスタンスを作成 `CspParameters` し、キーコンテナーを呼び出す名前をフィールドに渡し <xref:System.Security.Cryptography.CspParameters.KeyContainerName?displayProperty=nameWithType> ます。

1. クラス (通常はまたは) から派生したクラスの新しいインスタンスを作成 <xref:System.Security.Cryptography.AsymmetricAlgorithm> `RSACryptoServiceProvider` し、 `DSACryptoServiceProvider` 以前に作成したオブジェクトを `CspParameters` そのコンストラクターに渡します。

1. <xref:System.Security.Cryptography.RSACryptoServiceProvider.PersistKeyInCsp?displayProperty=nameWithType> <xref:System.Security.Cryptography.DSACryptoServiceProvider.PersistKeyInCsp?displayProperty=nameWithType> から派生するクラスのまたはのプロパティ `AsymmetricAlgorithm` を `false` (Visual Basic) に設定し `False` ます。

1. `Clear`から派生したクラスのメソッドを呼び出し `AsymmetricAlgorithm` ます。 このメソッドは、クラスのすべてのリソースを解放し、キー コンテナーを消去します。 

## <a name="example"></a>例

非対称キーを作成し、それをキー コンテナーへ格納し、後でキーを取得し、最後にキー コンテナーからキーを削除する方法の例を次に示します。

`GenKey_SaveInContainer` メソッドと `GetKeyFromContainer` メソッドのコードは類似していることに注意してください。 オブジェクトのキーコンテナー名を指定し、 <xref:System.Security.Cryptography.CspParameters> <xref:System.Security.Cryptography.AsymmetricAlgorithm> <xref:System.Security.Cryptography.RSACryptoServiceProvider.PersistKeyInCsp%2A> プロパティまたはプロパティがに設定されたオブジェクトに渡すと <xref:System.Security.Cryptography.DSACryptoServiceProvider.PersistKeyInCsp%2A> `true` 、の動作は次のようになります。

- 指定した名前のキー コンテナーが存在しない場合、コンテナーが作成されてキーが保持されます。
- 指定した名前のキー コンテナーが存在する場合、そのコンテナー内のキーが現在の <xref:System.Security.Cryptography.AsymmetricAlgorithm> オブジェクトに自動的に読み込まれます。

このため、メソッドのコードは `GenKey_SaveInContainer` 最初に実行されるので、キーを永続化します。一方、メソッドのコードは、 `GetKeyFromContainer` 2 番目に実行されるため、キーを読み込みます。

```vb
Imports System
Imports System.Security.Cryptography

Public Class StoreKey

    Public Shared Sub Main()
        Try
            ' Create a key and save it in a container.
            GenKey_SaveInContainer("MyKeyContainer")

            ' Retrieve the key from the container.
            GetKeyFromContainer("MyKeyContainer")

            ' Delete the key from the container.
            DeleteKeyFromContainer("MyKeyContainer")

            ' Create a key and save it in a container.
            GenKey_SaveInContainer("MyKeyContainer")

            ' Delete the key from the container.
            DeleteKeyFromContainer("MyKeyContainer")
        Catch e As CryptographicException
            Console.WriteLine(e.Message)
        End Try
    End Sub

    Private Shared Sub GenKey_SaveInContainer(ByVal ContainerName As String)
        ' Create the CspParameters object and set the key container
        ' name used to store the RSA key pair.
        Dim parameters As New CspParameters With {
            .KeyContainerName = ContainerName
        }

        ' Create a new instance of RSACryptoServiceProvider that accesses
        ' the key container MyKeyContainerName.
        Using rsa As New RSACryptoServiceProvider(parameters)
            ' Display the key information to the console.
            Console.WriteLine($"Key added to container:  {rsa.ToXmlString(True)}")
        End Using
    End Sub

    Private Shared Sub GetKeyFromContainer(ByVal ContainerName As String)
        ' Create the CspParameters object and set the key container
        '  name used to store the RSA key pair.
        Dim parameters As New CspParameters With {
            .KeyContainerName = ContainerName
        }

        ' Create a new instance of RSACryptoServiceProvider that accesses
        ' the key container MyKeyContainerName.
        Using rsa As New RSACryptoServiceProvider(parameters)
            ' Display the key information to the console.
            Console.WriteLine($"Key retrieved from container : {rsa.ToXmlString(True)}")
        End Using
    End Sub

    Private Shared Sub DeleteKeyFromContainer(ByVal ContainerName As String)
        ' Create the CspParameters object and set the key container
        '  name used to store the RSA key pair.
        Dim parameters As New CspParameters With {
            .KeyContainerName = ContainerName
        }

        ' Create a new instance of RSACryptoServiceProvider that accesses
        ' the key container.
        ' Delete the key entry in the container.
        Dim rsa As New RSACryptoServiceProvider(parameters) With {
            .PersistKeyInCsp = False
        }

        ' Call Clear to release resources and delete the key from the container.
        rsa.Clear()

        Console.WriteLine("Key deleted.")
    End Sub
End Class
```

```csharp
using System;
using System.Security.Cryptography;

public class StoreKey
{
    public static void Main()
    {
        try
        {
            // Create a key and save it in a container.
            GenKey_SaveInContainer("MyKeyContainer");

            // Retrieve the key from the container.
            GetKeyFromContainer("MyKeyContainer");

            // Delete the key from the container.
            DeleteKeyFromContainer("MyKeyContainer");

            // Create a key and save it in a container.
            GenKey_SaveInContainer("MyKeyContainer");

            // Delete the key from the container.
            DeleteKeyFromContainer("MyKeyContainer");
        }
        catch (CryptographicException e)
        {
            Console.WriteLine(e.Message);
        }
    }

    private static void GenKey_SaveInContainer(string containerName)
    {
        // Create the CspParameters object and set the key container
        // name used to store the RSA key pair.
        var parameters = new CspParameters
        {
            KeyContainerName = containerName
        };

        // Create a new instance of RSACryptoServiceProvider that accesses
        // the key container MyKeyContainerName.
        using var rsa = new RSACryptoServiceProvider(parameters);

        // Display the key information to the console.
        Console.WriteLine($"Key added to container: \n  {rsa.ToXmlString(true)}");
    }

    private static void GetKeyFromContainer(string containerName)
    {
        // Create the CspParameters object and set the key container
        // name used to store the RSA key pair.
        var parameters = new CspParameters
        {
            KeyContainerName = containerName
        };

        // Create a new instance of RSACryptoServiceProvider that accesses
        // the key container MyKeyContainerName.
        using var rsa = new RSACryptoServiceProvider(parameters);

        // Display the key information to the console.
        Console.WriteLine($"Key retrieved from container : \n {rsa.ToXmlString(true)}");
    }

    private static void DeleteKeyFromContainer(string containerName)
    {
        // Create the CspParameters object and set the key container
        // name used to store the RSA key pair.
        var parameters = new CspParameters
        {
            KeyContainerName = containerName
        };

        // Create a new instance of RSACryptoServiceProvider that accesses
        // the key container.
        using var rsa = new RSACryptoServiceProvider(parameters)
        {
            // Delete the key entry in the container.
            PersistKeyInCsp = false
        };

        // Call Clear to release resources and delete the key from the container.
        rsa.Clear();

        Console.WriteLine("Key deleted.");
    }
}
```

出力は次のようになります。

```console
Key added to container:
<RSAKeyValue> Key Information A</RSAKeyValue>
Key retrieved from container :
<RSAKeyValue> Key Information A</RSAKeyValue>
Key deleted.
Key added to container:
<RSAKeyValue> Key Information B</RSAKeyValue>
Key deleted.
```

## <a name="see-also"></a>関連項目

- [暗号化と復号化のためのキーの生成](generating-keys-for-encryption-and-decryption.md)
- [データの暗号化](encrypting-data.md)
- [データの復号化](decrypting-data.md)
- [暗号化サービス](cryptographic-services.md)
