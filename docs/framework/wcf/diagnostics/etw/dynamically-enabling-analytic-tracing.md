---
title: 分析トレースの動的な有効化
ms.date: 03/30/2017
ms.assetid: 58b63cfc-307a-427d-b69d-9917ff9f44ac
ms.openlocfilehash: 22d122f802e82c2aa04d72a996cb872e06fcaeaa
ms.sourcegitcommit: 515469828d0f040e01bde01df6b8e4eb43630b06
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78674954"
---
# <a name="dynamically-enabling-analytic-tracing"></a>分析トレースの動的な有効化
Windows オペレーティング システムに付属のツールでは、ETW (Event Tracing for Windows) を使用して、トレースを動的に有効化または無効化できます。 すべての[!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)]Wcf サービスでは、アプリケーションの Web.config ファイルを変更したり、サービスを再起動したりすることなく、分析トレースを動的に有効または無効にできます。 このため、トレース イベントを生成するアプリケーションに影響が生じません。  
  
 WCF トレース オプションは、同様の方法で構成できます。 たとえば、アプリケーションに影響を与えずに、重大度レベルを **Error** から **Information** に変更できます。 これは、次のツールで実行できます。  
  
- **Logman** : トレース データを構成、制御、および照会するためのコマンド ライン ツールです。 詳細については、「 [Logman のトレースの作成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc788036(v=ws.10))」および「[ログマン更新トレース](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc788128(v=ws.10))」を参照してください。  
  
- **EventViewer** : トレース結果を表示するための、Windows のグラフィカル管理ツールです。 詳細については、「 [WCF サービスと Windows およびイベント ビューアーのイベント トレース](../../samples/wcf-services-and-event-tracing-for-windows.md)」を参照[してください](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc766042(v=ws.11))。  
  
- **Perfmon** : カウンターを使用して、トレース カウンターおよびパフォーマンス トレースの効果を監視する、Windows のグラフィカル管理ツールです。 詳細については、「[データ コレクター セットを手動で作成する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc766404(v=ws.11))」を参照してください。  
  
### <a name="keywords"></a>Keywords  
 <xref:System.ServiceModel.Activation.Configuration.ServiceModelActivationSectionGroup.Diagnostics%2A> クラスを使用するときには、通常、.NET Framework トレース メッセージが重大度レベル (エラー、警告、情報など) でフィルターされます。 ETW は、重大度レベルの概念をサポートしますが、キーワードを使用して、新しい柔軟なフィルター機構も追加されています。 キーワードは任意のテキスト値で、これによって、トレース イベントでそのイベントの意味に関する追加のコンテキストが提供されます。  
  
 WCF 分析トレースでは、各トレース イベントには 2 種類のキーワードがあります。 まず、各イベントには 1 つ以上のシナリオ キーワードがあります。 これらのキーワードは、そのイベントがサポートするシナリオを示します。 次の表に示すように、特定の目的に対応する 3 つのシナリオ キーワードがあります。 キーワードを使用したフィルター処理は、WCF サービスを妨害することなく動的に変更できます。 このため、現在のトレース シナリオおよび収集するトレース情報の量を動的に変更できます。 たとえば、 `HealthMonitoring` を `Troubleshooting` に変更し、トレース イベントの詳細度を上げることができます。  
  
|Keyword|説明|  
|-------------|-----------------|  
|`HealthMonitoring`|サービスのアクティビティを監視できる、軽量の、最小限のトレース。|  
|`EndToEndMonitoring`|メッセージ フロー トレースのサポートに使用するイベント。|  
|`Troubleshooting`|WCF の拡張ポイントを中心に、より詳細なイベント。|  
  
 キーワードの 2 番目のグループは、.NET Framework のどのコンポーネントがイベントを生成するかを定義します。  
  
|Keyword|説明|  
|-------------|-----------------|  
|`UserEvents`|ユーザー コードによって生成され、.NET Framework ではなく、イベントが生成されます。|  
|`ServiceModel`|WCF ランタイムによって生成されるイベント。|  
|`ServiceHost`|サービス ホストが生成するイベント。|  
|`WCFMessageLogging`|WCF メッセージ ログ イベント。|  
  
## <a name="see-also"></a>関連項目

- [WCF サービスと Event Tracing for Windows](../../samples/wcf-services-and-event-tracing-for-windows.md)
