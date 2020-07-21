---
title: サービスとトランザクション
ms.date: 03/30/2017
helpviewer_keywords:
- service contracts [WCF], designing services and transactions
ms.assetid: 864813ff-2709-4376-912d-f5c8d318c460
ms.openlocfilehash: 4c59b83448f5a2c448843c12dae99c442441441f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79143279"
---
# <a name="services-and-transactions"></a>サービスとトランザクション
Windows 通信基盤 (WCF) アプリケーションは、クライアント内からトランザクションを開始し、サービス操作内でトランザクションを調整できます。 クライアントはトランザクションを開始し、複数のサービス操作を呼び出す可能性があります。サービス操作が、1 つの単位としてコミットまたはロールバックされます。  
  
 サービス コントラクトでトランザクション動作を有効にするには、<xref:System.ServiceModel.ServiceBehaviorAttribute> を指定し、クライアント トランザクションを必要とするサービス操作について <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> プロパティと <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> プロパティを設定します。 <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> パラメーターは、未処理の例外がスローされなかった場合に、メソッドが実行されているトランザクションが自動的に完了されるかどうかを指定します。 これらの属性の詳細については、「[サービスモデル トランザクション属性](./feature-details/servicemodel-transaction-attributes.md)」を参照してください。  
  
 データベース更新の記録など、サービス操作で実行され、リソース マネージャーで管理される作業は、クライアント トランザクションの一部です。  
  
 <xref:System.ServiceModel.ServiceBehaviorAttribute> 属性と <xref:System.ServiceModel.OperationBehaviorAttribute> 属性を使用して、サービス側のトランザクション動作を制御する方法を次の例に示します。  
  
```csharp
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CalculatorService: ICalculatorLog  
{  
    [OperationBehavior(TransactionScopeRequired = true,  
                           TransactionAutoComplete = true)]  
    public double Add(double n1, double n2)  
    {  
        recordToLog($"Added {n1} to {n2}");
        return n1 + n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,
                               TransactionAutoComplete = true)]  
    public double Subtract(double n1, double n2)  
    {  
        recordToLog($"Subtracted {n1} from {n2}");
        return n1 - n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,
                                       TransactionAutoComplete = true)]  
    public double Multiply(double n1, double n2)  
    {  
        recordToLog($"Multiplied {n1} by {n2}");
        return n1 * n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,
                                       TransactionAutoComplete = true)]  
    public double Divide(double n1, double n2)  
    {  
        recordToLog($"Divided {n1} by {n2}", n1, n2);
        return n1 / n2;  
    }  
  
}  
```  
  
 トランザクションとトランザクション フローを有効にするには、WS-AtomicTransaction プロトコルを使用するようにクライアントとサービスのバインディングを構成し、次`true`の[\<](../configure-apps/file-schema/wcf/transactionflow.md)サンプル構成に示すように、transactionFlow>要素を に設定します。  
  
```xml  
<client>  
    <endpoint address="net.tcp://localhost/ServiceModelSamples/service"
          binding="netTcpBinding"
          bindingConfiguration="netTcpBindingWSAT"
          contract="Microsoft.ServiceModel.Samples.ICalculatorLog" />  
</client>  
  
<bindings>  
    <netTcpBinding>  
        <binding name="netTcpBindingWSAT"  
                transactionFlow="true"  
                transactionProtocol="WSAtomicTransactionOctober2004" />  
     </netTcpBinding>  
</bindings>  
```  
  
 クライアントは、<xref:System.Transactions.TransactionScope> を作成し、トランザクションのスコープ内でサービス操作を呼び出すことにより、トランザクションを開始できます。  
  
```csharp
using (TransactionScope ts = new TransactionScope(TransactionScopeOption.RequiresNew))  
{  
    //Do work here  
    ts.Complete();  
}  
```  
  
## <a name="see-also"></a>関連項目

- [System.ServiceModel でのトランザクション サポート](./feature-details/transactional-support-in-system-servicemodel.md)
- [トランザクション モデル](./feature-details/transaction-models.md)
- [WS トランザクション フロー](./samples/ws-transaction-flow.md)
