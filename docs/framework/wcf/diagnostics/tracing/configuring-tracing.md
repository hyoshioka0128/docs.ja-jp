---
title: トレースの構成
description: トレースを有効にする方法、トレースソースを構成する方法、アクティビティのトレースと伝達を設定する方法、およびトレースリスナーを WCF のトレースにアクセスするように設定する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- tracing [WCF]
ms.assetid: 82922010-e8b3-40eb-98c4-10fc05c6d65d
ms.openlocfilehash: 55d701ee6769099698d2fd869a1502d94237b5a8
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245350"
---
# <a name="configuring-tracing"></a>トレースの構成
ここでは、トレースを有効にする方法、トレースを出力し、トレース レベルを設定するようにトレース ソースを構成する方法、エンドツーエンドのトレース相関をサポートするようにアクティビティ トレースと伝達を設定する方法、およびトレースにアクセスするようにトレース リスナーを設定する方法について説明します。  
  
 運用環境またはデバッグ環境でのトレース設定の推奨事項については、「[トレースとメッセージログの推奨設定](recommended-settings-for-tracing-and-message-logging.md)」を参照してください。  
  
> [!IMPORTANT]
> Windows 8 でアプリケーションによるトレース ログの生成を行うには、アプリケーションを権限の高い状態で実行 (管理者として実行) する必要があります。  
  
## <a name="enabling-tracing"></a>トレースの有効化  
 Windows Communication Foundation (WCF) は、診断トレース用に次のデータを出力します。  
  
- 操作呼び出し、コード例外、警告、その他の重要な処理イベントなど、アプリケーションのすべてのコンポーネントにわたるプロセスマイルストーンのトレース。  
  
- トレース機能が正しく動作しないときの Windows エラー イベント。 「[イベントログ](../event-logging/index.md)」を参照してください。  
  
 WCF トレースは、の上に構築されてい <xref:System.Diagnostics> ます。 トレースを使用するには、構成ファイルまたはコードでトレース ソースを定義する必要があります。 WCF は、WCF アセンブリごとにトレースソースを定義します。 `System.ServiceModel`トレースソースは、最も一般的な wcf トレースソースであり、wcf 通信スタック全体にわたる処理マイルストーンを記録します。これは、ユーザーコードを入力したり、そのままにしたりするためにトランスポートから移動する操作です。 `System.ServiceModel.MessageLogging` トレース ソースは、システムを通過するすべてのメッセージを記録します。  
  
 既定では、トレースは無効です。 トレースを有効にするには、トレースリスナーを作成し、構成で選択したトレースソースに対して "Off" 以外のトレースレベルを設定する必要があります。それ以外の場合、WCF はトレースを生成しません。 リスナーを指定しないと、トレースは自動的に無効になります。 リスナーを定義してもトレース レベルを指定しないと、トレース レベルは既定で "Off" に設定され、トレースが出力されなくなります。  
  
 カスタム操作の呼び出し元などの WCF 機能拡張ポイントを使用する場合は、独自のトレースを生成する必要があります。 これは、機能拡張ポイントを実装すると、WCF は既定のパスに標準のトレースを出力できなくなるためです。 トレースを出力することで手動トレースのサポートを実装しない場合、予測したトレースが得られない場合があります。  
  
 トレースを構成するには、アプリケーションの構成ファイル (Web ホストアプリケーションの場合は Web.config) を編集するか、自己ホスト型アプリケーションの場合は Appname.exe.config します。 以下は、このような編集の例です。 これらの設定の詳細については、「トレースを使用するためのトレースリスナーの構成」セクションを参照してください。  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <sources>  
         <source name="System.ServiceModel"
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
            <listeners>  
               <add name="traceListener"
                   type="System.Diagnostics.XmlWriterTraceListener"
                   initializeData= "c:\log\Traces.svclog" />  
            </listeners>  
         </source>  
      </sources>  
   </system.diagnostics>  
</configuration>  
```  
  
> [!NOTE]
> Visual Studio で WCF サービスプロジェクトの構成ファイルを編集するには、アプリケーションの構成ファイル (Web ホストアプリケーションの場合は Web.config) を右クリックし、自己ホスト型アプリケーションの場合は**ソリューションエクスプローラー**で Appname.exe.config します。 次に、[ **WCF 構成の編集**] コンテキストメニュー項目を選択します。 これにより、[構成エディターツール (SvcConfigEditor.exe)](../../configuration-editor-tool-svcconfigeditor-exe.md)が起動されます。これにより、グラフィカルユーザーインターフェイスを使用して WCF サービスの構成設定を変更できます。  
  
## <a name="configuring-trace-sources-to-emit-traces"></a>トレースを出力するためのトレース ソースの構成  
 WCF は、アセンブリごとにトレースソースを定義します。 アセンブリ内で生成されたトレースは、該当するソースで定義されているリスナーによってアクセスされます。 次のトレース ソースが定義されます。  
  
- System.servicemodel: WCF 処理のすべての段階をログに記録します。構成が読み込まれるたびに、メッセージがトランスポートで処理され、セキュリティ処理が行われ、ユーザーコードでメッセージがディスパッチされます。  
  
- System.ServiceModel.MessageLogging: システムを通過するすべてのメッセージを記録します。  
  
- System.IdentityModel  
  
- System.ServiceModel.Activation  
  
- System.IO.Log: Common Log File System (CLFS) への .NET Framework インターフェイスを記録します。  
  
- System.Runtime.Serialization: オブジェクトの読み取りまたは書き込みを記録します。  
  
- CardSpace  
  
 各トレース ソースは、次の構成例に示すように同じ (共有) リスナーを使用するように構成できます。  
  
```xml  
<configuration>  
    <system.diagnostics>  
        <sources>  
            <source name="System.ServiceModel"
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="CardSpace">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.IO.Log">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.Runtime.Serialization">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.IdentityModel">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
        </sources>  
  
        <sharedListeners>  
            <add name="xml"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="c:\log\Traces.svclog" />  
        </sharedListeners>  
    </system.diagnostics>  
