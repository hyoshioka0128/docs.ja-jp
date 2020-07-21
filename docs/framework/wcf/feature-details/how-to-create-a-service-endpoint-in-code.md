---
title: '方法: コード内にサービス エンドポイントを作成する'
description: クラスでサービスを実装し、そのエンドポイントをプログラムで定義する方法について説明します。 WCF では、エンドポイントは通常、構成ファイルで定義されます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3fbb22fa-2930-48b8-b437-def1de87c6a0
ms.openlocfilehash: 3b2ff2a17975bc381db61edc2c0f85f67edd3325
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247053"
---
# <a name="how-to-create-a-service-endpoint-in-code"></a>方法: コード内にサービス エンドポイントを作成する
この例では、電卓サービスに `ICalculator` コントラクトを定義し、そのサービスを `CalculatorService` クラスに実装し、コード内でサービス エンドポイントを定義します。このエンドポイントでは、サービスが <xref:System.ServiceModel.BasicHttpBinding> クラスを使用するように指定します。  
  
 通常、ベスト プラクティスは、コードで命令として記述するよりも、構成でバインディングを指定して情報を明示的にアドレス指定することです。 設置済みサービスのバインドおよびアドレスは一般的に、サービスの開発中に使用されるものとは異なるので、コード内でエンドポイントを定義することは通常、実用的ではありません。 一般的に、バインディング情報とアドレス情報をコードに含めないことで、変更時にアプリケーションの再コンパイルや再展開を行う必要がなくなります。  
  
#### <a name="to-create-a-service-endpoint-in-code"></a>コード内にサービス エンドポイントを作成するには  
  
1. サービス コントラクトを定義するインターフェイスを作成します。  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#1)]
     [!code-vb[c_HowTo_CodeServiceBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#1)]  
  
2. 手順 1. で定義したサービス コントラクトを実装します。  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#2)]
     [!code-vb[c_HowTo_CodeServiceBinding#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#2)]  
  
3. アプリケーションをホストする場合は、サービスで使用するサービスとバインディングのベース アドレスを作成します。  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#3)]
     [!code-vb[c_HowTo_CodeServiceBinding#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#3)]  
  
4. ホストを作成し、<xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%28System.Type%2CSystem.ServiceModel.Channels.Binding%2CSystem.String%29?displayProperty=nameWithType> または他のオーバーロードの 1 つを呼び出して、ホストのサービス エンドポイントを追加します。  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#6)]
     [!code-vb[c_HowTo_CodeServiceBinding#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#6)]  
  
     コードでバインディングを指定し、ランタイムによって提供される既定のエンドポイントを使用するには、を作成するときにベースアドレスをコンストラクターに渡し、を <xref:System.ServiceModel.ServiceHost> 呼び出しません <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A?displayProperty=nameWithType> 。  
  
     [!code-csharp[c_HowTo_CodeServiceBinding#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_codeservicebinding/cs/source.cs#7)]
     [!code-vb[c_HowTo_CodeServiceBinding#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_codeservicebinding/vb/source.vb#7)]  
  
     既定のエンドポイントの詳細については、「 [WCF サービスの](../samples/simplified-configuration-for-wcf-services.md)構成と簡略化された構成の[簡略化](../simplified-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [方法: コード内でサービス バインディングを指定する](../how-to-specify-a-service-binding-in-code.md)
