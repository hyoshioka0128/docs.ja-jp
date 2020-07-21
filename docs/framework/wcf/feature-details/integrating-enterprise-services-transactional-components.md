---
title: エンタープライズ サービスのトランザクション コンポーネントの統合
ms.date: 03/30/2017
ms.assetid: 05dab277-b8b2-48cf-b40c-826be128b175
ms.openlocfilehash: 1c4fabfadb113c79b216fa10ff80b551ba0f9716
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596852"
---
# <a name="integrating-enterprise-services-transactional-components"></a>エンタープライズ サービスのトランザクション コンポーネントの統合

Windows Communication Foundation (WCF) は、エンタープライズサービスと統合するための自動メカニズムを提供します (「 [COM + アプリケーションとの統合](integrating-with-com-plus-applications.md)」を参照してください)。 ただし、柔軟性を高めるために、エンタープライズ サービス内でホストされるトランザクション コンポーネントを内部的に使用するサービスを開発する場合があります。 WCF トランザクション機能はインフラストラクチャ上に構築されているため <xref:System.Transactions> 、Enterprise services と wcf を統合するプロセスは、エンタープライズサービス <xref:System.Transactions> [と com + トランザクションとの相互運用性](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.0/ms229974(v=vs.85))に関する説明にあるとおり、エンタープライズサービス間の相互運用性を指定するためのものと同じです。  
  
 フローされる受信トランザクションと COM+ コンテキスト トランザクションの間に必要なレベルの相互運用性を提供するには、サービス実装で <xref:System.Transactions.TransactionScope> インスタンスを作成し、<xref:System.Transactions.EnterpriseServicesInteropOption> 列挙型の適切な値を使用する必要があります。  
  
## <a name="integrating-enterprise-services-with-a-service-operation"></a>エンタープライズ サービスとサービス操作の統合  
 Allowed トランザクション フローで、<xref:System.Transactions.TransactionScope> オプションを指定して <xref:System.Transactions.EnterpriseServicesInteropOption.Full> を作成する操作を次のコードに示します。 このシナリオでは次の条件が適用されます。  
  
- クライアントがトランザクションをフローする場合、エンタープライズ サービス コンポーネント呼び出しを含む操作は、トランザクションのスコープ内で実行されます。 <xref:System.Transactions.EnterpriseServicesInteropOption.Full> を使用すると、トランザクションが <xref:System.EnterpriseServices> コンテキストと同期することが保証されます。つまり、<xref:System.Transactions> のアンビエント トランザクションと <xref:System.EnterpriseServices> とが同じになります。  
  
- クライアントがトランザクションをフローしない場合、<xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> を `true` に設定すると操作の新しいトランザクション スコープが作成されます。 同様に、<xref:System.Transactions.EnterpriseServicesInteropOption.Full> を使用すると、操作のトランザクションが <xref:System.EnterpriseServices> コンポーネントのコンテキスト内で使用されるトランザクションと同じになることが保証されます。  
  
 任意の追加のメソッド呼び出しも、同じ操作のトランザクションのスコープ内で行われます。  
  
```csharp
[ServiceContract()]  
public interface ICustomerServiceContract  
{  
   [OperationContract]  
   [TransactionFlow(TransactionFlowOption.Allowed)]  
   void UpdateCustomerNameOperation(int customerID, string newCustomerName);  
}  
  
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CustomerService : ICustomerServiceContract  
{  
   [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
   public void UpdateCustomerNameOperation(int customerID, string newCustomerName)  
   {  
   // Create a transaction scope with full ES interop  
      using (TransactionScope ts = new TransactionScope(  
                     TransactionScopeOption.Required,  
                     new TransactionOptions(),  
                     EnterpriseServicesInteropOption.Full))  
      {  
         // Create an Enterprise Services component  
         // Call UpdateCustomer method on an Enterprise Services
         // component
  
         // Call UpdateOtherCustomerData method on an Enterprise
         // Services component
         ts.Complete();  
      }  
  
      // Do UpdateAdditionalData on an non-Enterprise Services  
      // component  
   }  
}  
```  
  
 操作の現在のトランザクションと、エンタープライズ サービスのトランザクション コンポーネント呼び出しとの間の同期が不要な場合は、<xref:System.Transactions.TransactionScope> インスタンスのインスタンス化時に <xref:System.Transactions.EnterpriseServicesInteropOption.None> オプションを使用する必要があります。  
  
## <a name="integrating-enterprise-services-with-a-client"></a>エンタープライズ サービスとクライアントの統合  
 <xref:System.Transactions.TransactionScope> を設定した <xref:System.Transactions.EnterpriseServicesInteropOption.Full> インスタンスを使用するクライアント コードを次のコードに示します。 このシナリオでは、トランザクション フローをサポートするサービス操作の呼び出しが、エンタープライズ サービス コンポーネントへの呼び出しと同じトランザクションのスコープ内で発生します。  
  
```csharp
static void Main()  
{  
    // Create a client  
    CalculatorClient client = new CalculatorClient();  
  
    // Create a transaction scope with full ES interop  
    using (TransactionScope ts = new TransactionScope(  
          TransactionScopeOption.Required,  
          new TransactionOptions(),  
          EnterpriseServicesInteropOption.Full))  
    {  
        // Call Add calculator service operation  
  
        // Create an Enterprise Services component  
  
        // Call UpdateCustomer method on an Enterprise Services
        // component
  
        ts.Complete();  
    }  
  
    // Closing the client gracefully closes the connection and
    // cleans up resources  
    client.Close();  
}  
```  
  
## <a name="see-also"></a>関連項目

- [COM + アプリケーションとの統合](integrating-with-com-plus-applications.md)
- [COM アプリケーションとの統合](integrating-with-com-applications.md)
