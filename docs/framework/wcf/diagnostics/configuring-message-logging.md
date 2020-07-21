---
title: メッセージ ログの構成
description: ログを有効にする方法、ログレベル、メッセージフィルター、WCF でカスタムリスナーを構成する方法など、メッセージログを構成する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- message logging [WCF]
ms.assetid: 0ff4c857-8f09-4b85-9dc0-89084706e4c9
ms.openlocfilehash: 5203f19a18e5fa6b0ed7f68e1d1de0447da41abd
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85247663"
---
# <a name="configuring-message-logging"></a>メッセージ ログの構成

ここでは、さまざまなシナリオでのメッセージ ログの構成方法を示します。

## <a name="enabling-message-logging"></a>メッセージ ログの有効化

Windows Communication Foundation (WCF) では、既定ではメッセージはログに記録されません。 メッセージ ログをアクティブにするには、トレース リスナーを `System.ServiceModel.MessageLogging` トレース ソースに追加し、構成ファイルで `<messagelogging>` 要素の属性を設定する必要があります。

次の例は、ログを有効にして追加オプションを指定する方法を示しています。

```xml
<system.diagnostics>
  <sources>
    <source name="System.ServiceModel.MessageLogging">
      <listeners>
         <add name="messages"
              type="System.Diagnostics.XmlWriterTraceListener"
              initializeData="c:\logs\messages.svclog" />
        </listeners>
    </source>
  </sources>
</system.diagnostics>

<system.serviceModel>
  <diagnostics>
    <messageLogging
         logEntireMessage="true"
         logMalformedMessages="false"
         logMessagesAtServiceLevel="true"
         logMessagesAtTransportLevel="false"
         maxMessagesToLog="3000"
         maxSizeOfMessageToLog="2000"/>
  </diagnostics>
</system.serviceModel>
```

メッセージログの設定の詳細については、「[トレースとメッセージログの推奨設定](./tracing/recommended-settings-for-tracing-and-message-logging.md)」を参照してください。

`add` を使用して、使用するリスナーの名前と型を指定することができます。 この例の構成では、リスナーに "messages" という名前を付け、使用する型として標準の .NET Framework トレース リスナー (`System.Diagnostics.XmlWriterTraceListener`) を追加しています。 `System.Diagnostics.XmlWriterTraceListener` を使用する場合は、構成ファイルで出力ファイルの場所と名前を指定する必要があります。 指定するには、`initializeData` をログ ファイルの名前に設定します。 それ以外の場合、例外がスローされます。 また、既定のファイルにログを出力するカスタム リスナーを実装することもできます。

> [!NOTE]
> メッセージ ログはディスク領域にアクセスするため、ディスクに書き込む特定のサービスのメッセージ数を制限する必要があります。 メッセージ数が上限に達すると、情報レベルでのトレースが生成され、すべてのメッセージ ログ処理が停止します。

ログ レベルと追加オプションについては、「ログ レベルとオプション」のセクションで説明します。

`switchValue` の `source` 属性は、トレースに対してのみ有効です。 `switchValue` 属性を `System.ServiceModel.MessageLogging` トレース ソースに対して次のように指定しても無効です。

```xml
<source name="System.ServiceModel.MessageLogging" switchValue="Verbose">
</source>
```

トレース ソースを無効にする場合は、代わりに `logMessagesAtServiceLevel` 要素の `logMalformedMessages` 属性、`logMessagesAtTransportLevel` 属性、および `messageLogging` 属性を使用する必要があります。 これらすべての属性を `false` に設定します。 この設定を行うには、構成エディター UI インターフェイスで前のコード例の構成ファイルを使用するか、または WMI を使用します。 構成エディターツールの詳細については、「[構成エディターツール (SvcConfigEditor.exe)](../configuration-editor-tool-svcconfigeditor-exe.md)」を参照してください。 WMI の詳細については、「[診断のための Windows Management Instrumentation の使用](./wmi/index.md)」を参照してください。

## <a name="logging-levels-and-options"></a>ログ レベルとオプション

受信メッセージの場合は、メッセージが形成された直後、サービス レベルでメッセージがユーザー コードで処理される直前、および正しくないメッセージが検出されたときに、ログが記録されます。

送信メッセージの場合は、メッセージがユーザー コードから出力された直後およびメッセージがネットワークに出力される直前に、ログが記録されます。

WCF は、サービスとトランスポートの2つの異なるレベルでメッセージをログに記録します。 不正なメッセージも記録されます。 3 つのカテゴリは互いに独立しており、構成で個別に有効にすることができます。

`logMessagesAtServiceLevel` 要素の `logMalformedMessages`、`logMessagesAtTransportLevel`、および `messageLogging` の各属性を設定することによって、ログ レベルを制御することができます。

