---
title: Send アクティビティのキャッシュ共有レベルの変更
ms.date: 03/30/2017
ms.assetid: 03926a64-753d-460e-ac06-2a4ff8e1bbf5
ms.openlocfilehash: 101aab98a7d34ad45ad29efbe252cff0814ca290
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185391"
---
# <a name="changing-the-cache-sharing-levels-for-send-activities"></a>Send アクティビティのキャッシュ共有レベルの変更
<xref:System.ServiceModel.Activities.SendMessageChannelCache> 拡張機能により、キャッシュ共有レベルのカスタマイズやチャネル ファクトリ キャッシュの設定のカスタマイズを行えるほか、<xref:System.ServiceModel.Activities.Send> メッセージング アクティビティを使用してサービス エンドポイントにメッセージを送信するワークフローのチャネル キャッシュの設定のカスタマイズも可能になります。 これらのワークフローは、通常はクライアント ワークフローですが、<xref:System.ServiceModel.WorkflowServiceHost> でホストされるワークフロー サービスである場合もあります。 チャネル ファクトリ キャッシュには、<xref:System.ServiceModel.ChannelFactory%601> オブジェクトがキャッシュされます。 チャネル キャッシュには、チャネルがキャッシュされます。  
  
> [!NOTE]
> ワークフローは <xref:System.ServiceModel.Activities.Send> メッセージング アクティビティを使用してメッセージまたはパラメーターを送信できます。 このワークフローのランタイムはチャネル ファクトリをキャッシュに追加しますが、チャネル ファクトリで作成されるチャネルは、<xref:System.ServiceModel.Channels.IRequestChannel> アクティビティを <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティと共に使用したときは <xref:System.ServiceModel.Activities.Send> 型で、<xref:System.ServiceModel.Channels.IOutputChannel> アクティビティだけを (<xref:System.ServiceModel.Activities.Send> なしで) 使用したときは <xref:System.ServiceModel.Activities.ReceiveReply> 型です。  
  
## <a name="the-cache-sharing-levels"></a>キャッシュ共有レベル  
 既定では、<xref:System.ServiceModel.WorkflowServiceHost> によってホストされるワークフローにおいて、<xref:System.ServiceModel.Activities.Send> メッセージング アクティビティが使用するキャッシュは <xref:System.ServiceModel.WorkflowServiceHost> のすべてのワークフロー インスタンス間で共有されます (ホストレベルのキャッシュ)。 <xref:System.ServiceModel.WorkflowServiceHost> によってホストされないクライアント ワークフローの場合、キャッシュを使用できるのはワークフロー インスタンスだけです (インスタンスレベルのキャッシュ)。 このキャッシュは、アンセーフ キャッシュが有効になっている場合を除き、構成で定義されているエンドポイントを使用しない <xref:System.ServiceModel.Activities.Send> アクティビティに対してのみ使用可能です。  
  
 ワークフローの <xref:System.ServiceModel.Activities.Send> アクティビティに使用可能なさまざまなキャッシュ共有レベルと、推奨される使用方法を次に示します。  
  
- **ホスト レベル**: ホスト共有レベルでは、キャッシュはワークフロー サービス ホストでホストされているワークフロー インスタンスでのみ使用できます。 キャッシュはプロセス全体のキャッシュのワークフロー サービス ホスト間で共有できます。  
  
- **インスタンス レベル**: インスタンス共有レベルでは、キャッシュは有効期間を通じて特定のワークフロー インスタンスで使用できますが、キャッシュは他のワークフロー インスタンスでは使用できません。  
  
- **キャッシュなし**: 構成で定義されたエンドポイントを使用するワークフローがある場合、キャッシュは既定でオフになっています。 この場合、キャッシュをオンにすると安全性が損なわれることがあるため、オフにしておくことをお勧めします。 たとえば、送信ごとに異なる ID (異なる資格情報、または偽装の使用) が必要な場合があります。  
  
## <a name="changing-the-cache-sharing-level-for-a-client-workflow"></a>クライアント ワークフローのキャッシュ共有レベルの変更  
 クライアント ワークフローでのキャッシュの共有を設定するには、<xref:System.ServiceModel.Activities.SendMessageChannelCache> クラスのインスタンスを目的のワークフロー インスタンスのセットに拡張として追加します。 この結果、すべてのワークフロー インスタンス間でキャッシュが共有されます。 次のコード例は、この手順を実行する方法を示しています。  
  
 まず、<xref:System.ServiceModel.Activities.SendMessageChannelCache> 型のインスタンスを宣言します。  
  
