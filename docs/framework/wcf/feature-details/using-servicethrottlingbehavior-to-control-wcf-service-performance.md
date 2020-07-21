---
title: WCF サービス パフォーマンスを制御するための ServiceThrottlingBehavior の使用
ms.date: 03/30/2017
helpviewer_keywords:
- behavior [WCF], service performance
ms.assetid: f9dc120c-dc24-49d5-930e-b22f5bc73423
ms.openlocfilehash: 9cc5141805504bc46391105f475860b032f12d32
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600232"
---
# <a name="using-servicethrottlingbehavior-to-control-wcf-service-performance"></a>WCF サービス パフォーマンスを制御するための ServiceThrottlingBehavior の使用
<xref:System.ServiceModel.Description.ServiceThrottlingBehavior> クラスでは、アプリケーション レベルで作成されるインスタンス数またはセッション数の制限に使用できるプロパティが公開されています。 この動作を使用すると、Windows Communication Foundation (WCF) アプリケーションのパフォーマンスを微調整できます。  
  
## <a name="controlling-service-instances-and-concurrent-calls"></a>サービス インスタンスと同時呼び出しの制御  
 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> プロパティを使用して、<xref:System.ServiceModel.ServiceHost> クラスでアクティブに処理されるメッセージの最大数を指定します。また、<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> プロパティを使用して、サービス内の <xref:System.ServiceModel.InstanceContext> オブジェクトの最大数を指定します。  
  
 これらのプロパティの設定は通常、ロードに対してアプリケーションを実行する実際のエクスペリエンスの後に決定されるため、プロパティの設定 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior> は、通常、要素を使用してアプリケーション構成ファイルで指定され [\<serviceThrottling>](../../configure-apps/file-schema/wcf/servicethrottling.md) ます。  
  
 簡単な例として、<xref:System.ServiceModel.Description.ServiceThrottlingBehavior>、<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentSessions%2A>、および <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A> の各プロパティを 1 に設定するアプリケーション構成ファイルから <xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> クラスを使用する方法を次のコード例に示します。 特定のアプリケーションでの最適な設定については、実際の動作から判断します。  
  
 [!code-xml[ServiceThrottlingBehavior#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/servicethrottlingbehavior/cs/hostapplication.exe.config#3)]  
  
 実行時における正確な動作は <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> プロパティと <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> プロパティの値により異なります。この値により、操作内で一度に実行できるメッセージ数や、受信チャネル セッションに関連するサービス <xref:System.ServiceModel.InstanceContext> の有効期間をそれぞれ制限します。  
  
 詳細については、「<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentCalls%2A>」および「<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A>」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>
- <xref:System.ServiceModel.NetTcpBinding.MaxConnections%2A>
