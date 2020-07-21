---
title: エンドポイント:アドレス、バインディング、およびコントラクト
description: WCF サービスとのすべての通信がサービスエンドポイントを介してどのように行われるかについて説明します。これにより、クライアントがサービスによって提供される機能にアクセスできるようになります。
ms.date: 03/30/2017
helpviewer_keywords:
- endpoints [WCF]
- Windows Communication Foundation [WCF], endpoints
- WCF [WCF], endpoints
ms.assetid: 9ddc46ee-1883-4291-9926-28848c57e858
ms.openlocfilehash: ce0874bfed716716b6fd1801b35a4266095cd752
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247313"
---
# <a name="endpoints-addresses-bindings-and-contracts"></a>エンドポイント:アドレス、バインディング、およびコントラクト

Windows Communication Foundation (WCF) サービスとの通信はすべて、サービスの*エンドポイント*を介して行われます。 エンドポイントは、クライアントが WCF サービスによって提供される機能にアクセスできるようにします。

各エンドポイントは、次の 4 つのプロパティで構成されます。

- そのエンドポイントの場所を示すアドレス。

- クライアントがエンドポイントと通信する方法を指定するバインディング。

- 利用可能な操作を識別するためのコントラクト。

- エンドポイントのローカル実装の詳細を指定する一連の動作。

このトピックでは、このエンドポイント構造について説明し、WCF オブジェクトモデルでの表現方法について説明します。

## <a name="the-structure-of-an-endpoint"></a>エンドポイントの構造

各エンドポイントの構造は次のとおりです。

- アドレス : アドレスは、エンドポイントを一意に識別し、サービスの潜在的ユーザーにそのエンドポイントの場所を示します。 これは、WCF オブジェクトモデルでクラスによって表され <xref:System.ServiceModel.EndpointAddress> ます。 <xref:System.ServiceModel.EndpointAddress> クラスには次のものが含まれます。

  - <xref:System.ServiceModel.EndpointAddress.Uri%2A> プロパティは、サービスのアドレスを表します。

  - <xref:System.ServiceModel.EndpointAddress.Identity%2A> プロパティは、サービスのセキュリティ ID とオプションのメッセージ ヘッダーのコレクションを表します。 オプションのメッセージ ヘッダーは、エンドポイントの識別またはエンドポイントとの対話のための、より詳細なアドレス指定情報を追加するために使用されます。

  詳細については、「[エンドポイントアドレスの指定](../specifying-an-endpoint-address.md)」を参照してください。

- バインディング : バインディングは、エンドポイントとの通信方法を指定します。 これには次のものが含まれます

  - 使用するトランスポート プロトコル (例 : TCP や HTTP)。

  - メッセージに使用するエンコーディング (例 : テキストやバイナリ)。

  - 必要なセキュリティ要件 (例 : SSL メッセージ セキュリティや SOAP メッセージ セキュリティ)。

  詳細については、「 [WCF バインディングの概要](../bindings-overview.md)」を参照してください。 バインドは、WCF オブジェクトモデルで抽象基本クラスによって表され <xref:System.ServiceModel.Channels.Binding> ます。 ほとんどのシナリオでは、システム指定のバインディングを使用できます。 詳細については、「[システム指定のバインディング](../system-provided-bindings.md)」を参照してください。

- コントラクト : コントラクトは、エンドポイントがクライアントに公開する機能を示します。 コントラクトは、以下の項目を指定します。

  - クライアントから呼び出すことができる操作。

  - メッセージの形式。

  - 操作を呼び出すために必要な入力パラメーターまたはデータの型。

  - クライアントが予期できる処理メッセージまたは応答メッセージの種類。

  コントラクトを定義する方法の詳細については、「[サービスコントラクトの設計](../designing-service-contracts.md)」を参照してください。

- 動作 : エンドポイントの動作を使用すると、サービス エンドポイントのローカル動作をカスタマイズできます。 エンドポイント動作では、WCF ランタイムの構築プロセスに参加することによってこれを実現します。 エンドポイントの動作の一例は、<xref:System.ServiceModel.Description.ServiceEndpoint.ListenUri%2A> プロパティです。このプロパティにより、SOAP アドレスまたは Web サービス記述言語 (WSDL) アドレスとは異なるリッスン アドレスを指定できます。 詳細については、「 [ClientViaBehavior](../diagnostics/wmi/clientviabehavior.md)」を参照してください。

## <a name="defining-endpoints"></a>エンドポイントの定義

サービスのエンドポイントは、コードを使用して強制的に指定するか、構成を介して宣言として指定することができます。 詳細については、「[方法: 構成でサービスエンドポイントを作成](how-to-create-a-service-endpoint-in-configuration.md)する」および「[方法: コードでサービスエンドポイントを作成する](how-to-create-a-service-endpoint-in-code.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

このセクションでは、バインディング、エンドポイント、およびアドレスの目的を説明し、バインディングとエンドポイントの構成方法および `ClientVia` 動作と `ListenUri` プロパティの使用方法を示します。

[扱い](endpoint-addresses.md)\
WCF でのエンドポイントのアドレス指定方法について説明します。

[現存](bindings.md)\
バインディングを使用して、クライアントとサービスが相互に通信するために必要なトランスポート、エンコーディング、およびプロトコルの詳細を指定する方法について説明します。

[関する](contracts.md)\
コントラクトでサービスのメソッドが定義されるしくみについて説明します。

[方法: 構成にサービスエンドポイントを作成する](how-to-create-a-service-endpoint-in-configuration.md)\
構成にサービス エンドポイントを作成する方法について説明します。

[方法: コードでサービスエンドポイントを作成する](how-to-create-a-service-endpoint-in-code.md)\
コード内にサービス エンドポイントを作成する方法について説明します。

[方法: Svcutil.exe を使用してコンパイル済みサービスコードを検証する](how-to-use-svcutil-exe-to-validate-compiled-service-code.md)\
[ServiceModel メタデータユーティリティツール (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を使用してサービスをホストせずにサービスの実装と構成でエラーを検出する方法について説明します。

## <a name="see-also"></a>関連項目

- [サービスの構成](../configuring-services.md)
- [バインディングの拡張](../extending/extending-bindings.md)