```csharp  
// Create an instance of SendMessageChannelCache with default cache settings.  
static SendMessageChannelCache sharedChannelCacheExtension =  
    new SendMessageChannelCache();  
```  
  
 次に、各クライアント ワークフローのインスタンスにキャッシュ拡張を追加します。  
  
```csharp
WorkflowApplication clientInstance1 = new WorkflowApplication(new clientWorkflow1());  
WorkflowApplication clientInstance2 = new WorkflowApplication(new clientWorkflow2());  
  
// Share the cache extension object
  
clientInstance1.Extensions.Add(sharedChannelCacheExtension);  
clientInstance2.Extensions.Add(sharedChannelCacheExtension);  
```  
  
## <a name="changing-the-cache-sharing-level-for-a-hosted-workflow-service"></a>ホストされるワークフロー サービスのキャッシュ共有レベルの変更  
 ホストされるワークフロー サービスでのキャッシュの共有を設定するには、<xref:System.ServiceModel.Activities.SendMessageChannelCache> クラスのインスタンスをすべてのワークフロー サービス ホストに拡張として追加します。 この結果、すべてのワークフロー サービス ホスト間でキャッシュが共有されます。 次のコード例は、この手順を実行する方法を示しています。  
  
 まず、<xref:System.ServiceModel.Activities.SendMessageChannelCache> 型のインスタンスをクラス レベルで宣言します。  
  
```csharp  
// Create static instance of SendMessageChannelCache with default cache settings.  
static SendMessageChannelCache sharedChannelCacheExtension = new  
    SendMessageChannelCache();  
```  
  
 次に、各ワークフロー サービス ホストに静的キャッシュ拡張を追加します。  
  
```csharp  
WorkflowServiceHost host1 = new WorkflowServiceHost(new serviceWorkflow1(), new Uri(baseAddress1));  
WorkflowServiceHost host2 = new WorkflowServiceHost(new serviceWorkflow2(), new Uri(baseAddress2));  
  
// Share the static cache to get an AppDomain level cache.  
host1.WorkflowExtensions.Add(sharedChannelCacheExtension);  
host2.WorkflowExtensions.Add(sharedChannelCacheExtension);  
```  
  
 ホストされるワークフロー サービスでのキャッシュ共有をインスタンス レベルに設定するには、`Func<SendMessageChannelCache>` デリゲートをワークフロー サービス ホストに拡張として追加し、<xref:System.ServiceModel.Activities.SendMessageChannelCache> クラスの新しいインスタンスをインスタンス化するコードにこのデリゲートを割り当てます。 この結果、ワークフロー サービス ホストのすべてのワークフロー インスタンスで 1 つのキャッシュが共有されるのではなく、ワークフロー インスタンスごとに異なるキャッシュが使用されます。 次のコード例は、このデリゲートがポイントする <xref:System.ServiceModel.Activities.SendMessageChannelCache> 拡張を直接定義するラムダ式を使用して上記の処理を実行する方法を示しています。  
  
```csharp
serviceHost.WorkflowExtensions.Add(() => new SendMessageChannelCache  
{  
    // Use FactorySettings property to add custom factory cache settings.  
    FactorySettings = new ChannelCacheSettings
    { MaxItemsInCache = 5, },  
    // Use ChannelSettings property to add custom channel cache settings.  
    ChannelSettings = new ChannelCacheSettings
    { MaxItemsInCache = 10 },  
});  
```  
  
## <a name="customizing-cache-settings"></a>キャッシュ設定のカスタマイズ  
 チャネル ファクトリ キャッシュおよびチャネル キャッシュのキャッシュ設定をカスタマイズできます。 キャッシュ設定は <xref:System.ServiceModel.Activities.ChannelCacheSettings> クラスで定義されています。 この<xref:System.ServiceModel.Activities.SendMessageChannelCache>クラスは、チャネル ファクトリ キャッシュとチャネル キャッシュの既定のキャッシュ設定をパラメーターなしのコンストラクターで定義します。 次の表は、これらのキャッシュ設定の既定値をキャッシュのタイプごとに示しています。  
  
|設定|LeaseTimeout (分)|IdleTimeout (分)|MaxItemsInCache|  
|-|-|-|-|  
|ファクトリ キャッシュの既定値|TimeSpan.MaxValue|2|16|  
|チャネル キャッシュの既定値|5|2|16|  
  
 ファクトリ キャッシュおよびチャネル キャッシュの設定をカスタマイズするには、パラメーター化されたコンストラクター <xref:System.ServiceModel.Activities.SendMessageChannelCache> を使用して <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> クラスをインスタンス化し、<xref:System.ServiceModel.Activities.ChannelCacheSettings> の新しいインスタンスをカスタム値と共に `factorySettings` パラメーターおよび `channelSettings` パラメーターにそれぞれ渡します。 次に、このクラスの新しいインスタンスをワークフロー サービス ホストまたはワークフロー インスタンスに拡張として追加します。 次のコード例は、ワークフロー インスタンスに対してこの手順を実行する方法を示しています。  
  
