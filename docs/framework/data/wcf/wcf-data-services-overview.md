---
title: WCF Data Services の概要
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services
- WCF Data Services, about
ms.assetid: 7924cf94-c9a6-4015-afc9-f5d22b1743bb
ms.openlocfilehash: 21c09608bcf5d9f0b7bfc05b703d1ebe846a77bd
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73975061"
---
# <a name="wcf-data-services-overview"></a>WCF Data Services の概要
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] により、Open Data Protocol (OData) を使用して、Web またはイントラネット用のデータサービスの作成と使用が可能になります。 OData を使用すると、Uri でアドレス指定できるリソースとしてデータを公開できます。 したがって、Representational State Transfer (REST) のセマンティクス (標準的な HTTP 動詞 GET、PUT、POST、DELETE) を使用してデータにアクセスし、そのデータを変更できます。 このトピックでは、OData で定義されているパターンとプラクティスの概要と、.NET Framework ベースのアプリケーションで OData を利用するために [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] によって提供される機能について説明します。  
  
## <a name="address-data-as-resources"></a>リソースとしてのデータのアドレス指定  
 OData は、URI でアドレス指定できるリソースとしてデータを公開します。 リソース パスは、Entity Data Model のエンティティとリレーションシップの規則に基づいて構築されます。 このモデルでは、エンティティは、顧客、注文、アイテム、製品など、アプリケーションドメインのデータの操作単位を表します。 詳細については、「 [Entity Data Model](../adonet/entity-data-model.md)」を参照してください。  
  
 OData では、エンティティ型のインスタンスを含むエンティティセットとしてエンティティリソースのアドレスを設定します。 たとえば、URI <https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders> は、`Northwind` データサービスから、`CustomerID` 値を持つ顧客に関連付けられているすべての注文を返し `ALFKI.`  
  
 クエリ式を使用して、リソースに対して従来のクエリ操作 (フィルターの適用、並べ替え、ページングなど) を実行できます。 たとえば、URI <https://services.odata.org/Northwind/Northwind.svc/Customers( ' ALFKI ')/Orders? $filter = 貨物 gt 50 > は、リソースをフィルター処理して、輸送費が $50 以上の注文のみを返します。 詳細については、「[データサービスリソースへのアクセス](accessing-data-service-resources-wcf-data-services.md)」を参照してください。  
  
## <a name="interoperable-data-access"></a>相互運用可能なデータ アクセス  
 OData は、標準のインターネットプロトコルに基づいて、.NET Framework を使用しないアプリケーションとデータサービスを相互運用できるようにします。 標準の Uri を使用してデータのアドレスを指定できるため、アプリケーションは、Representational State Transfer (REST) のセマンティクス (特に、GET、PUT、POST、および DELETE の標準 HTTP 動詞) を使用してデータにアクセスし、変更することができます。 そのため、標準的な HTTP プロトコルを介して転送されるデータの解析、およびこれらのデータへのアクセスを行うことができる任意のクライアントからこれらのサービスにアクセスできます。  
  
 OData は、Atom 公開プロトコル (AtomPub) に対する一連の拡張機能を定義します。 さまざまなクライアント アプリケーションおよびプラットフォームに対応するために、複数のデータ形式による HTTP 要求と応答をサポートしています。 OData フィードは、Atom、JavaScript Object Notation (JSON)、および XML 形式のデータを表すことができます。 Atom が既定の形式ですが、フィードの形式は HTTP 要求のヘッダーで指定されます。 詳細については、 [odata: Atom 形式](https://go.microsoft.com/fwlink/?LinkID=185794)と[Odata: JSON 形式](https://go.microsoft.com/fwlink/?LinkID=185795)に関する説明を参照してください。  
  
 OData フィードとしてデータをパブリッシュする場合、[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] は、キャッシュや認証などの他の既存のインターネット機能に依存します。 これを実現するために、[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] は、ASP.NET、Windows Communication Foundation (WCF)、インターネットインフォメーションサービス (IIS) などの既存のホストアプリケーションおよびサービスと統合されています。  
  
## <a name="storage-independence"></a>ストレージの独立性  
 リソースはエンティティリレーションシップモデルに基づいてアドレス指定されますが、[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] は、基になるデータソースに関係なく、OData フィードを公開します。 URI で指定されたリソースへの HTTP 要求を [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] が受け取ると、その要求は逆シリアル化され、その要求の表現が [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] プロバイダーに渡されます。 このプロバイダーは、要求をデータ ソース固有の形式に変換し、基になるデータ ソースで要求を実行します。 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] は、OData によって規定されたリソースをアドレス指定する概念モデルを、基になるデータソースの特定のスキーマから分離することによって、ストレージの独立性を実現します。  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] と ADO.NET Entity Framework の組み合わせにより、リレーショナル データを公開するデータ サービスを作成できます。 Entity Data Model ツールを使用して、エンティティとしてアドレス指定可能なリソースを含むデータ モデルを作成すると同時に、このモデルと基になるデータベースのテーブルの間のマッピングを定義できます。 詳細については、「 [Entity Framework プロバイダー](entity-framework-provider-wcf-data-services.md)」を参照してください。  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] では、<xref:System.Linq.IQueryable%601> インターフェイスの実装を返すデータ構造を公開するデータサービスを作成することもできます。 そのため、.NET Framework 型からデータを公開するデータ サービスを作成できます。 <xref:System.Data.Services.IUpdatable> インターフェイスも実装すると、作成、更新、および削除操作がサポートされます。 詳細については、「[リフレクションプロバイダー](reflection-provider-wcf-data-services.md)」を参照してください。  
  
 これらのデータプロバイダーと [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] を統合する方法の図解は、このトピックで後述する「アーキテクチャ図」を参照してください。  
  
