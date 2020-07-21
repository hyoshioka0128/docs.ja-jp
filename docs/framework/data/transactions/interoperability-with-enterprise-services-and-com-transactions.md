---
title: Enterprise Services および COM+ トランザクションとの相互運用性
description: System.Transactions 名前空間を利用した、.NET での Enterprise Services および COM+ トランザクションとの相互運用性を理解します。
ms.date: 03/30/2017
ms.assetid: d0fd0d26-fe86-443b-b208-4d57d39fa4aa
ms.openlocfilehash: ebd6166fbd99ef102cf10ba1bcef9e3eb8aaa5da
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141902"
---
# <a name="interoperability-with-enterprise-services-and-com-transactions"></a>Enterprise Services および COM+ トランザクションとの相互運用性
<xref:System.Transactions> 名前空間は、この名前空間を使用して作成されたトランザクション オブジェクトと COM+ によって作成されたトランザクションとの間の相互運用をサポートします。  
  
 新しい <xref:System.Transactions.EnterpriseServicesInteropOption> インスタンスを作成する際に <xref:System.Transactions.TransactionScope> 列挙体を使用すれば、COM+ との相互運用性のレベルを指定することができます。  
  
 既定では、アプリケーション コードによって静的 <xref:System.Transactions.Transaction.Current%2A> プロパティが検査されると、<xref:System.Transactions> によって、その他の場合は最新であるトランザクション、または <xref:System.Transactions.Transaction.Current%2A> が **null** であることを指示する <xref:System.Transactions.TransactionScope> オブジェクトが探されます。 どちらも見つからないと、<xref:System.Transactions> は COM+ コンテキストに照会してトランザクションを探します。 <xref:System.Transactions> は、COM+ コンテキストからトランザクションが見つかる場合でも、<xref:System.Transactions> にネイティブなトランザクションを優先します。  
  
## <a name="interoperability-levels"></a>相互運用性のレベル  
 <xref:System.Transactions.EnterpriseServicesInteropOption> 列挙体は、<xref:System.Transactions.EnterpriseServicesInteropOption.None>、<xref:System.Transactions.EnterpriseServicesInteropOption.Full>、および <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic> の各相互運用性レベルを定義します。  
  
 <xref:System.Transactions.TransactionScope> クラスは、<xref:System.Transactions.EnterpriseServicesInteropOption> をパラメーターとして受け入れるコンストラクターを提供します。  
  
 <xref:System.Transactions.EnterpriseServicesInteropOption.None> は、その名前が示すように、<xref:System.EnterpriseServices> コンテキストとトランザクション スコープの間に相互運用性がないことを意味します。 <xref:System.Transactions.TransactionScope> で <xref:System.Transactions.EnterpriseServicesInteropOption.None> オブジェクトを作成した場合は、その後 <xref:System.Transactions.Transaction.Current%2A> にどのような変更を加えても、その変更が COM+ コンテキストに反映されることはありません。 同様に、COM+ コンテキスト内のトランザクションに対する変更も <xref:System.Transactions.Transaction.Current%2A> には反映されません。 追加の同期は必要ないため、これは <xref:System.Transactions> に対する最速の操作モードです。 <xref:System.Transactions.EnterpriseServicesInteropOption.None> は、<xref:System.Transactions.TransactionScope> をパラメーターとして受け入れないすべてのコンストラクターで、<xref:System.Transactions.EnterpriseServicesInteropOption> よって使用される既定値です。  
  
 <xref:System.EnterpriseServices> トランザクションをアンビエント トランザクションと組み合わせる場合は、<xref:System.Transactions.EnterpriseServicesInteropOption.Full> または <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic> のいずれかを使用する必要があります。 これらの値はいずれもコンポーネントのないサービスと呼ばれる機能に依存するため、これらの値を使用する際には Windows XP Service Pack 2 または Windows Server 2003 が稼働している必要があります。  
  
 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> は、<xref:System.Transactions> と <xref:System.EnterpriseServices> のアンビエント トランザクションが常に同じものであることを指定します。 結果として、新しい <xref:System.EnterpriseServices> トランザクション コンテキストが作成され、そのコンテキストにとって <xref:System.Transactions.TransactionScope> が最新になるようにするため最新のトランザクションが適用されます。 そのため、<xref:System.Transactions.Transaction.Current%2A> のトランザクションは <xref:System.EnterpriseServices.ContextUtil.Transaction%2A> のトランザクションと完全に同期することになります。 この値を使用すると、新しい COM+ コンテキストを作成しなければならない場合があるため、パフォーマンスが低下します。  
  
 <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic> では次の要件が指定されます。  
  
- <xref:System.Transactions.Transaction.Current%2A> が検査されると、<xref:System.Transactions> は、既定のコンテキスト以外のコンテキストで実行されていることを検出した場合、COM+ コンテキスト内のトランザクションをサポートする必要があります。 既定のコンテキストには、トランザクションを含めることができません。 したがって、既定のコンテキストでは、<xref:System.Transactions.EnterpriseServicesInteropOption.Automatic> を使用した場合でも、<xref:System.Transactions> によって使用されるスレッド ローカル ストレージに格納されているトランザクションが <xref:System.Transactions.Transaction.Current%2A> に対して返されます。  
  