### <a name="service-level"></a>サービス レベル

このレイヤーでは、ユーザー コードに入力 (受信時) される直前、またはユーザー コードから出力 (送信時) される直前のメッセージが記録されます。 フィルターを定義した場合は、そのフィルターと一致するメッセージだけが記録されます。 それ以外の場合は、サービス レベルのすべてのメッセージが記録されます。 このレベルでは、インフラストラクチャ メッセージ (トランザクション、ピア チャネル、およびセキュリティ) も記録されます。ただし、信頼できるメッセージング メッセージは記録されません。 ストリーム メッセージの場合は、ヘッダーだけが記録されます。 また、セキュリティで保護されたメッセージもこのレベルで復号化されて記録されます。

### <a name="transport-level"></a>トランスポート レベル

このレイヤーで記録されるメッセージは、ネットワーク上での転送に向けてエンコードできる状態になっているもの、および転送後にデコードできる状態になっているものです。 フィルターを定義した場合は、そのフィルターと一致するメッセージだけが記録されます。 それ以外の場合は、トランスポート レイヤーのすべてのメッセージが記録されます。 このレイヤーでは、信頼できるメッセージング メッセージを含むすべてのインフラストラクチャ メッセージが記録されます。 ストリーム メッセージの場合は、ヘッダーだけが記録されます。 また、セキュリティで保護されたメッセージも、HTTPS などのセキュリティで保護されたトランスポートを使用している場合を除き、暗号化された状態でこのレベルで記録されます。

### <a name="malformed-level"></a>不正レベル

無効なメッセージとは、処理のどの段階でも WCF スタックによって拒否されるメッセージのことです。 正しくないメッセージは、そのままの状態で記録されます。暗号化されていれば、暗号化されたままで、適切でない XML も、そのままになります。 `maxSizeOfMessageToLog` は、CDATA として記録されるメッセージのサイズを定義します。 `maxSizeOfMessageToLog` の既定値は 256 K です。 この属性の詳細については、「その他のオプション」セクションを参照してください。

### <a name="other-options"></a>その他のオプション

ログ レベルに加えて、次のオプションを指定することができます。

- 全体メッセージの記録 (`logEntireMessage` 属性) : この値は、全体メッセージ (メッセージ ヘッダーと本文) を記録するかどうかを指定します。 既定値は、`false` で、ヘッダーだけ記録することを意味します。 この設定は、サービス メッセージ ログ レベルおよびトランスポート メッセージ ログ レベルに影響を与えます。

- 記録するメッセージの最大数 (`maxMessagesToLog` 属性) : この値は、記録するメッセージの最大数を指定します。 すべてのメッセージ (サービス メッセージ、トランスポート メッセージ、および不正メッセージ) が、このクォータに対してカウントされます。 クォータに達すると、トレースが出力され、それ以上メッセージは記録されません。 既定値は 10000 です。

- 記録するメッセージの最大サイズ (`maxSizeOfMessageToLog` 属性) : この値は、記録するメッセージの最大サイズをバイト単位で指定します。 サイズ制限を超えたメッセージは記録されず、そのメッセージに対して何の処理も実行されません。 この設定は、すべてのトレース レベルに影響を与えます。 ServiceModel トレースがオンの場合は、最初の記録ポイントで警告レベル トレース (ServiceModelSend* または TransportReceive) が出力され、ユーザーに通知します。 サービス レベルとトランスポート レベルのメッセージの既定値は 256 K ですが、正しくないメッセージの既定値は 4 K です。

  > [!CAUTION]
  > `maxSizeOfMessageToLog` と照合するために計算されるメッセージ サイズは、シリアル化される前のメモリ上でのメッセージ サイズです。 このサイズは、記録されるメッセージ文字列の実際の長さとは異なります。実際のサイズよりも大きい場合がほとんどです。 その結果、メッセージが記録されない場合があります。 `maxSizeOfMessageToLog` 属性をメッセージの見積もりサイズよりも 10% 大きく設定することによって、この現象を回避することができます。 また、不正メッセージを記録する場合は、メッセージ ログに使用する実際のディスク領域を、`maxSizeOfMessageToLog` で指定した値の最大 5 倍にすることができます。

構成ファイルでトレース リスナーを定義していない場合は、ログ レベルの指定に関係なくログ出力は生成されません。

