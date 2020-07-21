---
title: トレースの拡張
ms.date: 03/30/2017
ms.assetid: 2b971a99-16ec-4949-ad2e-b0c8731a873f
ms.openlocfilehash: 59bdfeea41bac812840ffe166895050a6cd1ad2d
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600517"
---
# <a name="extend-tracing"></a>トレースの拡張

このサンプルでは、ユーザー定義のアクティビティトレースをクライアントとサービスコードに記述することによって、Windows Communication Foundation (WCF) トレース機能を拡張する方法を示します。 ユーザー定義のアクティビティトレースを記述すると、ユーザーはトレースアクティビティを作成し、トレースを論理的な作業単位にグループ化することができます。 さらに、転送 (同じエンドポイント内) や伝達 (異なるエンドポイント間) を経由してアクティビティを相互に関連付けることもできます。 このサンプルでは、トレースはクライアントとサービスの両方で有効です。 クライアントとサービスの構成ファイルでトレースを有効にする方法の詳細については、「[トレースとメッセージログ](tracing-and-message-logging.md)」を参照してください。  
  
 このサンプルは、[はじめに](getting-started-sample.md)に基づいています。  
  
> [!NOTE]
> このサンプルのセットアップ手順とビルド手順については、このトピックの最後を参照してください。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Management\ExtendingTracing`  
  
## <a name="tracing-and-activity-propagation"></a>トレースとアクティビティの伝達  
 ユーザー定義のアクティビティトレースを使用すると、ユーザーは独自のトレースアクティビティを作成して、トレースを論理的な作業単位にグループ化し、転送と伝達を通じてアクティビティを相互に関連付けることができます。また、WCF トレース (ログファイルのディスク領域コストなど) のパフォーマンスコストを削減することもできます。  
  
### <a name="add-custom-sources"></a>カスタムソースの追加  
 ユーザー定義のトレースは、クライアントとサービス コードの両方に追加できます。 トレースソースをクライアントまたはサービスの構成ファイルに追加すると、これらのカスタムトレースを記録して[サービストレースビューアーツール (svctraceviewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md)に表示できます。 次のコードは、`ServerCalculatorTraceSource` というユーザー定義のトレース ソースを構成ファイルに追加する方法を示します。  
  
```xml  
<system.diagnostics>  
    <sources>  
        <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
        <source name="ServerCalculatorTraceSource" switchValue="Information,ActivityTracing">  
            <listeners>  
                <add type="System.Diagnostics.DefaultTraceListener" name="Default">  
                    <filter type="" />  
                </add>  
                <add name="xml">  
                    <filter type="" />  
                </add>  
            </listeners>  
        </source>  
    </sources>  
    <sharedListeners>  
       <add initializeData="C:\logs\ServerTraces.svclog" type="System.Diagnostics.XmlWriterTraceListener"  
        name="xml" traceOutputOptions="Callstack">  
            <filter type="" />  
        </add>  
    </sharedListeners>  
    <trace autoflush="true" />  
</system.diagnostics>
....
```  
  
### <a name="correlate-activities"></a>アクティビティの関連付け  
 エンドポイント間でアクティビティを直接関連付けるには、`propagateActivity` トレース ソースの `true` 属性を `System.ServiceModel` に設定する必要があります。 また、WCF アクティビティを介さずにトレースを伝達するには、ServiceModel アクティビティトレースをオフにする必要があります。 次のコード サンプルを参照してください。  
  
> [!NOTE]
> ServiceModel アクティビティ トレースをオフにすることは、`switchValue` プロパティが表すトレース レベルをオフにすることとは異なります。  
  
```xml  
<system.diagnostics>  
    <sources>  
      <source name="System.ServiceModel" switchValue="Warning" propagateActivity="true">  
  
    ...  
  
       </source>  
    </sources>  
</system.diagnostics>  
```  
  
### <a name="lessen-performance-cost"></a>パフォーマンスコストの軽減  
 `ActivityTracing` トレース ソースの `System.ServiceModel` をオフに設定すると、ユーザー定義のアクティビティ トレースのみを含み、ServiceModel アクティビティ トレースは含まないトレース ファイルが生成されます。 ServiceModel アクティビティトレースを除外すると、ログファイルが大幅に小さくなります。 ただし、WCF 処理トレースを相互に関連付ける機会は失われます。  
  
## <a name="set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行する  
  
1. [Windows Communication Foundation サンプルの1回限りのセットアップ手順](one-time-setup-procedure-for-the-wcf-samples.md)を実行したことを確認します。  
  
2. ソリューションの C# 版または Visual Basic .NET 版をビルドするには、「 [Building the Windows Communication Foundation Samples](building-the-samples.md)」の手順に従います。  
  
3. サンプルを単一コンピューター構成または複数コンピューター構成で実行するには、「 [Windows Communication Foundation サンプルの実行](running-the-samples.md)」の手順に従います。  
  
## <a name="see-also"></a>関連項目

- [AppFabric の監視のサンプル](https://docs.microsoft.com/previous-versions/appfabric/ff383407(v=azure.10))
