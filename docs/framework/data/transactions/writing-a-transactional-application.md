---
title: トランザクション アプリケーションの作成
description: .NET でトランザクション アプリケーションを作成します。 Transaction クラスまたは TransactionScope クラスでそれぞれ、明示的または暗黙的なプログラミング モデルを使用します。
ms.date: 03/30/2017
ms.assetid: a4d891f2-6fc8-4395-93c6-6819492406e0
ms.openlocfilehash: 0235bb507d974e0bd3a7046ea213d8b78d870d59
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85415772"
---
# <a name="writing-a-transactional-application"></a>トランザクション アプリケーションの作成
トランザクション アプリケーションのプログラマは、<xref:System.Transactions> 名前空間に用意されている 2 つのプログラミング モデルを活用して、トランザクションを作成できます。 <xref:System.Transactions.Transaction> クラスを使用した明示的なプログラミング モデルを使用できるほか、<xref:System.Transactions.TransactionScope> クラスを使用して、トランザクションが自動的にインフラストラクチャによって管理される暗黙的なプログラミング モデルも利用できます。 開発では、暗黙的なトランザクション モデルを使用することをお勧めします。 トランザクション スコープの使用方法については、「[トランザクション スコープを使用した暗黙的なトランザクションの実装](implementing-an-implicit-transaction-using-transaction-scope.md)」のトピックを参照してください。  
  
 両モデルとも、プログラムが整合性の取れた状態に達した時点で、トランザクションのコミットをサポートします。 コミットが成功すると、トランザクションは永続的にコミットされます。 コミットが失敗すると、トランザクションは中止されます。 アプリケーション プログラムがトランザクションを完了できない場合は、トランザクションを中止してその処理内容を取り消すことを試みます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
### <a name="creating-a-transaction"></a>トランザクションの作成  
 <xref:System.Transactions> 名前空間には、トランザクションを作成する 2 つのモデルが用意されています。 これらのモデルは、以下のトピックで取り上げられています。  
  
 [トランザクション スコープを使用した暗黙的なトランザクションの実装](implementing-an-implicit-transaction-using-transaction-scope.md)  
  
 <xref:System.Transactions> 名前空間がサポートする、<xref:System.Transactions.TransactionScope> クラスを使用した暗黙的なトランザクションの作成について説明します。  
  
 [CommittableTransaction を使用した明示的なトランザクションの実装](implementing-an-explicit-transaction-using-committabletransaction.md)  
  
 <xref:System.Transactions> 名前空間がサポートする、<xref:System.Transactions.CommittableTransaction> クラスを使用した明示的なトランザクションの作成について説明します。  
  
### <a name="escalating-transaction-management"></a>トランザクション管理のエスカレート  
 トランザクションが別のアプリケーション ドメインにあるリソースにアクセスする必要がある場合、または別の永続的なリソース マネージャーに参加する場合は、トランザクションが MSDTC によって管理されるよう自動的にエスカレートされます。 トランザクションのエスカレーションの詳細については、「[トランザクション管理のエスカレーション](transaction-management-escalation.md)」のトピックを参照してください。  
  
### <a name="concurrency"></a>コンカレンシー  
 「[DependentTransaction によるコンカレンシーの管理](managing-concurrency-with-dependenttransaction.md)」のトピックでは、<xref:System.Transactions.DependentTransaction> クラスを使用して、非同期タスク間でコンカレンシーを実現する方法について説明します。  
  
### <a name="com-interop"></a>COM+ 相互運用  
 「[Enterprise Services および COM+ トランザクションとの相互運用性](interoperability-with-enterprise-services-and-com-transactions.md)」のトピックでは、分散トランザクションを COM+ トランザクションと連係させる方法について説明します。  
  
### <a name="diagnostics"></a>診断  
 「[診断トレース](diagnostic-traces.md)」では、<xref:System.Transactions> インフラストラクチャによって生成されるトレース コードを使用して、アプリケーションのエラーのトラブルシューティングを行う方法について説明します。  
  
### <a name="working-within-aspnet"></a>ASP.NET 内での使用  
 「[ASP.NET での System.Transactions の使用](using-system-transactions-in-aspnet.md)」のトピックでは、ASP.NET アプリケーション内で <xref:System.Transactions> を正しく使用する方法について説明します。