</configuration>  
```  
  
 さらに、次の例に示すように、ユーザー定義のトレース ソースを追加してユーザー コード トレースを出力することもできます。  
  
```xml  
<system.diagnostics>  
   <sources>  
       <source name="UserTraceSource" switchValue="Warning, ActivityTracing" >  
          <listeners>  
              <add name="xml"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="C:\logs\UserTraces.svclog" />  
          </listeners>  
       </source>  
   </sources>  
   <trace autoflush="true" />
</system.diagnostics>  
```  
  
 ユーザー定義トレースソースの作成の詳細については、「[トレースの拡張](../../samples/extending-tracing.md)」を参照してください。  
  
## <a name="configuring-trace-listeners-to-consume-traces"></a>トレースを使用するためのトレース リスナーの構成  
 実行時に、WCF はデータを処理するリスナーにトレースデータをフィードします。 WCF には、の定義済みリスナーがいくつか用意されて <xref:System.Diagnostics> います。これは、出力に使用する形式が異なります。 カスタム リスナーの種類を追加することもできます。  
  
 `add` を使用して、使用するトレース リスナーの名前と種類を指定できます。 この例の構成では、リスナーに `traceListener` という名前を付け、使用する種類として標準の .NET Framework トレース リスナー (`System.Diagnostics.XmlWriterTraceListener`) を追加しています。 ソースごとに任意の数のトレース リスナーを追加できます。 トレース リスナーがトレースをファイルに出力する場合は、構成ファイルで出力ファイルの場所と名前を指定する必要があります。 指定するには、`initializeData` をそのリスナーのファイルの名前に設定します。 ファイル名を指定しないと、使用するリスナーの種類に基づいて任意のファイル名が生成されます。 <xref:System.Diagnostics.XmlWriterTraceListener> を使用した場合は、拡張子のないファイル名が生成されます。 カスタム リスナーを実装した場合は、この属性を使用して、ファイル名以外の初期化データを受け取ることもできます。 たとえば、この属性にデータベース識別子を指定できます。  
  
 カスタム トレース リスナーは、ネットワーク上のリモート データベースなどにトレースを送信するように構成できます。 アプリケーションを展開するユーザーは、リモート コンピューターのトレース ログに適切なアクセス制御を適用する必要があります。  
  
 また、トレース リスナーはプログラムによって構成することもできます。 詳細については、「[方法: トレースリスナーを作成および初期化](../../../debug-trace-profile/how-to-create-and-initialize-trace-listeners.md)する」および「[カスタム TraceListener の作成](https://docs.microsoft.com/archive/msdn-magazine/2006/april/clr-inside-out-extending-system-diagnostics)」を参照してください。  
  
> [!CAUTION]
> `System.Diagnostics.XmlWriterTraceListener` はスレッド セーフではないため、トレース ソースは、トレースを出力するときにリソースを排他的にロックする可能性があります。 このリスナーを使用するように構成されたトレース ソースに多くのスレッドがトレースを出力すると、リソースの競合が発生し、パフォーマンスに重大な問題が生じる場合があります。 この問題を解決するには、スレッド セーフなカスタム リスナーを実装する必要があります。  
  
## <a name="trace-level"></a>トレース レベル  
 トレース レベルは、トレース ソースの `switchValue` 設定で制御します。 使用できるトレース レベルを次の表に示します。  
  
|トレース レベル|追跡イベントの性質|追跡イベントの内容|追跡イベント|対象ユーザー|  
|-----------------|----------------------------------|-----------------------------------|--------------------|-----------------|  
|オフ|N/A|N/A|トレースは出力されません。|N/A|  
|重要|"否定的な" イベント: 予期しない処理またはエラー状態を示すイベント。||次の例を含む未処理の例外が記録されます。<br /><br /> -OutOfMemoryException<br />-ThreadAbortException (CLR は任意の ThreadAbortExceptionHandler を呼び出します)<br />-StackOverflowException (キャッチできません)<br />-System.configuration.configurationerrorsexception<br />-SEHException<br />-アプリケーション開始エラー<br />-Failfast イベント<br />-システムがハングする<br />-有害メッセージ: アプリケーションが失敗する原因となるメッセージトレース。|管理者<br /><br /> アプリケーション開発者|  
|エラー|"否定的な" イベント: 予期しない処理またはエラー状態を示すイベント。|予期しない処理が発生した。 アプリケーションが、タスクを正常に実行できなかった。 ただし、アプリケーションは依然として動作している。|すべての例外がログに記録されます。|管理者<br /><br /> アプリケーション開発者|  
|警告|"否定的な" イベント: 予期しない処理またはエラー状態を示すイベント。|問題が発生したか、発生する可能性があるが、アプリケーションは正常に動作している。 ただし、正常な動作を継続できなくなる可能性がある。|-アプリケーションは、制限設定によって許可されているよりも多くの要求を受信しています。<br />-受信キューが、構成されている最大容量に近づいています。<br />-タイムアウトを超えました。<br />-資格情報は拒否されます。|管理者<br /><br /> アプリケーション開発者|  
|Information|"肯定的な" イベント: 成功したマイルストーンをマークするイベント|アプリケーションが正常に動作しているかどうかとは無関係の、アプリケーションの実行に関する重要で正常なマイルストーン。|一般に、システム ステータスの監視と診断、パフォーマンスの計測、またはプロファイリングに有用なメッセージが生成されます。 この情報は、キャパシティ プランニングやパフォーマンス管理のために利用できます。<br /><br /> -チャネルが作成されます。<br />-エンドポイントリスナーが作成されます。<br />-Message はトランスポートに出入りします。<br />-セキュリティトークンが取得されます。<br />-構成設定が読み取られます。|管理者<br /><br /> アプリケーション開発者<br /><br /> 製品開発者。|  
|"詳細"|"肯定的な" イベント: 成功したマイルストーンをマークするイベント。|ユーザーコードとサービスの両方に対する低レベルのイベントが出力されます。|一般に、このレベルはデバッグやアプリケーションの最適化に利用できます。<br /><br /> -メッセージヘッダーを認識しています。|管理者<br /><br /> アプリケーション開発者<br /><br /> 製品開発者。|  
|ActivityTracing||処理アクティビティとコンポーネント間のフロー イベント。|このレベルを使用すると、管理者と開発者は同じアプリケーション ドメイン内のアプリケーションの相関関係を示すことができます。<br /><br /> -開始/停止などのアクティビティ境界のトレース。<br />-転送のトレース。|All|  
|All||アプリケーションが正常に動作している可能性があります。 すべてのイベントが出力されます。|前のすべてのイベント。|すべて|  
  
 Verbose から Critical までのレベルは相互にスタックされます。つまり、各トレース レベルには、そのレベルよりも上位のすべてのレベルが含まれます (Off レベルを除く)。 たとえば、Warning レベルでリッスンしているリスナーは、Critical、Error、Warning の各トレースを受け取ります。 All レベルには、Verbose から Critical までのイベントとアクティビティ トレース イベントが含まれます。  
  
> [!CAUTION]
> Information、Verbose、および ActivityTracing の各レベルは、多くのトレースを生成するため、コンピューターで利用可能なすべてのリソースを使い果たした場合は、メッセージ スループットに悪影響を及ぼす可能性があります。  
  
## <a name="configuring-activity-tracing-and-propagation-for-correlation"></a>アクティビティ トレースと伝達の関連付けの構成  
 `activityTracing` 属性に指定する `switchValue` 値を使用してアクティビティ トレースを有効にし、エンドポイント内のアクティビティの境界と転送のトレースを出力できます。  
  
> [!NOTE]
> WCF で特定の機能拡張機能を使用する場合、 <xref:System.NullReferenceException> アクティビティトレースが有効になっていると、が発生することがあります。 この問題を解決するには、アプリケーションの構成ファイルを調べて、トレース ソースの `switchValue` 属性が `activityTracing` に設定されていないことを確認します。  
  
 `propagateActivity` 属性は、メッセージ交換に参加している他のエンドポイントにアクティビティを伝達する必要があるかどうかを示します。 この値を `true` に設定すると、任意の 2 つのエンドポイントで生成されたトレース ファイルを取得し、一方のエンドポイントのトレース セットがもう一方のエンドポイントのトレース セットにどのように転送されるかを監視できます。  
  
 アクティビティのトレースと伝達の詳細については、「[伝達](propagation.md)」を参照してください。  
  
 `propagateActivity`と `ActivityTracing` ブール値は両方とも System.servicemodel tracesource に適用されます。 この `ActivityTracing` 値は、WCF またはユーザー定義のトレースソースを含む任意のトレースソースにも適用されます。  
  
 ユーザー定義のトレース ソースでは、`propagateActivity` 属性を使用できません。 ユーザー コード アクティビティ ID の伝達では、ServiceModel `ActivityTracing` 属性を `propagateActivity` に設定しているときは、ServiceModel `true` を設定しないでください。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [管理と診断](../index.md)
- [方法: トレース リスナーを作成し初期化する](../../../debug-trace-profile/how-to-create-and-initialize-trace-listeners.md)
- [カスタム TraceListener の作成](https://docs.microsoft.com/archive/msdn-magazine/2006/april/clr-inside-out-extending-system-diagnostics)
