---
title: トランザクション アプリケーションの診断
ms.date: 03/30/2017
ms.assetid: 4a993492-1088-4d10-871b-0c09916af05f
ms.openlocfilehash: fb3a83083e876cf697621ba70dcf7dd67636f83a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599218"
---
# <a name="diagnosing-transactional-applications"></a>トランザクション アプリケーションの診断
このトピックでは、Windows Communication Foundation (WCF) の管理と診断の機能を使用して、トランザクションアプリケーションのトラブルシューティングを行う方法について説明します。  
  
## <a name="performance-counters"></a>パフォーマンス カウンター  
 WCF には、トランザクションアプリケーションのパフォーマンスを測定するための、標準のパフォーマンスカウンターのセットが用意されています。 詳細については、「[パフォーマンスカウンター](../diagnostics/performance-counters/index.md)」を参照してください。  
  
 パフォーマンス カウンターには次の表に示すように、サービス、エンドポイント、操作の 3 つのレベルがあります。  
  
### <a name="service-performance-counters"></a>サービス パフォーマンス カウンター  
  
|パフォーマンス カウンター|説明|  
|-------------------------|-----------------|  
|トランザクション フロー|このサービスで操作に対して実行されたトランザクションの数です。 このカウンターは、サービスに送信されたメッセージにトランザクションがある場合は常にインクリメントされます。|  
|1 秒あたりのトランザクション フロー|このサービスの操作に対して実行された 1 秒あたりのトランザクションの数です。 このカウンターは、サービスに送信されたメッセージにトランザクションがある場合は常にインクリメントされます。|  
|コミットされたトランザクション操作|このサービスで、結果がコミットされた状態で完了したトランザクション操作の数です。 そのような操作中に実行された作業は完全にコミットされました。 リソースは、操作で実行された作業に応じて更新されます。|  
|1 秒あたりのコミットされたトランザクション操作|このサービスで、結果がコミットされた状態で完了したトランザクション操作の 1 秒あたりの数です。 そのような操作中に実行された作業は完全にコミットされました。 リソースは、操作で実行された作業に応じて更新されます。|  
|中止されたトランザクション操作|このサービスで、結果が中止された状態で完了したトランザクション操作の数です。 そのような操作中に実行された作業はロールバックされました。 リソースは、それぞれの直前の状態に復元されました。|  
|1 秒あたりの中止されたトランザクション操作|このサービスで、結果が中止された状態で完了したトランザクション操作の 1 秒あたりの数です。 そのような操作中に実行された作業はロールバックされました。 リソースは、それぞれの直前の状態に復元されました。|  
|不明なトランザクション操作|このサービスで、結果が不明な状態で完了したトランザクション操作の数です。 結果が不明な作業は中間状態になります。 リソースは、保留中となります。|  
|1 秒あたりの不明なトランザクション操作|このサービスで、結果が不明な状態で完了したトランザクション操作の 1 秒あたりの数です。 結果が不明な作業は中間状態になります。 リソースは、保留中となります。|  
  
### <a name="endpoint-performance-counters"></a>エンドポイントのパフォーマンス カウンター  
  
|パフォーマンス カウンター|説明|  
|-------------------------|-----------------|  
|トランザクション フロー|このエンドポイントでの操作に対して実行されたトランザクションの数。 このカウンターは、エンドポイントに送信されたメッセージにトランザクションがある場合は常にインクリメントされます。|  
|1 秒あたりのトランザクション フロー|毎秒ごとにこのエンドポイントでの操作に対して実行されたトランザクションの数。 このカウンターは、エンドポイントに送信されたメッセージにトランザクションがある場合は常にインクリメントされます。|  
  
### <a name="operation-performance-counters"></a>操作パフォーマンス カウンター  
  
|パフォーマンス カウンター|説明|  
|-------------------------|-----------------|  
|トランザクション フロー|このエンドポイントでの操作に対して実行されたトランザクションの数。 このカウンターは、エンドポイントに送信されたメッセージにトランザクションがある場合は常にインクリメントされます。|  
|1 秒あたりのトランザクション フロー|毎秒ごとにこのエンドポイントでの操作に対して実行されたトランザクションの数。 このカウンターは、エンドポイントに送信されたメッセージにトランザクションがある場合は常にインクリメントされます。|  
  
## <a name="windows-management-instrumentation"></a>Windows Management Instrumentation  
 WCF は、実行時に WCF Windows Management Instrumentation (WMI) プロバイダーを介してサービスの検査データを公開します。 WMI データへのアクセスの詳細については、「[診断のための Windows Management Instrumentation の使用](../diagnostics/wmi/index.md)」を参照してください。  
  
 WMI プロパティには、サービスに適用されるトランザクション設定を示す読み取り専用のプロパティが多数あります。 次の表にこれらの設定をすべて示します。  
  
 サービスの `ServiceBehaviorAttribute` には、次のプロパティがあります。  
  
