---
title: 接続の管理
description: データ リソースに HTTP を使用するアプリケーションで、ServicePoint および ServicePointManager クラスを使用して接続を管理できるしくみについて説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Internet, connections
- HTTP, classes for connecting
- requesting data from Internet, connections
- sending data, connections
- receiving data, connections
- ServicePoint class, about ServicePoint class
- response to Internet request, connections
- connections [.NET Framework], classes
- network resources, connections
- downloading Internet resources, connections
- ServicePointManager class, about ServicePointManager class
ms.assetid: 9b3d3de7-189f-4f7d-81ae-9c29c441aaaa
ms.openlocfilehash: 124dff1b104e323b929d13f73cf17d740e747c32
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502289"
---
# <a name="managing-connections"></a>接続の管理
HTTP を使用してデータ リソースに接続するアプリケーションは、.NET Framework の <xref:System.Net.ServicePoint> クラスと <xref:System.Net.ServicePointManager> クラスを使用してインターネットに対する接続を管理し、最適なスケールとパフォーマンスを達成することができます。  
  
 **ServicePoint** クラスは、アプリケーションがインターネット リソースにアクセスするときに、接続に使用できるエンドポイントを提供します。 各 **ServicePoint** には、接続間で最適化情報を共有してパフォーマンスを改善することで、インターネット サーバーとの接続を最適化できる情報が含まれています。  
  
 各 **ServicePoint** は、Uniform Resource Identifier (URI) で識別され、URI のスキーム識別子とホスト フラグメントに従って分類されます。 たとえば、スキーム識別子 (http) とホスト フラグメント (`www.contoso.com`) が同じであるため、1 つの **ServicePoint** インスタンスから URI `http://www.contoso.com/index.htm` と `http://www.contoso.com/news.htm?date=today` に対して要求が提供されます。 サーバー `www.contoso.com` に対する永続的な接続が既にあるアプリケーションの場合は、その接続を使用して両方の要求が取得され、2 つの接続を作成しなくても済むようにします。  
  
 **ServicePointManager** は、**ServicePoint** インスタンスの作成と破棄を管理する静的クラスです。 既存の **ServicePoint** インスタンスのコレクション内にないインターネット リソースをアプリケーションから要求された場合、**ServicePointManager** によって **ServicePoint** が作成されます。 最大アイドル時間を超えた場合、または既存の **ServicePoint** インスタンスがアプリケーションの最大 **ServicePoint** インスタンス数を超えた場合、**ServicePoint** インスタンスは破棄されます。 既定の最大アイドル時間と最大 **ServicePoint** インスタンス数はいずれも、**ServicePointManager** で <xref:System.Net.ServicePointManager.MaxServicePointIdleTime%2A> プロパティと <xref:System.Net.ServicePointManager.MaxServicePoints%2A> プロパティを設定して制御できます。  
  
 クライアントとサーバー間の接続数は、アプリケーションのスループットに大きな影響を及ぼす可能性があります。 既定で、<xref:System.Net.HttpWebRequest> クラスを使用するアプリケーションは、特定のサーバーに対して最大で 2 つの永続的な接続を使用しますが、最大接続数はアプリケーションごとに設定できます。  
  
> [!NOTE]
> HTTP/1.1 仕様では、アプリケーションからの接続数をサーバーごとに 2 接続に制限しています。  
  
 最適な接続数は、アプリケーションが実行されている実際の条件によって変わります。 アプリケーションに使用できる接続数を増やしても、アプリケーションのパフォーマンスに影響しない可能性があります。 接続数を増やした場合の影響を判断するには、接続数を変えながらパフォーマンス テストを実行します。 アプリケーションが使用する接続数を変更するには、次のコード例のように、アプリケーションの初期化時に **ServicePointManager** クラスの静的な <xref:System.Net.ServicePointManager.DefaultConnectionLimit%2A> プロパティを変更します。  
  
```csharp  
// Set the maximum number of connections per server to 4.  
ServicePointManager.DefaultConnectionLimit = 4;  
```  
  
```vb  
' Set the maximum number of connections per server to 4.  
ServicePointManager.DefaultConnectionLimit = 4  
```  
  
 **ServicePointManager.DefaultConnectionLimit** プロパティを変更しても、既に初期化されている **ServicePoint** インスタンスに影響はありません。 次のコードは、サーバー `http://www.contoso.com` の既存の **ServicePoint** の接続制限を、`newLimit` に保存されている値に変更する例を示しています。  
  
```csharp  
Uri uri = new Uri("http://www.contoso.com/");  
ServicePoint sp = ServicePointManager.FindServicePoint(uri);  
sp.ConnectionLimit = newLimit;  
```  
  
```vb  
Dim uri As New Uri("http://www.contoso.com/")  
Dim sp As ServicePoint = ServicePointManager.FindServicePoint(uri)  
sp.ConnectionLimit = newLimit  
```  
  
## <a name="see-also"></a>関連項目

- [接続のグループ化](connection-grouping.md)
- [アプリケーション プロトコルの使用](using-application-protocols.md)
