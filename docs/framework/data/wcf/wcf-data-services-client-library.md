---
title: WCF Data Services クライアント ライブラリ
description: WCF Data Services クライアント ライブラリを使用して .NET Framework クライアント アプリケーションからデータにアクセスしてデータを変更する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, client library
- DataServiceQuery class, about DataServiceQuery class
- DataServiceContext class, about DataServiceContext class
ms.assetid: 21075e50-8917-413e-a8ea-35a0f6e65aa5
ms.openlocfilehash: 58d038d5c2ac4973c2b41f4d49c1746f48f2a2fb
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247741"
---
# <a name="wcf-data-services-client-library"></a>WCF Data Services クライアント ライブラリ
HTTP 要求を送信し、データ サービスが返す Open Data Protocol (OData) フィードを処理できるのであれば、どのようなアプリケーションでも OData ベースのデータ サービスと対話できます。 この相互運用性によって、広範な Web 対応アプリケーションから OData ベースのサービスにアクセスすることが可能になります。 WCF Data Services には、.NET Framework ベースのアプリケーションまたは Silverlight ベースのアプリケーションから OData フィードを使用する際のプログラミング エクスペリエンスを向上させるクライアント ライブラリが含まれています。  
  
 クライアント ライブラリの 2 つの主要なクラスは、<xref:System.Data.Services.Client.DataServiceContext> クラスと <xref:System.Data.Services.Client.DataServiceQuery%601> クラスです。 <xref:System.Data.Services.Client.DataServiceContext> クラスは、特定のデータ サービスに対してサポートされている操作をカプセル化します。 OData サービスはステートレスですが、コンテキストはステートレスではありません。 このため <xref:System.Data.Services.Client.DataServiceContext> クラスを使用すると、変更管理などの機能をサポートするためにデータ サービスとの対話操作間におけるクライアントの状態を保持できます。 このクラスは、ID の管理と変更の追跡も行います。 <xref:System.Data.Services.Client.DataServiceQuery%601> クラスは、特定のエンティティ セットに対するクエリを表します。  
  
 このセクションでは、クライアント ライブラリを使用して .NET Framework クライアント アプリケーションからデータにアクセスしてデータを変更する方法について説明します。 Silverlight ベースのアプリケーションで WCF Data Services クライアント ライブラリを使用する方法については、「[WCF Data Services (Silverlight)](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc838234(v%3dvs.95))」を参照してください。 その他の種類のアプリケーションで OData フィードを使用する場合は、それぞれに対応したクライアント ライブラリが用意されています。 OData SDK の詳細については、[OData SDK のサンプルコード](https://www.odata.org/ecosystem/#sdk)を参照してください。
  
## <a name="in-this-section"></a>このセクションの内容  
 [データ サービス クライアント ライブラリの生成](generating-the-data-service-client-library-wcf-data-services.md)  
 クライアント ライブラリ、および OData フィードに基づくクライアント データ サービス クラスを生成する方法について説明します。  
  
 [データ サービスに対するクエリ](querying-the-data-service-wcf-data-services.md)  
 クライアント ライブラリを使用して .NET Framework ベースのアプリケーションからデータ サービスを照会する方法について説明します。  
  
 [遅延コンテンツの読み込み](loading-deferred-content-wcf-data-services.md)  
 最初のクエリ応答に含まれない追加のコンテンツを読み込む方法について説明します。  
  
 [データ サービスの更新](updating-the-data-service-wcf-data-services.md)  
 クライアント ライブラリを使用してエンティティおよびリレーションシップを作成、変更、および削除する方法について説明します。  
  
 [非同期操作](asynchronous-operations-wcf-data-services.md)  
 非同期でデータ サービスを操作するためにクライアント ライブラリで提供される機能について説明します。  
  
 [バッチ処理](batching-operations-wcf-data-services.md)  
 クライアント ライブラリを使用して複数の要求を 1 つのバッチでデータ サービスに送信する方法について説明します。  
  
 [コントロールへのデータのバインド](binding-data-to-controls-wcf-data-services.md)  
 コントロールをデータ サービスによって返される OData フィードにバインドする方法について説明します。  
  
 [サービス操作の呼び出し](calling-service-operations-wcf-data-services.md)  
 クライアント ライブラリを使用してサービス操作を呼び出す方法について説明します。  
  
 [データ サービス コンテキストの管理](managing-the-data-service-context-wcf-data-services.md)  
 クライアント ライブラリの動作を管理するオプションについて説明します。  
  
 [バイナリ データの操作](working-with-binary-data-wcf-data-services.md)  
 データ サービスによってデータ ストリームとして返されるバイナリ データにアクセスしてバイナリ データを変更する方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [WCF Data Services の定義](defining-wcf-data-services.md)
- [はじめに](getting-started-with-wcf-data-services.md)
