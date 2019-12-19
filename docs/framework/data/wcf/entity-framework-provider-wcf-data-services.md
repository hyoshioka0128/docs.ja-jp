---
title: Entity Framework プロバイダー (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: 650b5eb6-c71d-4dc1-8b64-b6beaf752114
ms.openlocfilehash: 0b75e9645f05e5e83ff76cc138ee37e90600769a
ms.sourcegitcommit: 79a2d6a07ba4ed08979819666a0ee6927bbf1b01
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2019
ms.locfileid: "74569263"
---
# <a name="entity-framework-provider-wcf-data-services"></a>Entity Framework プロバイダー (WCF Data Services)
WCF Data Services と同様に、ADO.NET Entity Framework は、エンティティリレーションシップモデルの一種である Entity Data Model に基づいています。 Entity Framework は、*概念モデル*と呼ばれる Entity Data Model の実装に対する操作を、データソースに対する同等の操作に変換します。 これにより Entity Framework は、リレーショナルデータに基づくデータサービスの理想的なプロバイダーになります。また、Entity Framework をサポートするデータプロバイダーを持つデータベースであれば、WCF Data Services で使用できます。 現在 Entity Framework をサポートしているデータソースの一覧については、「 [Entity Framework のサードパーティプロバイダー](https://go.microsoft.com/fwlink/?LinkId=143699)」を参照してください。  
  
 概念モデルでは、エンティティ コンテナーはサービスのルートです。 データ サービスでデータを公開する前に、Entity Framework で概念モデルを定義する必要があります。 詳細については、「[方法: ADO.NET Entity Framework データソースを使用してデータサービスを作成](create-a-data-service-using-an-adonet-ef-data-wcf.md)する」を参照してください。  
  
 WCF Data Services は、エンティティの同時実行トークンを定義できるようにすることで、オプティミスティック同時実行制御モデルをサポートします。 このコンカレンシー トークンは、エンティティの 1 つ以上のプロパティが含まれており、要求、更新、または削除されているデータに対して行われた変更があるかどうかを判断するためにデータ サービスによって使用されます。 要求内の eTag から取得したトークンの値がエンティティの現在の値と異なる場合、データ サービスで例外が発生します。 プロパティが同時実行トークンの一部であることを示すには、Entity Framework プロバイダーによって定義されたデータモデルで属性 `ConcurrencyMode="Fixed"` を適用する必要があります。 コンカレンシー トークンには、キー プロパティまたはナビゲーション プロパティを含めることはできません。 詳細については、「[データサービスの更新](updating-the-data-service-wcf-data-services.md)」を参照してください。  
  
 Entity Framework の詳細については、「 [Entity Framework の概要](../adonet/ef/overview.md)」を参照してください。  
  
## <a name="see-also"></a>参照

- [Data Services プロバイダー](data-services-providers-wcf-data-services.md)
- [リフレクション プロバイダー](reflection-provider-wcf-data-services.md)
- [Entity Data Model](../adonet/entity-data-model.md)
