---
title: 分析トレースの概要
ms.date: 03/30/2017
helpviewer_keywords:
- analytic tracing [WCF], overview
ms.assetid: ae55e9cc-0809-442f-921f-d644290ebf15
ms.openlocfilehash: f6ffed3d9f0bf5e3dc5698d51276eb1db276993c
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74837494"
---
# <a name="analytic-tracing-overview"></a>分析トレースの概要
[!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)] の分析トレースは、Event Tracing for Windows (ETW) を基盤とするトレース機能のセットです。詳細度は低いのですが、パフォーマンスに優れています。 ETW は、カーネル レベルで実行され、トレース操作のオーバーヘッドを大幅に削減します。 ユーザー モードおよびカーネル モードのイベントを効率よくバッファーし、サービスの再起動を必要とすることなく、動的にログを有効化できます。 トレース データは、生成および受信されると、イベント ログから確認できます。  
  
 ETW の詳細については、「 [etw を使用したデバッグとパフォーマンスチューニングの向上](https://go.microsoft.com/fwlink/?LinkId=164781)」を参照してください。  
  
 Windows システム、セキュリティ、およびアプリケーションのイベントログを使用してアプリケーションを分析するだけでなく、Windows Vista および [!INCLUDE[lserver](../../../../../includes/lserver-md.md)] では、[アプリケーションとサービスログ] トップレベルノードに追加のログが導入されました。 これらの新しいログは、システム全体に影響するグローバルなイベント (セキュリティ イベント ログで記録されるようなイベントなど) ではなく、特定のアプリケーションやコンポーネントのイベントを格納することを目的としています。 [!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] は、WCF トレースイベント、WCF メッセージログ、および [!INCLUDE[wf1](../../../../../includes/wf1-md.md)] 追跡レコードのログ記録を、アプリケーションとサービスログに統合して関連付けます。  
  
## <a name="concepts-and-capabilities"></a>概念と機能  
 WCF 分析トレースには、次の概念と機能が適用されます。  
  
### <a name="enabling-wcf-diagnostics-settings"></a>WCF 診断設定の有効化  
 WCF 診断は \<System.servicemodel >\<diagnostics > 構成セクション内で有効になっています。  
  
```xml  
<system.serviceModel>  
  <diagnostics>  
```  
  
 Web でホストされる IIS 仮想アプリケーションの WCF 診断の設定は、アプリケーションの Web.config ファイルで有効にします。 または、アプリケーション内のサブディレクトリに Web.config を作成することもできます。  この方法では、設定がサブディレクトリ内のすべてのサービスに適用されます。  診断設定が、アプリケーション内のすべてのサービスに対して一貫して初期化されるようにするには、これらの設定を、アプリケーション内の個別のサブディレクトリの 1 つではなく、アプリケーション ディレクトリ内の Web.config に含める必要があります。  
  
### <a name="channels"></a>チャネル  
 ETW の場合、ソフトウェア コンポーネントは、チャネルを使用することで、トレース イベントをユーザーの種類に応じて振り分けることができます。 たとえば、システム管理者向けのイベントを 1 つのチャネルに送信し、アプリケーション開発者にとって重要なイベントを別のチャネルに送信できます。 チャネルには名前が付けられ、Windows に登録されるので、ユーザーは、特定のチャネルのイベントをイベント ビューアーを使用して確認できます。  
  
 [!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] の WCF の分析トレース機能は、Microsoft-Windows-アプリケーション-サーバーアプリケーションのチャネルに書き込みます。 このチャネルは、実稼働環境で WCF サービスの正常性を監視する必要があるユーザー向けに特別に設計されています。 このチャネルでは、さまざまな状態監視およびトラブルシューティング シナリオで使用できるイベントがいくつか定義されています。  
  
 メッセージがイベント ログで正常にデコードされるように Event Tracing for Windows マニファストを有効にするために、次のようにコマンド ラインで ServiceModelReg ツールを使用します。  
  
 `ServiceModelReg.exe -i -c:etw`  
  
### <a name="dynamic-configuration"></a>動的構成  
 ETW のインフラストラクチャでは、標準の Windows ツールを使用して動的にトレースを有効化および構成できます。 詳細については、「[分析トレースの動的な有効化](dynamically-enabling-analytic-tracing.md)」を参照してください。  
  
### <a name="message-flow-tracing"></a>メッセージ フローのトレース  
 メッセージフローのトレースを有効にする方法の詳細については、「[メッセージフローのトレースの構成](configuring-message-flow-tracing.md)」を参照してください。  
  
### <a name="keywords"></a>キーワード  
 キーワードは、トレースメッセージをフィルター処理し、イベントを生成した .NET Framework のコンポーネントを定義するために使用されます。 詳細については、「[分析トレースの動的な有効化](dynamically-enabling-analytic-tracing.md)」を参照してください。