- 新しい <xref:System.Transactions.TransactionScope> オブジェクトが作成され、その作成が既定のコンテキスト以外のコンテキストで行われた場合は、<xref:System.Transactions.TransactionScope> オブジェクトにとって最新であるトランザクションが COM+ に反映される必要があります。 この場合、<xref:System.Transactions.EnterpriseServicesInteropOption.Automatic> は、新しい COM+ コンテキストを作成するという点で、<xref:System.Transactions.EnterpriseServicesInteropOption.Full> と同様に動作します。  
  
 さらに、<xref:System.Transactions.Transaction.Current%2A> と <xref:System.Transactions.EnterpriseServicesInteropOption.Full> の両方で <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic> が設定されると、これらのモードはいずれも、<xref:System.Transactions.Transaction.Current%2A> を直接設定できないことを示します。  <xref:System.Transactions.Transaction.Current%2A> を作成する以外に <xref:System.Transactions.TransactionScope> を直接設定しようとすると、<xref:System.InvalidOperationException> が発生します。 <xref:System.Transactions.EnterpriseServicesInteropOption> 列挙値には、使用する値を明示的に指定しない新しいトランザクション スコープが継承されます。 たとえば、新しい <xref:System.Transactions.TransactionScope> オブジェクトを <xref:System.Transactions.EnterpriseServicesInteropOption.Full> で作成した後、2 番目の <xref:System.Transactions.TransactionScope> オブジェクトを作成した場合 (ただし、<xref:System.Transactions.EnterpriseServicesInteropOption> 値を指定しない)、その 2 番目の <xref:System.Transactions.TransactionScope> オブジェクトも <xref:System.Transactions.EnterpriseServicesInteropOption.Full> を持つことになります。  
  
 要約すると、新しいトランザクション スコープを作成するときには次の規則が適用されます。  
  
1. <xref:System.Transactions.Transaction.Current%2A> は、トランザクションがあるかどうかを確認するために検査されます。 この検査の結果、次のことが行われます。  
  
    - スコープがあるかどうかが検査されます。  
  
    - スコープがある場合は、そのスコープが最初に作成されたときに渡された <xref:System.Transactions.EnterpriseServicesInteropOption> 列挙体の値が検査されます。  
  
    - <xref:System.Transactions.EnterpriseServicesInteropOption> 列挙体が <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic> に設定された場合は、COM+ トランザクション (<xref:System.EnterpriseServices> トランザクション) がマネージド スレッド ローカル ストレージ内の <xref:System.Transactions> トランザクションよりも優先されます。  
  
         値が <xref:System.Transactions.EnterpriseServicesInteropOption.None> に設定された場合は、マネージド スレッド ローカル ストレージ内の <xref:System.Transactions> トランザクションが優先されます。  
  
         値が <xref:System.Transactions.EnterpriseServicesInteropOption.Full> の場合は、トランザクションは 1 つだけあり、それは COM+ トランザクションです。  
  
2. <xref:System.Transactions.TransactionScopeOption> コンストラクターによって渡された <xref:System.Transactions.TransactionScope> 列挙体の値が検査されます。 これにより、新しいトランザクションを作成する必要があるかどうかが決定されます。  
  
3. 新しいトランザクションを作成する場合は、<xref:System.Transactions.EnterpriseServicesInteropOption> の値に応じてそれぞれ次のようになります。  
  
    - <xref:System.Transactions.EnterpriseServicesInteropOption.Full>:  COM+ コンテキストに関連付けられたトランザクションが作成されます。  
  
    - <xref:System.Transactions.EnterpriseServicesInteropOption.None>: <xref:System.Transactions> トランザクションが作成されます。  
  
    - <xref:System.Transactions.EnterpriseServicesInteropOption.Automatic>: COM+ コンテキストがある場合は、トランザクションが作成され、コンテキストにアタッチされます。  
  
 次の表は、Enterprise Services (ES) コンテキストと、<xref:System.Transactions.EnterpriseServicesInteropOption> 列挙体を使用するトランザクションを必要とするトランザクション スコープを示しています。  
  
|ES コンテキスト|None|自動|完全|  
|----------------|----------|---------------|----------|  
|既定のコンテキスト|既定のコンテキスト|既定のコンテキスト|新規作成 <br />コンテキストの作成|  
|既定以外のコンテキスト|クライアントのコンテキストの保守|新しいトランザクション コンテキストの作成|新しいトランザクション コンテキストの作成|  
  
 次の表は、特定の <xref:System.EnterpriseServices> コンテキストと、<xref:System.Transactions.EnterpriseServicesInteropOption> 列挙体を使用するトランザクションを必要とするトランザクション スコープがあると、アンビエント トランザクションがどうなるかを示しています。  
  
|ES コンテキスト|None|自動|完全|  
|----------------|----------|---------------|----------|  
|既定のコンテキスト|ST|ST|ES|  
|既定以外のコンテキスト|ST|ES|ES|  
  
 注:  
  
- ST は、スコープのアンビエント トランザクションが <xref:System.Transactions> によって管理され、どの <xref:System.EnterpriseServices> コンテキストのトランザクション (存在する場合) にも関連付けられていないことを示します。  
  
- ES は、スコープのアンビエント トランザクションが <xref:System.EnterpriseServices> コンテキストのトランザクションと同じものであることを示します。
