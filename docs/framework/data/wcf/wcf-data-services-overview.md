---
title: WCF Data Services の概要
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services
- WCF Data Services, about
ms.assetid: 7924cf94-c9a6-4015-afc9-f5d22b1743bb
ms.openlocfilehash: e4c5bc03038a3df9df2b7629da762caee175b6e8
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202148"
---
# <a name="wcf-data-services-overview"></a>WCF Data Services の概要
WCF Data Services では、Open Data Protocol (OData) を使用して、Web またはイントラネット用のデータ サービスを作成し、それらを使用することができます。 OData を使用すると、URI でアドレス指定できるリソースとしてデータを公開できます。 したがって、Representational State Transfer (REST) のセマンティクス (標準的な HTTP 動詞 GET、PUT、POST、DELETE) を使用してデータにアクセスし、そのデータを変更できます。 このトピックでは、OData で定義されるパターンとプラクティスの両方の概要について説明します。また、.NET Framework ベースのアプリケーションで OData を利用するために WCF Data Services で提供される機能についても説明します。  
  
## <a name="address-data-as-resources"></a>リソースとしてのデータのアドレス指定  
 OData は、URI でアドレス指定できるリソースとしてデータを公開します。 リソース パスは、Entity Data Model のエンティティとリレーションシップの規則に基づいて構築されます。 このモデルでは、エンティティはアプリケーション ドメイン内のデータの操作単位を表します (顧客、注文、項目、製品など)。 詳細については、「[Entity Data Model](../adonet/entity-data-model.md)」を参照してください。  
  
 OData では、エンティティ型のインスタンスを含むエンティティ セットとしてエンティティ リソースのアドレスを指定します。 たとえば、`https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders` という URI を指定すると、`Northwind` データ サービスから、`CustomerID` の値が `ALFKI.` である顧客に関連するすべての注文が返されます。  
  
 クエリ式を使用して、リソースに対して従来のクエリ操作 (フィルターの適用、並べ替え、ページングなど) を実行できます。 たとえば、`https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders?$filter=Freight gt 50` という URI は、リソースをフィルターして、$50 以上の運賃の注文だけを返します。 詳細については、「[データ サービス リソースへのアクセス](accessing-data-service-resources-wcf-data-services.md)」を参照してください。  
  
## <a name="interoperable-data-access"></a>相互運用可能なデータ アクセス  
 OData は標準的なインターネット プロトコルに基づいているので、データ サービスは .NET Framework 対応でないアプリケーションとも相互運用が可能です。 標準的な URI を使用してデータのアドレスを指定できるので、アプリケーションでは Representational State Transfer (REST) のセマンティクス (特に GET、PUT、POST、および DELETE の HTTP 動詞) を使用してデータにアクセスして変更できます。 そのため、標準的な HTTP プロトコルを介して転送されるデータの解析、およびこれらのデータへのアクセスを行うことができる任意のクライアントからこれらのサービスにアクセスできます。  
  