```csharp  
ChannelCacheSettings factorySettings = new ChannelCacheSettings{  
                        MaxItemsInCache = 5,
                        IdleTimeout = TimeSpan.FromMinutes(5),
                        LeaseTimeout = TimeSpan.FromMinutes(20)};  
  
ChannelCacheSettings channelSettings = new ChannelCacheSettings{  
                        MaxItemsInCache = 5,
                        IdleTimeout = TimeSpan.FromMinutes(2),  
                        LeaseTimeout = TimeSpan.FromMinutes(10) };  
  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache(factorySettings, channelSettings);  
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 構成で定義されているエンドポイントがワークフロー サービスにある場合にキャッシュを有効にするには、<xref:System.ServiceModel.Activities.SendMessageChannelCache> パラメーターが <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> に設定された、パラメーター化されたコンストラクター `allowUnsafeCaching` を使用して `true` クラスをインスタンス化します。 次に、このクラスの新しいインスタンスをワークフロー サービス ホストまたはワークフロー インスタンスに拡張として追加します。 次のコード例は、ワークフロー インスタンスのキャッシュを有効にする方法を示しています。  
  
```csharp  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache{ AllowUnsafeCaching = true };  
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 チャネル ファクトリおよびチャネルのキャッシュを完全に無効にするには、チャネル ファクトリ キャッシュを無効にします。 こうすると、対応するチャネル ファクトリにチャネルが所有されるので、チャネル キャッシュもオフになります。 チャネル ファクトリ キャッシュを無効にするには、`factorySettings` 値が 0 の <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> インスタンスに初期化された <xref:System.ServiceModel.Activities.ChannelCacheSettings> コンストラクターに <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> パラメーターを渡します。 このコード例を次に示します。  
  
```csharp  
// Disable the factory cache. This results in the channel cache to be turned off as well.  
ChannelCacheSettings factorySettings = new ChannelCacheSettings  
    { MaxItemsInCache = 0 };  
  
ChannelCacheSettings channelSettings = new ChannelCacheSettings();  
  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache(factorySettings, channelSettings);
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 チャネル ファクトリ キャッシュのみを使用し、チャネル キャッシュを無効にするには、`channelSettings` 値が 0 の <xref:System.ServiceModel.Activities.SendMessageChannelCache.%23ctor%2A> インスタンスに初期化された <xref:System.ServiceModel.Activities.ChannelCacheSettings> コンストラクターに <xref:System.ServiceModel.Activities.ChannelCacheSettings.MaxItemsInCache%2A> パラメーターを渡します。 このコード例を次に示します。  
  
```csharp  
ChannelCacheSettings factorySettings = new ChannelCacheSettings();  
// Disable only the channel cache.  
ChannelCacheSettings channelSettings = new ChannelCacheSettings  
    { MaxItemsInCache = 0};  
  
SendMessageChannelCache customChannelCacheExtension =
    new SendMessageChannelCache(factorySettings, channelSettings);
  
clientInstance.Extensions.Add(customChannelCacheExtension);  
```  
  
 ホストされたワークフロー サービスでは、ファクトリ キャッシュとチャネル キャッシュの設定をアプリケーション構成ファイルで指定できます。 これを行うには、ファクトリ キャッシュおよびチャネル キャッシュのキャッシュ設定を含むサービス動作を追加し、そのサービス動作をサービスに追加します。 次の例は、カスタム ファクトリ キャッシュとチャネル`MyChannelCacheBehavior`キャッシュ設定を使用したサービス動作を含む構成ファイルの内容を示しています。 このサービス動作は、 属性を介して`behaviorConfiguration`サービスに追加されます。  
  
```xml  
<configuration>
  <system.serviceModel>  
    <!-- List of other config sections here -->
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="MyChannelCacheBehavior">  
          <sendMessageChannelCache allowUnsafeCaching ="false" >  
            <!-- Control only the host level settings -->
            <factorySettings maxItemsInCache = "8" idleTimeout = "00:05:00" leaseTimeout="10:00:00" />  
            <channelSettings maxItemsInCache = "32" idleTimeout = "00:05:00" leaseTimeout="00:06:00" />  
          </sendMessageChannelCache>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <services>  
      <service name="MyService" behaviorConfiguration="MyChannelCacheBehavior" />  
    </services>  
  </system.serviceModel>  
</configuration>  
```
