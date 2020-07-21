---
title: '方法: コントラクトを SOAP クライアントおよび Web クライアントに公開する'
description: SOAP と SOAP 以外のクライアントの両方で WFC サーバーエンドポイントを使用できるようにする方法について説明します。 既定では、エンドポイントは SOAP クライアントでのみ使用できます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: bb765a48-12f2-430d-a54d-6f0c20f2a23a
ms.openlocfilehash: b1bdb7af51e0e2795c36865058fbeb34a716e3e2
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246975"
---
# <a name="how-to-expose-a-contract-to-soap-and-web-clients"></a>方法: コントラクトを SOAP クライアントおよび Web クライアントに公開する

既定では、Windows Communication Foundation (WCF) は、エンドポイントを SOAP クライアントのみに使用できるようにします。 [「方法: 基本的な WCF WEB HTTP サービスを作成](how-to-create-a-basic-wcf-web-http-service.md)する」では、SOAP 以外のクライアントがエンドポイントを使用できるようにします。 状況によっては、同じコントラクトを Web エンドポイントと SOAP エンドポイントのどちらとしても利用できることが望ましい場合があります。 ここでは、これを実現する方法の例について示します。

## <a name="to-define-the-service-contract"></a>サービス コントラクトを定義するには

1. <xref:System.ServiceModel.ServiceContractAttribute> <xref:System.ServiceModel.Web.WebInvokeAttribute> 次のコードに示すように、、、および属性でマークされたインターフェイスを使用して、サービスコントラクトを定義し <xref:System.ServiceModel.Web.WebGetAttribute> ます。

    [!code-csharp[htSoapWeb#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#0)]
    [!code-vb[htSoapWeb#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#0)]

    > [!NOTE]
    > 既定では、<xref:System.ServiceModel.Web.WebInvokeAttribute> は POST 呼び出しを操作にマッピングします。 ただし、"method=" パラメーターを指定することで、操作にマッピングするメソッドを指定できます。 <xref:System.ServiceModel.Web.WebGetAttribute> には "method=" パラメーターがないため、サービス操作には GET 呼び出しのみがマッピングされます。

2. 次のコードに示すように、サービスコントラクトを実装します。

     [!code-csharp[htSoapWeb#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#1)]
     [!code-vb[htSoapWeb#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#1)]

## <a name="to-host-the-service"></a>サービスをホストするには

1. 次の <xref:System.ServiceModel.ServiceHost> コードに示すように、オブジェクトを作成します。

     [!code-csharp[htSoapWeb#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#2)]
     [!code-vb[htSoapWeb#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#2)]

2. 次の <xref:System.ServiceModel.Description.ServiceEndpoint> <xref:System.ServiceModel.BasicHttpBinding> コードに示すように、SOAP エンドポイントに対してを追加します。

     [!code-csharp[htSoapWeb#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#3)]
     [!code-vb[htSoapWeb#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#3)]

3. 次の <xref:System.ServiceModel.Description.ServiceEndpoint> <xref:System.ServiceModel.WebHttpBinding> コードに示すように、SOAP 以外のエンドポイントに対してを追加し、 <xref:System.ServiceModel.Description.WebHttpBehavior> エンドポイントにを追加します。

     [!code-csharp[htSoapWeb#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#4)]
     [!code-vb[htSoapWeb#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#4)]

4. `Open()` <xref:System.ServiceModel.ServiceHost> 次のコードに示すように、インスタンスでを呼び出して、サービスホストを開きます。

     [!code-csharp[htSoapWeb#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#5)]
     [!code-vb[htSoapWeb#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#5)]

## <a name="to-call-service-operations-mapped-to-get-in-internet-explorer"></a>Internet Explorer で GET にマッピングされたサービス操作を呼び出すには

1. Internet Explorer を開き、「 `http://localhost:8000/Web/EchoWithGet?s=Hello, world!` 」と入力して、enter キーを押します。 URL には、サービスのベースアドレス ( `http://localhost:8000/` )、エンドポイントの相対アドレス ("")、呼び出すサービス操作 ("EchoWithGet")、アンパサンド (&) で区切られた名前付きパラメーターのリストが含まれています。

## <a name="to-call-service-operations-on-the-web-endpoint-in-code"></a>コードから Web エンドポイントにあるサービス操作を呼び出すには

1. 次のコードに示すように、<xref:System.ServiceModel.Web.WebChannelFactory%601> のインスタンスを `using` ブロック内に作成します。

     [!code-csharp[htSoapWeb#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#6)]
     [!code-vb[htSoapWeb#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#6)]

> [!NOTE]
> `Close()` は `using` ブロックの末尾のチャネルで自動的に呼び出されます。

1. 次のコードに示すように、チャネルを作成してサービスを呼び出します。

     [!code-csharp[htSoapWeb#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#8)]
     [!code-vb[htSoapWeb#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#8)]

## <a name="to-call-service-operations-on-the-soap-endpoint"></a>SOAP エンドポイントにあるサービス操作を呼び出すには

1. 次のコードに示すように、<xref:System.ServiceModel.ChannelFactory> のインスタンスを `using` ブロック内に作成します。

    [!code-csharp[htSoapWeb#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#10)]
    [!code-vb[htSoapWeb#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#10)]

2. 次のコードに示すように、チャネルを作成してサービスを呼び出します。

    [!code-csharp[htSoapWeb#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#11)]
    [!code-vb[htSoapWeb#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#11)]

## <a name="to-close-the-service-host"></a>サービス ホストを閉じるは

1. 次のコードに示すように、サービス ホストを閉じます。

    [!code-csharp[htSoapWeb#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#9)]
    [!code-vb[htSoapWeb#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#9)]

## <a name="example"></a>例

このトピックの完全なコードリストを次に示します。

[!code-csharp[htSoapWeb#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/htsoapweb/cs/program.cs#13)]
[!code-vb[htSoapWeb#13](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/htsoapweb/vb/program.vb#13)]

## <a name="compiling-the-code"></a>コードのコンパイル

 Service.cs のコンパイル時には、System.ServiceModel.dll と System.ServiceModel.Web.dll を参照します。

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
- <xref:System.ServiceModel.Web.WebInvokeAttribute>
- <xref:System.ServiceModel.Web.WebServiceHost>
- <xref:System.ServiceModel.ChannelFactory>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- [WCF Web HTTP プログラミング モデル](wcf-web-http-programming-model.md)