## <a name="custom-business-logic"></a>カスタム ビジネス ロジック  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] を使用すると、サービス操作とインターセプターを通じてカスタムビジネスロジックをデータサービスに簡単に追加できます。 サービス操作とは、データ リソースと同じ形態の URI によるアドレス指定が可能な、サーバーで定義されるメソッドです。 サービス操作では、クエリ式構文を使用して、操作によって返されるデータのフィルター、並べ替え、およびページングを行うこともできます。 たとえば、`http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$orderby=OrderDate&$top=10&$skip=10` という URI は、ロンドン (London) の顧客の注文を Northwind データ サービスから返し、ページングされた結果を `GetOrdersByCity` で並べ替える `OrderDate` というサービス操作への呼び出しを表します。 詳細については、「[サービス操作](service-operations-wcf-data-services.md)」を参照してください。  
  
 インターセプターを使用すると、カスタム アプリケーション ロジックをデータ サービスによる要求メッセージまたは応答メッセージの処理に統合できます。 インターセプターは、指定されたエンティティ セットに対してクエリ、挿入、更新、または削除の各操作が行われたときに呼び出されます。 インターセプターは、その後データの変更や承認ポリシーの強制を行うか、さらには操作を終了することもあります。 インターセプターのメソッドは、データ サービスによって公開される何らかのエンティティ セットに明示的に登録されている必要があります。 詳細については、「[インターセプター](interceptors-wcf-data-services.md)」を参照してください。  
  
## <a name="client-libraries"></a>クライアント ライブラリ  
 OData は、データサービスと対話するための一貫したパターンのセットを定義します。 これにより、データサービスを簡単に使用できるようにするクライアント側ライブラリなど、これらのサービスに基づく再利用可能なコンポーネントを作成できます。  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] には、.NET Framework ベースのクライアント アプリケーションと Silverlight ベースのクライアント アプリケーションの両方のクライアント ライブラリが含まれます。 これらのクライアント ライブラリでは、.NET Framework オブジェクトを使用してデータ サービスと対話できます。 また、オブジェクト ベースのクエリと LINQ クエリ、関連オブジェクトの読み込み、変更の追跡、および ID 解決もサポートしています。 詳細については、「 [WCF Data Services クライアントライブラリ](wcf-data-services-client-library.md)」を参照してください。  
  
 .NET Framework と Silverlight に含まれる OData クライアントライブラリに加えて、PHP、AJAX、Java アプリケーションなどのクライアントアプリケーションで OData フィードを使用できるようにするその他のクライアントライブラリもあります。 詳細については、 [ODATA SDK](https://go.microsoft.com/fwlink/?LinkID=185796)を参照してください。  
  
## <a name="architecture-overview"></a>アーキテクチャの概要  
 次の図は、odata フィードを公開し、OData 対応クライアントライブラリでこれらのフィードを使用するための [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] アーキテクチャを示しています。  
  
 ![WCF Data Services アーキテクチャダイアグラムを示すスクリーンショット。](./media/wcf-data-services-overview/windows-communication-foundation-data-services-architecture.gif)  
  
## <a name="see-also"></a>関連項目

- [WCF Data Services 4.5](index.md)
- [はじめに](getting-started-with-wcf-data-services.md)
- [WCF Data Services の定義](defining-wcf-data-services.md)
- [データサービスリソースへのアクセス (WCF Data Services)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd728283(v=vs.100))
- [WCF Data Services クライアント ライブラリ](wcf-data-services-client-library.md)
- [Representational State Transfer (REST)](https://go.microsoft.com/fwlink/?LinkId=113919)
