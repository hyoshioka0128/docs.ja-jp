---
title: 一方向サービス
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Communication Foundation [WCF], one-way service contracts
- WCF [WCF], one-way service contracts
- service contracts [WCF], defining one-way
ms.assetid: 19053a36-4492-45a3-bfe6-0365ee0205a3
ms.openlocfilehash: 0d69af40e4b9a0133e44b64b45466f9aac84ffe2
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598750"
---
# <a name="one-way-services"></a>一方向サービス
サービス操作の既定の動作は、要求/応答パターンです。 要求/応答パターンでは、サービス操作がコードで `void` 型のメソッドとして表される場合であっても、クライアントは応答メッセージを待機します。 一方向操作では、メッセージが 1 つ送信されるだけです。 受信者は応答メッセージを送信せず、送信者もこれを待機しません。  
  
 一方向デザイン パターンは次の場合に使用します。  
  
- クライアントが操作を呼び出す必要があり、操作レベルで操作の結果に影響を受けない場合。  
  
- <xref:System.ServiceModel.NetMsmqBinding> クラスまたは <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> クラスを使用している場合  (このシナリオの詳細については、「 [WCF のキュー](queues-in-wcf.md)」を参照してください)。  
  
 操作が一方向の場合、エラー情報をクライアントに伝達する応答メッセージはありません。 エラー状態を検出するには、信頼できるセッションのような基になるバインディングの機能を使用できます。また、2 つの一方向操作 (1 つは、サービス操作を呼び出すための、クライアントからサービスへの一方向コントラクト、もう 1 つは、クライアントが実装するコールバックを使用してサービスがエラーを返せるようにする、サービスとクライアントの間の一方向コントラクト) を使用する双方向サービス コントラクトをデザインすることもできます。  
  
 一方向サービス コントラクトを作成するには、サービス コントラクトを定義し、<xref:System.ServiceModel.OperationContractAttribute> クラスを各操作に適用し、<xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> プロパティを `true` に設定します。次のコードを参照してください。  
  
```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOneWayCalculator  
{  
    [OperationContract(IsOneWay=true)]  
    void Add(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Subtract(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Multiply(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Divide(double n1, double n2);  
}  
```  
  
 完全な例については、[一方向](../samples/one-way.md)のサンプルを参照してください。  
  
## <a name="clients-blocking-with-one-way-operations"></a>一方向操作でのクライアントのブロック  
 一部の一方向アプリケーションは、送信データがネットワーク接続に書き込まれるとすぐに戻りますが、いくつかのシナリオでは、バインディングまたはサービスの実装によって、WCF クライアントが一方向の操作を使用してブロックされる可能性があることに注意してください。 WCF クライアントアプリケーションでは、送信データがネットワーク接続に書き込まれるまで、WCF クライアントオブジェクトは返されません。 これは一方向操作を含め、すべてのメッセージ交換パターンについて当てはまることで、トランスポートへのデータの書き込みに何らかの問題があると、クライアントが処理を終了できなくなることを意味します。 問題の種類によっては、例外が発生したりサービスへのメッセージの送信に遅延が発生したりする結果となることがあります。  
  
 たとえば、トランスポートがエンドポイントを見つけられない場合、大きな遅延なしに <xref:System.ServiceModel.EndpointNotFoundException?displayProperty=nameWithType> 例外がスローされます。 ただし、サービスが何らかの理由によりデータをネットワークから読み込めないために、クライアントのトランスポート送信操作が終了しない可能性もあります。 このような場合、クライアントのトランスポート バインディングで <xref:System.ServiceModel.Channels.Binding.SendTimeout%2A?displayProperty=nameWithType> 期間が経過すると、<xref:System.TimeoutException?displayProperty=nameWithType> がスローされますが、タイムアウト時間が経過するまで例外はスローされません。 またサービスに多数のメッセージが集中しているために、一定の期間が経過するまでサービスがメッセージを処理できないことがあります。 この場合も、サービスがメッセージを処理できるまで、または例外がスローされるまで、一方向クライアントはブロックします。  
  
 さらに別の状況として、サービスの <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=nameWithType> プロパティが <xref:System.ServiceModel.ConcurrencyMode.Single> に設定されているのに、バインディングが複数のセッションを使用する場合があります。 この場合、ディスパッチャーにより受信メッセージの並び替え (セッションの要件) が強制され、サービスがそのセッションの以前のメッセージの処理を終えるまで、後続のメッセージはネットワークから読み込まれません。 この場合も、クライアントはブロックしますが、例外が発生するかどうかは、サービスがこのクライアントで設定されているタイムアウト期間が経過する前に、待機中のデータを処理できるかどうかによって異なります。  
  
 この問題を軽減するには、クライアント オブジェクトとクライアントのトランスポート送信操作との間にバッファーを挿入します。 たとえば、非同期呼び出しまたはメモリ内メッセージ キューを使用すると、クライアント オブジェクトの処理を短時間で終了できます。 どちらのアプローチでも機能性は向上しますが、スレッド プールとメッセージ キューのサイズによる制限は残ります。  
  
 代わりに、クライアントおよびサービスの各種コントロールを調べてアプリケーション シナリオをテストし、最適な構成がどちら側にあるのかを判断することをお勧めします。 たとえば、セッションの使用によりサービスでのメッセージの処理がブロックされている場合、<xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> プロパティを <xref:System.ServiceModel.InstanceContextMode.PerCall> に設定することによって、異なるサービス インスタンスによって各メッセージが処理されるようにし、また <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> を <xref:System.ServiceModel.ConcurrencyMode.Multiple> に設定することによって、複数のスレッドで同時にメッセージをディスパッチできるようにします。 また、別のアプローチとして、サービスとクライアント バインディングの読み取りクォータを増やすという方法もあります。  
  
## <a name="see-also"></a>関連項目

- [一方向](../samples/one-way.md)