このセクションで説明されている属性などのメッセージ ログ オプションは、実行時に WMI (Windows Management Instrumentation) を使用して変更できます。 これを行うには、 [AppDomainInfo](./wmi/appdomaininfo.md)インスタンスにアクセスします。このインスタンスは、、、およびのブール型プロパティを公開します `LogMessagesAtServiceLevel` `LogMessagesAtTransportLevel` `LogMalformedMessages` 。 そのため、メッセージ ログ用のトレース リスナーを構成していても、これらのオプションを構成で `false` に設定している場合は、後でアプリケーションを実行しているときに `true` に変更できます。 これで、メッセージ ログが実行時に有効になります。 同様に、構成ファイルでメッセージ ログを有効にしている場合は、実行時に WMI を使用して無効にできます。 詳細については、「[診断のための Windows Management Instrumentation の使用](./wmi/index.md)」を参照してください。

メッセージ ログの `source` フィールドは、要求メッセージを送信または受信する際に要求/応答または一方向の要求については、サービス モデル レイヤーまたはトランスポート レイヤーで、または正しくないメッセージの場合に、メッセージを記録するコンテキストを指定します。

間違った形式のメッセージの場合、 `source` はと等しく `Malformed` なります。 それ以外の場合、source には、コンテキストに基づいて、以下の値が設定されます。

要求/応答の場合

||Send Request|Receive Request|Send Reply|Receive Reply|
|-|------------------|---------------------|----------------|-------------------|
|Service Model layer|サービス<br /><br /> Level<br /><br /> Send<br /><br /> 要求|サービス<br /><br /> Level<br /><br /> 受信<br /><br /> 要求|サービス<br /><br /> Level<br /><br /> Send<br /><br /> Reply|サービス<br /><br /> Level<br /><br /> 受信<br /><br /> Reply|
|Transport layer|トランスポート<br /><br /> Send|トランスポート<br /><br /> 受信|トランスポート<br /><br /> Send|トランスポート<br /><br /> 受信|

一方向の要求の場合

||Send Request|Receive Request|
|-|------------------|---------------------|
|Service Model layer|サービス<br /><br /> Level<br /><br /> Send<br /><br /> データグラム|サービス<br /><br /> Level<br /><br /> 受信<br /><br /> データグラム|
|Transport layer|トランスポート<br /><br /> Send|トランスポート<br /><br /> 受信|

## <a name="message-filters"></a>メッセージ フィルター

メッセージ フィルターは、`messageLogging` 構成セクションの `diagnostics` 構成要素で定義されます。 これらは、サービス レベルとトランスポート レベルで適用されます。 1 つ以上のフィルターを定義した場合は、少なくとも 1 つのフィルターと一致するメッセージだけが記録されます。 フィルターを定義しなかった場合は、すべてのメッセージが通過します。

フィルターは、完全な XPath 構文をサポートし、構成ファイルでの出現順に適用されます。 フィルターが構文的に正しくない場合は、構成例外が発生します。

フィルターは、フィルターに一致するかどうかを確認できる、XPath DOM 内のノードの最大数を制限する `nodeQuota` 属性を使用することで、安全機能も提供します。

次の例は、SOAP ヘッダー セクションがあるメッセージだけを記録するフィルターの設定方法を示します。

```xml
<messageLogging logEntireMessage="true"
    logMalformedMessages="true"
    logMessagesAtServiceLevel="true"
    logMessagesAtTransportLevel="true"
    maxMessagesToLog="420">
    <filters>
        <add nodeQuota="10" xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
                 /soap:Envelope/soap:Header
        </add>
     </filters>
</messageLogging>
```

フィルターは、メッセージの本文には適用できません。 メッセージの本文を操作しようとするフィルターは、フィルターの一覧から削除されます。 その場合には、このことを示すイベントも出力されます。 たとえば、次のフィルターは、フィルター テーブルから削除されます。

```xml
<add xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">/s:Envelope/s:Body[contains(text(), "Hello")]</add>
```

## <a name="configuring-a-custom-listener"></a>カスタム リスナーの構成

追加オプションでカスタム リスナーを構成することもできます。 カスタム リスナーは、記録を行う前に、アプリケーション固有の PII 要素をメッセージからフィルター処理するのに役立ちます。 次の例は、カスタム リスナーの構成を示しています。

```xml
<system.diagnostics>
   <sources>
     <source name="System.ServiceModel.MessageLogging">
           <listeners>
             <add name="MyListener"
                    type="YourCustomListener"
                    initializeData="c:\logs\messages.svclog"
                    maxDiskSpace="1000"/>
           </listeners>
     </source>
   </sources>
</system.diagnostics>
```

`type` 属性は、型のアセンブリ修飾名に設定する必要があることに注意してください。

## <a name="see-also"></a>関連項目

- [\<messageLogging>](../../configure-apps/file-schema/wcf/messagelogging.md)
- [メッセージ ログ](message-logging.md)
- [トレースとメッセージ ログの推奨設定](./tracing/recommended-settings-for-tracing-and-message-logging.md)
