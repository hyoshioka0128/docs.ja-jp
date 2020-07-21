---
title: '方法: 双方向コントラクトを使用してサービスにアクセスする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- duplex contracts [WCF]
ms.assetid: 746a9d64-f21c-426c-b85d-972e916ec6c5
ms.openlocfilehash: bc42792b827b49265a0b1addf959de2fa1a041e3
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597216"
---
# <a name="how-to-access-services-with-a-duplex-contract"></a>方法: 双方向コントラクトを使用してサービスにアクセスする

Windows Communication Foundation (WCF) の1つの機能は、双方向のメッセージングパターンを使用するサービスを作成する機能です。 双方向のメッセージング パターンを使用するサービスは、コールバックを通じてクライアントと通信できます。 このトピックでは、コールバックインターフェイスを実装するクライアントクラスで WCF クライアントを作成する手順について説明します。

二重バインディングでは、クライアントの IP アドレスをサービスに公開します。 クライアントは、セキュリティを使用して信頼するサービスだけに接続できるようにする必要があります。

基本的な WCF サービスとクライアントの作成に関するチュートリアルについては、[はじめにチュートリアル](../getting-started-tutorial.md)を参照してください。

## <a name="to-access-a-duplex-service"></a>双方向サービスにアクセスするには

1. 2 つのインターフェイスを含むサービスを作成します。 1 つ目のインターフェイスはサービスに使用し、2 つ目のインターフェイスはコールバックに使用します。 双方向サービスの作成の詳細については、「[方法: 双方向コントラクトを作成](how-to-create-a-duplex-contract.md)する」を参照してください。

2. サービスを実行します。

3. [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を使用して、クライアントのコントラクト (インターフェイス) を生成します。 この方法の詳細については、「[方法: クライアントを作成](../how-to-create-a-wcf-client.md)する」を参照してください。

4. 次の例に示すように、クライアント クラスにコールバック インターフェイスを実装します。

    ```csharp
    public class CallbackHandler : ICalculatorDuplexCallback
    {
        public void Result(double result)
        {
            Console.WriteLine("Result ({0})", result);
        }
        public void Equation(string equation)
        {
            Console.WriteLine("Equation({0})", equation);
        }
    }
    ```

    ```vb
    Public Class CallbackHandler
    Implements ICalculatorDuplexCallback
       Public Sub Result (ByVal result As Double)
          Console.WriteLine("Result ({0})", result)
       End Sub
        Public Sub Equation(ByVal equation As String)
            Console.WriteLine("Equation({0})", equation)
        End Sub
    End Class
    ```

5. <xref:System.ServiceModel.InstanceContext> クラスのインスタンスを作成します。 コンストラクターには、クライアント クラスのインスタンスが必要です。

    ```csharp
    InstanceContext site = new InstanceContext(new CallbackHandler());
    ```

    ```vb
    Dim site As InstanceContext = New InstanceContext(new CallbackHandler())
    ```

6. オブジェクトを必要とするコンストラクターを使用して、WCF クライアントのインスタンスを作成し <xref:System.ServiceModel.InstanceContext> ます。 コンストラクターの 2 番目のパラメーターは、構成ファイルに含まれるエンドポイントの名前です。

    ```csharp
    CalculatorDuplexClient wcfClient = new CalculatorDuplexClient(site, "default");
    ```

    ```vb
    Dim wcfClient As New CalculatorDuplexClient(site, "default")
    ```

7. 必要に応じて、WCF クライアントのメソッドを呼び出します。

## <a name="example"></a>例

双方向コントラクトにアクセスするクライアント クラスを作成する方法を次のコード例に示します。

[!code-csharp[S_DuplexClients#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_duplexclients/cs/client.cs#1)]
[!code-vb[S_DuplexClients#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_duplexclients/vb/client.vb#1)]

## <a name="see-also"></a>関連項目

- [はじめにチュートリアル](../getting-started-tutorial.md)
- [方法: 双方向コントラクトを作成する](how-to-create-a-duplex-contract.md)
- [ServiceModel メタデータ ユーティリティ ツール (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)
- [方法: クライアントを作成する](../how-to-create-a-wcf-client.md)
- [方法: ChannelFactory を使用する](how-to-use-the-channelfactory.md)
