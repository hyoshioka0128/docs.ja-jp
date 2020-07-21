---
title: '方法: 基本的な WCF Web HTTP サービスを作成する'
description: WCF で web エンドポイントを公開するサービスを作成する方法について説明します。 Web エンドポイントは、XML または JSON を使用してデータを送信します。 SOAP エンベロープがありません。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 877662d3-d372-4e08-b417-51f66a0095cd
ms.openlocfilehash: 7481367f27d973ba809dff5ca1c4a4f168fbbb98
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247105"
---
# <a name="how-to-create-a-basic-wcf-web-http-service"></a>方法: 基本的な WCF Web HTTP サービスを作成する

Windows Communication Foundation (WCF) を使用すると、Web エンドポイントを公開するサービスを作成できます。 Web エンドポイントは、XML または JSON でデータを送信します。SOAP エンベロープはありません。 ここでは、このようなエンドポイントを公開する方法を示します。

> [!NOTE]
> Web エンドポイントをセキュリティで保護する唯一の方法は、トランスポート セキュリティを使用する HTTPS を介してエンドポイントを公開することです。 メッセージ ベースのセキュリティを使用する場合、セキュリティ情報は通常 SOAP ヘッダーに配置されます。SOAP 以外のエンドポイントに送信するメッセージには SOAP エンベロープが含まれないため、セキュリティ情報を配置する場所がなく、トランスポート セキュリティに依存する必要があります。

## <a name="to-create-a-web-endpoint"></a>Web エンドポイントを作成するには

1. <xref:System.ServiceModel.ServiceContractAttribute>、<xref:System.ServiceModel.Web.WebInvokeAttribute>、および <xref:System.ServiceModel.Web.WebGetAttribute> の各属性でマークされたインターフェイスを使用して、サービス コントラクトを定義します。

     [!code-csharp[htBasicService#0](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#0)]
     [!code-vb[htBasicService#0](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#0)]

    > [!NOTE]
    > 既定では、<xref:System.ServiceModel.Web.WebInvokeAttribute> は POST 呼び出しを操作にマッピングします。 ただし、"method=" パラメーターを指定することで、操作にマッピングする HTTP メソッド (HEAD、PUT、DELETE など) を指定できます。 <xref:System.ServiceModel.Web.WebGetAttribute> には "method=" パラメーターがないため、サービス操作には GET 呼び出しのみがマッピングされます。

2. サービス コントラクトを実装します。

     [!code-csharp[htBasicService#1](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#1)]
     [!code-vb[htBasicService#1](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#1)]

## <a name="to-host-the-service"></a>サービスをホストするには

1. <xref:System.ServiceModel.Web.WebServiceHost> オブジェクトを作成します。

     [!code-csharp[htBasicService#2](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#2)]
     [!code-vb[htBasicService#2](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#2)]

2. <xref:System.ServiceModel.Description.ServiceEndpoint> を持つ <xref:System.ServiceModel.Description.WebHttpBehavior> を追加します。

     [!code-csharp[htBasicService#3](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#3)]
     [!code-vb[htBasicService#3](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#3)]

    > [!NOTE]
    > エンド ポイントを追加しない場合は、<xref:System.ServiceModel.Web.WebServiceHost> が自動的に既定のエンド ポイントを作成します。 <xref:System.ServiceModel.Web.WebServiceHost> は、他にも <xref:System.ServiceModel.Description.WebHttpBehavior> を追加し、HTTP ヘルプ ページと Web サービス記述言語 (WSDL) GET 機能を無効にすることによって、メタデータ エンドポイントが既定の HTTP エンドポイントに干渉しないようにします。
    >
    >  URL が "" である SOAP 以外のエンドポイントを追加すると、エンドポイント上の操作の呼び出しを行うときに予期しない動作が発生します。 これは、エンドポイントのリッスン URI が、ヘルプページ (WCF サービスのベースアドレスを参照するときに表示されるページ) と同じであるためです。

     これを回避するには、次のいずれかの操作を行います。

    - SOAP 以外のエンドポイントについては、空ではない URI を指定するようにします。

    - ヘルプ ページを無効にします。 これは、次のコードを使用して行うことができます。

     [!code-csharp[htBasicService#4](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#4)]
     [!code-vb[htBasicService#4](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#4)]

3. サービス ホストを開き、ユーザーが Enter キーを押すのを待ちます。

     [!code-csharp[htBasicService#5](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/snippets.cs#5)]
     [!code-vb[htBasicService#5](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/snippets.vb#5)]

     このサンプルでは、コンソール アプリケーションで Web スタイル サービスをホストする方法を示します。 IIS からこのようなサービスをホストすることもできます。 これを行うには、次のコードに示すように、.svc ファイルで <xref:System.ServiceModel.Activation.WebServiceHostFactory> クラスを指定します。

    ```text
    <%ServiceHost
        language=c#
        Debug="true"
        Service="Microsoft.Samples.Service"
        Factory=System.ServiceModel.Activation.WebServiceHostFactory%>
    ```

## <a name="to-call-service-operations-mapped-to-get-in-internet-explorer"></a>Internet Explorer で GET にマッピングされたサービス操作を呼び出すには

1. Internet Explorer を開き、「 `http://localhost:8000/EchoWithGet?s=Hello, world!` 」と入力して、enter キーを押します。 URL には、サービスのベースアドレス ( `http://localhost:8000/` )、エンドポイントの相対アドレス ("")、呼び出すサービス操作 ("EchoWithGet")、アンパサンド (&) で区切られた名前付きパラメーターのリストが含まれています。

## <a name="to-call-service-operations-in-code"></a>コードからサービス操作を呼び出すには

1. <xref:System.ServiceModel.ChannelFactory%601> ブロック内で `using` のインスタンスを作成します。

     [!code-csharp[htBasicService#6](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#6)]
     [!code-vb[htBasicService#6](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#6)]

2. <xref:System.ServiceModel.Description.WebHttpBehavior> が呼び出すエンドポイントに <xref:System.ServiceModel.ChannelFactory%601> を追加します。

     [!code-csharp[htBasicService#7](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#7)]
     [!code-vb[htBasicService#7](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#7)]

3. チャネルを作成し、サービスを呼び出します。

     [!code-csharp[htBasicService#8](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#8)]
     [!code-vb[htBasicService#8](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#8)]

4. <xref:System.ServiceModel.Web.WebServiceHost> を閉じます。

     [!code-csharp[htBasicService#9](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#9)]
     [!code-vb[htBasicService#9](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#9)]

## <a name="example"></a>例

この例の完全なコードの一覧を以下に示します。

[!code-csharp[htBasicService#10](~/samples/snippets/csharp/VS_Snippets_CFX/htbasicservice/cs/service.cs#10)]
[!code-vb[htBasicService#10](~/samples/snippets/visualbasic/VS_Snippets_CFX/htbasicservice/vb/service.vb#10)]

## <a name="compiling-the-code"></a>コードのコンパイル

Service.cs のコンパイル時には、System.ServiceModel.dll と System.ServiceModel.Web.dll が参照されます。

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.WebHttpBinding>
- <xref:System.ServiceModel.Web.WebGetAttribute>
- <xref:System.ServiceModel.Web.WebInvokeAttribute>
- <xref:System.ServiceModel.Web.WebServiceHost>
- <xref:System.ServiceModel.Description.WebHttpBehavior>
- [WCF Web HTTP プログラミング モデル](wcf-web-http-programming-model.md)