OData では、Atom 公開プロトコル (AtomPub) に対する一連の拡張が定義されています。 さまざまなクライアント アプリケーションおよびプラットフォームに対応するために、複数のデータ形式による HTTP 要求と応答をサポートしています。 OData フィードでは、Atom、JavaScript Object Notation (JSON)、および通常の XML でデータを表現できます。 Atom が既定の形式ですが、フィードの形式は HTTP 要求のヘッダーで指定されます。 詳細については、[OData のAtom 形式](https://www.odata.org/documentation/odata-version-2-0/atom-format/)および [OData のJSON 形式](https://www.odata.org/documentation/odata-version-2-0/json-format/)に関するページを参照してください。  
  
 データを OData フィードとして公開すると、WCF Data Services では他の既存のインターネット機能がキャッシュや認証などの操作に使用されます。 これを可能にするため、WCF Data Services は ASP.NET、Windows Communication Foundation (WCF)、インターネット インフォメーション サービス (IIS) などの既存のホスト アプリケーションおよびサービスと統合されています。  
  
## <a name="storage-independence"></a>ストレージの独立性  
 リソースはエンティティ リレーションシップ モデルに基づいてアドレス指定されますが、WCF Data Services では、基になるデータ ソースとは関係なく OData フィードが公開されます。 WCF Data Services が URI によって識別されるリソースへの HTTP 要求を受け取ると、要求は逆シリアル化され、その要求の表現が WCF Data Services プロバイダーに渡されます。 このプロバイダーは、要求をデータ ソース固有の形式に変換し、基になるデータ ソースで要求を実行します。 WCF Data Services では、OData で規定されるリソースをアドレス指定する概念モデルと、基になるデータ ソースのスキーマとを分離することによって、ストレージの独立性が実現されます。  
  
 WCF Data Services は ADO.NET Entity Framework と統合されているので、リレーショナル データを公開するデータ サービスを作成できます。 Entity Data Model ツールを使用して、エンティティとしてアドレス指定可能なリソースを含むデータ モデルを作成すると同時に、このモデルと基になるデータベースのテーブルの間のマッピングを定義できます。 詳しくは、「[Entity Framework プロバイダー](entity-framework-provider-wcf-data-services.md)」をご覧ください。  
  
 WCF Data Services では、<xref:System.Linq.IQueryable%601> インターフェイスの実装を返すデータ構造を公開するデータ サービスを作成することもできます。 そのため、.NET Framework 型からデータを公開するデータ サービスを作成できます。 <xref:System.Data.Services.IUpdatable> インターフェイスも実装すると、作成、更新、および削除操作がサポートされます。 詳細については、「[リフレクション プロバイダー](reflection-provider-wcf-data-services.md)」を参照してください。  
  
 WCF Data Services をこれらのデータ プロバイダーと統合する方法については、このトピックの最後にあるアーキテクチャの図を参照してください。  
  
## <a name="custom-business-logic"></a>カスタム ビジネス ロジック  
 WCF Data Services を使用すると、サービス操作およびインターセプターを介してデータ サービスにカスタム ビジネス ロジックを簡単に追加できます。 サービス操作とは、データ リソースと同じ形態の URI によるアドレス指定が可能な、サーバーで定義されるメソッドです。 サービス操作では、クエリ式構文を使用して、操作によって返されるデータのフィルター、並べ替え、およびページングを行うこともできます。 たとえば、`http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$orderby=OrderDate&$top=10&$skip=10` という URI は、ロンドン (London) の顧客の注文を Northwind データ サービスから返し、ページングされた結果を `GetOrdersByCity` で並べ替える `OrderDate` というサービス操作への呼び出しを表します。 詳細については、「[サービス操作](service-operations-wcf-data-services.md)」を参照してください。  
  
 インターセプターを使用すると、カスタム アプリケーション ロジックをデータ サービスによる要求メッセージまたは応答メッセージの処理に統合できます。 インターセプターは、指定されたエンティティ セットに対してクエリ、挿入、更新、または削除の各操作が行われたときに呼び出されます。 インターセプターは、その後データの変更や承認ポリシーの強制を行うか、さらには操作を終了することもあります。 インターセプターのメソッドは、データ サービスによって公開される何らかのエンティティ セットに明示的に登録されている必要があります。 詳細については、「[インターセプター](interceptors-wcf-data-services.md)」を参照してください。  
  
## <a name="client-libraries"></a>クライアント ライブラリ  
 OData では、データ サービスと対話する統一パターンのセットが定義されています。 その結果、これらのサービスに基づいて再使用可能なコンポーネントを作成できます (データ サービスの使用を簡略化するクライアント側ライブラリなど)。  
  
 WCF Data Services には、.NET Framework ベースのクライアント アプリケーションと Silverlight ベースのクライアント アプリケーションの両方のクライアント ライブラリが含まれます。 これらのクライアント ライブラリでは、.NET Framework オブジェクトを使用してデータ サービスと対話できます。 また、オブジェクト ベースのクエリと LINQ クエリ、関連オブジェクトの読み込み、変更の追跡、および ID 解決もサポートしています。 詳細については、「[WCF Data Services クライアント ライブラリ](wcf-data-services-client-library.md)」を参照してください。  
  
 .NET Framework および Silverlight に含まれる OData クライアント ライブラリのほかに、PHP、AJAX、Java アプリケーションなどのクライアント アプリケーションで OData フィードを使用できるようにするクライアント ライブラリがあります。 OData SDK の詳細については、[OData SDK のサンプルコード](https://www.odata.org/ecosystem/#sdk)を参照してください。
  
## <a name="architecture-overview"></a>アーキテクチャの概要  
 OData フィードを公開し、OData 対応クライアント ライブラリでこれらのフィードを使用するための WCF Data Services アーキテクチャを次の図に示します。  
  
 ![WCF Data Services アーキテクチャ図を示すスクリーンショット。](./media/wcf-data-services-overview/windows-communication-foundation-data-services-architecture.gif)  
  
## <a name="see-also"></a>関連項目

- [WCF Data Services 4.5](index.md)
- [はじめに](getting-started-with-wcf-data-services.md)
- [WCF Data Services の定義](defining-wcf-data-services.md)
- [データ サービス リソースへのアクセス (WCF Data Services)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/dd728283(v=vs.100))
- [WCF Data Services クライアント ライブラリ](wcf-data-services-client-library.md)
- [Representational State Transfer (REST)](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
