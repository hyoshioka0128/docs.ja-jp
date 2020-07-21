---
title: WS-AtomicTransaction の使用
ms.date: 03/30/2017
helpviewer_keywords:
- WS-AT protocol [WCF]
ms.assetid: 04a4c200-0af0-4c5d-a3d9-87cb7339e054
ms.openlocfilehash: 71090efbb096bc3b7b3d6bcf40ff496b78ac6252
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600686"
---
# <a name="using-ws-atomictransaction"></a>WS-AtomicTransaction の使用
WS-AtomicTransaction (WS-AT) は、相互運用が可能なトランザクション プロトコルです。 Web サービス メッセージを使用して分散トランザクションをフローできるようにすると共に、異種のトランザクション インフラストラクチャ間で相互運用できるように調整します。 WS-AT では、2 フェーズ コミット プロトコルを使用して、分散アプリケーション、トランザクション マネージャー、およびリソース マネージャー間でアトミックな結果を実現します。  
  
 WS-AT 実装 Windows Communication Foundation (WCF) には、Microsoft 分散トランザクションコーディネーター (MSDTC) トランザクションマネージャーに組み込まれているプロトコルサービスが含まれています。 WS-AT を使用すると、WCF アプリケーションは、サードパーティのテクノロジを使用して構築された相互運用可能な Web サービスを含む、他のアプリケーションにトランザクションをフローさせることができます。  
  
 クライアント アプリケーションとサーバー アプリケーション間でトランザクションをフローさせるときに使用されるトランザクション プロトコルは、クライアントが選択したエンドポイントでサーバーが公開するバインディングによって決定されます。 WCF システム指定のバインディングの中には、既定では、 `OleTransactions` プロトコルをトランザクションの伝達形式として指定するものと、ws-at を指定するものがあります。 特定のバインディング内部でのトランザクション プロトコルの選択は、プログラムによって変更することもできます。  
  
 プロトコルの選択は、次の内容に影響を与えます。  
  
- トランザクションをクライアントからサーバーにフローさせるために使用されるメッセージ ヘッダーの形式。  
  
- トランザクションの結果を解決するために、クライアントのトランザクション マネージャーとサーバーのトランザクション マネージャーの間で 2 フェーズ コミット プロトコルを実行するために使用されるネットワーク プロトコル。  
  
 サーバーとクライアントが WCF を使用して記述されている場合は、WS-AT を使用する必要はありません。 その代わりに、`NetTcpBinding` プロトコルを使用する `TransactionFlow` 属性を有効にして `OleTransactions` の既定の設定を使用できます。 詳細については、「[\<netTcpBinding>](../../configure-apps/file-schema/wcf/nettcpbinding.md)」を参照してください。 ただし、サードパーティのテクノロジで構築された Web サービスにトランザクションをフローさせる場合は、WS-AT を使用する必要があります。  
  
## <a name="see-also"></a>関連項目

- [WS-AtomicTransaction サポートの構成](configuring-ws-atomic-transaction-support.md)
