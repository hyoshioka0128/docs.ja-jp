---
title: アプリケーション ドメインからのセットアップ情報の取得
description: System.AppDomain クラスまたは AppDomainSetup オブジェクトを使用し、.NET でアプリケーション ドメインからセットアップ情報を取得します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- AppDomainSetup object
- retrieving setup information
- application domains, retrieving setup information
ms.assetid: 5cdb12ae-1e37-4a62-8ec7-93d6dcc6e8d9
ms.openlocfilehash: 3b7fdd302ac11caa423815483a4add38264f0910
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325663"
---
# <a name="retrieve-setup-information-from-an-application-domain"></a>アプリケーション ドメインからのセットアップ情報を取得する

アプリケーション ドメインの各インスタンスは、プロパティと <xref:System.AppDomainSetup> 情報の両方で構成されています。 <xref:System.AppDomain?displayProperty=nameWithType> クラスを使って、アプリケーション ドメインからセットアップ情報を取得できます。 このクラスでは、アプリケーション ドメインに関する構成情報を取得する複数のメンバーが提供されています。  
  
 また、アプリケーション ドメインの **AppDomainSetup** オブジェクトに対してクエリを実行し、作成時にドメインに渡されたセットアップ情報を取得することもできます。  
  
 次の例では、新しいアプリケーション ドメインを作成し、いくつかのメンバーの値をコンソールに出力しています。  
  
 [!code-cpp[AppDomain_Setup#2](../../../samples/snippets/cpp/VS_Snippets_CLR/AppDomain_Setup/CPP/source2.cpp#2)]
 [!code-csharp[AppDomain_Setup#2](../../../samples/snippets/csharp/VS_Snippets_CLR/AppDomain_Setup/CS/source2.cs#2)]
 [!code-vb[AppDomain_Setup#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AppDomain_Setup/VB/source2.vb#2)]  
  
 次の例では、アプリケーション ドメインのセットアップ情報を設定してから取得しています。 `AppDomain.SetupInformation.ApplicationBase` により構成情報が取得されます。  
  
 [!code-cpp[AppDomain_Setup#3](../../../samples/snippets/cpp/VS_Snippets_CLR/AppDomain_Setup/CPP/source3.cpp#3)]
 [!code-csharp[AppDomain_Setup#3](../../../samples/snippets/csharp/VS_Snippets_CLR/AppDomain_Setup/CS/source3.cs#3)]
 [!code-vb[AppDomain_Setup#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AppDomain_Setup/VB/source3.vb#3)]  
  
## <a name="see-also"></a>関連項目

- [アプリケーション ドメインを使用したプログラミング](application-domains.md#programming-with-application-domains)
- [アプリケーション ドメインの使用](use.md)