|名前|Type|Description|  
|----------|----------|-----------------|  
|ReleaseServiceInstanceOnTransactionComplete|Boolean|現在のトランザクションの完了時に、サービス オブジェクトをリサイクルするかどうかを指定します。|  
|TransactionAutoCompleteOnSessionClose|Boolean|現在のセッションの終了時に、保留中のトランザクションを完了するかどうかを指定します。|  
|TransactionIsolationLevel|<xref:System.Transactions.IsolationLevel> 列挙体の有効な値を含む文字列。|このサービスがサポートするトランザクションの分離レベルを指定します。|  
|TransactionTimeout|<xref:System.DateTime>|トランザクションを完了しなければならない期間を指定します。|  
  
 `ServiceTimeoutsBehavior` には、次のプロパティがあります。  
  
|名前|Type|Description|  
|----------|----------|-----------------|  
|TransactionTimeout|<xref:System.DateTime>|トランザクションを完了しなければならない期間を指定します。|  
  
 バインディングの `TransactionFlowBindingElement` には、次のプロパティがあります。  
  
|名前|Type|Description|  
|----------|----------|-----------------|  
|TransactionProtocol|<xref:System.ServiceModel.TransactionProtocol> 型の有効な値を含む文字列。|トランザクションをフローさせるために使用するトランザクション プロトコルを指定します。|  
|TransactionFlow|Boolean|受信トランザクション フローを有効にするかどうかを指定します。|  
  
 操作の `OperationBehaviorAttribute` には、次のプロパティがあります。  
  
|名前|Type|Description|  
|----------|----------|-----------------|  
|TransactionAutoComplete|Boolean|未処理の例外が発生しなかった場合に、現在のトランザクションを自動的にコミットするかどうかを指定します。|  
|TransactionScopeRequired|Boolean|操作がトランザクションを必要とするかどうかを指定します。|  
  
 操作の `TransactionFlowAttribute` には、次のプロパティがあります。  
  
|名前|Type|説明|  
|----------|----------|-----------------|  
|TransactionFlowOption|<xref:System.ServiceModel.TransactionFlowOption> 列挙体の有効な値を含む文字列。|トランザクション フローが要求される範囲を指定します。|  
  
## <a name="tracing"></a>トレース  
 トレースを使用すると、トランザクション アプリケーションにおけるエラーを監視および分析できます。 トレースは次の方法を使用して有効にできます。  
  
- 標準 WCF トレース  
  
     この種類のトレースは、WCF アプリケーションのトレースと同じです。 詳細については、「 [Configuring Tracing](../diagnostics/tracing/configuring-tracing.md)」を参照してください。  
  
- WS-AtomicTransaction トレース  
  
     Ws-atomictransaction のトレースは、ws-atomictransaction[構成ユーティリティ (wsatConfig .exe)](../ws-atomictransaction-configuration-utility-wsatconfig-exe.md)を使用して有効にすることができます。 このトレースでは、トランザクションの状態とシステム内の参加要素を把握できます。 内部のサービス モデル トレースも有効にするには、`HKLM\SOFTWARE\Microsoft\WSAT\3.0\ServiceModelDiagnosticTracing` レジストリ キーを <xref:System.Diagnostics.SourceLevels> 列挙体の有効な値に設定します。 メッセージログは、他の WCF アプリケーションと同じ方法で有効にすることができます。  
  
- `System.Transactions` トレース  
  
     OleTransactions プロトコルを使用する場合、プロトコル メッセージはトレースできません。 <xref:System.Transactions> インフラストラクチャではトレースがサポートされるため (OleTransactions を使用)、ユーザーはトランザクションで発生したイベントを確認できます。 <xref:System.Transactions> アプリケーションのトレースを有効にするには、`App.config` 構成ファイルに次のコードを含めます。  
  
    ```xml  
    <configuration>  
      <system.diagnostics>  
         <sources>  
            <source name="System.Transactions" switchValue="Verbose, ActivityTracing">  
               <listeners>  
                  <add name="Text"  
                     type="System.Diagnostics.XmlWriterTraceListener"  
                     initializeData="SysTx.log"  
                     traceOutputOptions="Callstack" />  
               </listeners>  
            </source>  
         </sources>  
         <trace autoflush="true" indentsize="4">  
         </trace>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
     また、wcf でもインフラストラクチャを利用するため、WCF トレースが有効になり <xref:System.Transactions> ます。  
  
## <a name="see-also"></a>関連項目

- [管理と診断](../diagnostics/index.md)
- [トレースの構成](../diagnostics/tracing/configuring-tracing.md)
- [WS-AtomicTransaction 構成ユーティリティ (wsatConfig.exe)](../ws-atomictransaction-configuration-utility-wsatconfig-exe.md)
