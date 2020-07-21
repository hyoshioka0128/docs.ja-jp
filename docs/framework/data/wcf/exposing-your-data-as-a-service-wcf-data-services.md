---
title: サービスとしてのデータの公開 (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, configuring
- getting started, WCF Data Services
- WCF Data Services, getting started
ms.assetid: df0bbcee-f66f-4a88-abb4-4e73c8b9c908
ms.openlocfilehash: 71f26d7d41d112e13e6a77f0927c61d51b176b27
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73975308"
---
# <a name="expose-your-data-as-a-service-wcf-data-services"></a>サービスとしてデータを公開する (WCF Data Services)

WCF Data Services を Visual Studio に統合すると、サービスを簡単に定義し、Open Data Protocol (OData) フィードとしてデータを公開できます。 OData フィードを公開するデータ サービスを作成するには、次のような基本的な手順を実行します。

1. **データ モデルを定義します。** WCF Data Services では、[ADO.NET Entity Framework](../adonet/ef/index.md) に基づくデータ モデルがネイティブでサポートされています。 詳細については、[ADO.NET Entity Framework データ ソースを使用してデータ サービスを作成する](create-a-data-service-using-an-adonet-ef-data-wcf.md)」を参照してください。

     WCF Data Services では、<xref:System.Linq.IQueryable%601> インターフェイスのインスタンスを返す共通言語ランタイム (CLR) オブジェクトに基づくデータ モデルもサポートされています。 そのため、.NET Framework のリスト、配列、およびコレクションに基づいてデータ サービスを配置できます。 これらのデータ構造での作成、更新、および削除操作を有効にするには、<xref:System.Data.Services.IUpdatable> インターフェイスも実装する必要があります。 詳細については、[リフレクション プロバイダーを使用してデータ サービスを作成する](create-a-data-service-using-rp-wcf-data-services.md)」を参照してください。

     より高度なシナリオの場合、WCF Data Services には、遅延バインディング データ型に基づいてデータ モデルを定義できるプロバイダーのセットが含まれています。 詳しくは、「[カスタム データ サービス プロバイダー](custom-data-service-providers-wcf-data-services.md)」をご覧ください。

2. **データ サービスを作成します。** 最も基本的なデータ サービスでは、 <xref:System.Data.Services.DataService%601> クラスを継承するクラスを `T` 型 (エンティティ コンテナーの名前空間修飾名) と一緒に公開します。 詳細については、「 [Defining WCF Data Services](defining-wcf-data-services.md)の開発と配置について説明します。

3. **データ サービスを構成します。** 既定では、WCF Data Services では、エンティティ コンテナーによって公開されているリソースへのアクセスは無効になります。 <xref:System.Data.Services.DataServiceConfiguration> インターフェイスを使用すると、リソースとサービス操作へのアクセスの構成、サポートされる OData のバージョンの指定、およびサービス全体のその他の動作 (バッチ動作や 1 つの応答で返すことができるエンティティの最大数など) を定義できます。 詳細については、「[データ サービスの構成](configuring-the-data-service-wcf-data-services.md)」を参照してください。

Northwind サンプル データベースに基づく単純なデータ サービスを作成する方法の例については、「[クイックスタート](quickstart-wcf-data-services.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [はじめに](getting-started-with-wcf-data-services.md)
- [概要](wcf-data-services-overview.md)
