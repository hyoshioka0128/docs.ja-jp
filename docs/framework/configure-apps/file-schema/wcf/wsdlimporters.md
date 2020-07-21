---
title: <wsdlImporters>
ms.date: 03/30/2017
ms.assetid: 270c7f93-eab7-47b6-8b94-ac3f5b7f17e4
ms.openlocfilehash: da9ab00c86e7f2657bfc28724d328ccbbc6957b1
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "69915159"
---
# \<wsdlImporters>
この構成要素は、WS-Policy が添付された Web サービス記述言語 (WSDL) 1.1 メタデータをインポートするすべての WSDL インポートを指定します。 各子要素は、 `wsdlImporter` メタデータをインポートする方法を指定し、その情報をコントラクトおよびエンドポイント情報を表すさまざまなクラスに変換する方法を指定する <> です。 コントラクトおよびエンドポイントの情報やプロパティを選択的にインポートできます。これらは、任意のインポート エラーを公開し、インポートおよび変換プロセスに関連する型情報を受け取ります。 また、任意のポリシー ドキュメント、WSDL ドキュメント、WSDL 拡張、および XML スキーマ ドキュメントにアクセスするためのバインディング情報およびプロパティのインポートもサポートします。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.MetadataElement>
- <xref:System.ServiceModel.Configuration.WsdlImporterElementCollection>
- <xref:System.ServiceModel.Description.MetadataImporter>
- <xref:System.ServiceModel.Description.WsdlImporter>
- [WCF クライアントの構成](../../../wcf/feature-details/client-configuration.md)
- [クライアント](../../../wcf/feature-details/clients.md)
