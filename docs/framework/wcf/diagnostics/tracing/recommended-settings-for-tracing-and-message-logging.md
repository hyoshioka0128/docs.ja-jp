---
title: トレースとメッセージ ログの推奨設定
description: WCF のさまざまなオペレーティング環境で推奨されるトレースとメッセージログの設定について説明します。
ms.date: 03/30/2017
ms.assetid: c6aca6e8-704e-4779-a9ef-50c46850249e
ms.openlocfilehash: 71067a4d6f4cec65a148a8162c40e44d82b85784
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245328"
---
# <a name="recommended-settings-for-tracing-and-message-logging"></a>トレースとメッセージ ログの推奨設定
このトピックでは、さまざまな動作環境における、推奨されるトレースとメッセージ ログの設定について説明します。  
  
## <a name="recommended-settings-for-a-production-environment"></a>本運用環境での推奨される設定  
 本運用環境で WCF トレース ソースを使用する場合は、`switchValue` を Warning に設定します。 WCF `System.ServiceModel` トレース ソースを使用する場合は、`switchValue` 属性を `Warning` に設定し、`propagateActivity` 属性を `true` に設定します。 ユーザー定義のトレース ソースを使用する場合は、`switchValue` 属性を `Warning, ActivityTracing` に設定します。 これは、[構成エディターツール (SvcConfigEditor.exe)](../../configuration-editor-tool-svcconfigeditor-exe.md)を使用して手動で行うことができます。 前述のすべての場合において、パフォーマンスに影響しないと思われる場合は、`switchValue` 属性を `Information` に設定できます。これにより、相当な量のトレース データが生成されます。 次の例に、これらの推奨設定を示します。  
  
```xml  
<configuration>  
 <system.diagnostics>  
  <sources>  
    <source name="System.ServiceModel"  
            switchValue="Warning"  
            propagateActivity="true" >  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
    <source name="myUserTraceSource"  
            switchValue="Warning, ActivityTracing">  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
  </sources>  
  <sharedListeners>  
    <add name="xml"  
         type="System.Diagnostics.XmlWriterTraceListener"  
               initializeData="C:\logs\Traces.svclog" />  
  </sharedListeners>  
 </system.diagnostics>  
  
<system.serviceModel>  
  <diagnostics wmiProviderEnabled="true">  
  </diagnostics>  
 </system.serviceModel>  
</configuration>  
```  
  
## <a name="recommended-settings-for-deployment-or-debugging"></a>展開またはデバッグでの推奨される設定  
 展開またはデバッグ環境では、`Information` または `Verbose` を選択すると共に、ユーザー定義のトレース ソースまたは `ActivityTracing` トレース ソースの場合は `System.ServiceModel` を選択します。 また、デバッグ機能を向上させるには、トレース ソース (`System.ServiceModel.MessageLogging`) を構成に追加してメッセージ ログを有効にする必要があります。 `switchValue` 属性はこのトレース ソースに影響しません。  
  
 次の例に、`XmlWriterTraceListener` を利用した共有リスナーを使用する推奨設定を示します。  
  
```xml  
<configuration>  
 <system.diagnostics>  
  <sources>  
    <source name="System.ServiceModel"  
            switchValue="Information, ActivityTracing"  
            propagateActivity="true" >  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
    <source name="System.ServiceModel.MessageLogging">  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
    <source name="myUserTraceSource"  
            switchValue="Information, ActivityTracing">  
      <listeners>  
        <add name="xml"/>  
      </listeners>  
    </source>  
  </sources>  
  <sharedListeners>  
    <add name="xml"  
         type="System.Diagnostics.XmlWriterTraceListener"  
               initializeData="C:\logs\Traces.svclog" />  
  </sharedListeners>  
 </system.diagnostics>  
  
 <system.serviceModel>  
  <diagnostics wmiProviderEnabled="true">  
      <messageLogging
           logEntireMessage="true"
           logMalformedMessages="true"  
           logMessagesAtServiceLevel="true"
           logMessagesAtTransportLevel="true"  
           maxMessagesToLog="3000"
       />  
  </diagnostics>  
 </system.serviceModel>  
</configuration>  
```  
  
## <a name="using-wmi-to-modify-settings"></a>WMI を使用した設定変更  
 WMI を使用して実行時に構成設定を変更できます (前述の構成例のように構成の `wmiProviderEnabled` 属性を有効にします)。 たとえば、CIM Studio 内で WMI を使用し、実行時にトレース ソース レベルを Warning から Information に変更できます。 この方法でライブ デバッグを実行した場合のパフォーマンスへの負荷は非常に高くなる可能性があるので注意が必要です。 WMI の使用方法の詳細については、「 [using Windows Management Instrumentation For Diagnostics](../wmi/index.md) 」トピックを参照してください。  
  
## <a name="enable-correlated-events-in-aspnet-tracing"></a>ASP.NET トレースでの相関イベントの有効化  
 ASP.NET イベントでは、ASP.NET イベントのトレースが有効になっていないと、相関 ID (ActivityID) が設定されません。 相関イベントを適切に表示するには、コマンドコンソールで次のコマンドを使用して、ASP.NET イベントのトレースを有効にする必要があります。これは、 **Start**、 **Run** 、および type **cmd**に移動して呼び出すことができます。  
  
```console  
logman start mytrace -pf logman.providers -o test.etl –ets  
```  
  
 ASP.NET イベントのトレースを無効にするには、次のコマンドを使用します。  
  
```console
logman stop mytrace -ets  
```  
  
## <a name="see-also"></a>関連項目

- [診断に Windows Management Instrumentation を使用する](../wmi/index.md)
