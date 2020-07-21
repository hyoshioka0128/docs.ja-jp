---
title: <filters>
ms.date: 03/30/2017
ms.assetid: 37a87222-ec78-4728-8105-9ca1bd961f0c
ms.openlocfilehash: e4ce0452cc46a8f29334fa67f51f14b83290b1c8
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "69918886"
---
# \<filters>

`filters` 要素は、ログに記録されるメッセージの種類の制御に使用される XPath フィルターのコレクションを保持します。

フィルターは、`logMessagesAtTransportLevel` を `true` に設定することによって指定されるトランスポート層でのみ適用されます。 サービス レベルおよび形式が正しくないメッセージ ログ記録は、フィルターの影響を受けません。

コレクションにフィルターを追加するには、`add` を使用します。 1 つ以上のフィルターを定義した場合は、少なくとも 1 つのフィルターと一致するメッセージだけが記録されます。 フィルターを定義しなかった場合は、すべてのメッセージが通過します。

フィルターは、完全な XPath 構文をサポートし、構成ファイルでの出現順に適用されます。 フィルターが構文的に正しくない場合は、構成例外が発生します。

SOAP ヘッダー セクションがあるメッセージだけを記録するフィルターの設定方法の例を次に示します。
  
```xml  
<messageLogging logEntireMessage="true"
                logMalformedMessages="true"
                logMessagesAtServiceLevel="true"
                logMessagesAtTransportLevel="true"
                maxMessagesToLog="420">
  <filters>
    <add xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
      /soap:Envelope/soap:Headers
    </add>
  </filters>
</messageLogging>
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Configuration.DiagnosticSection>
- <xref:System.ServiceModel.Diagnostics>
- <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A>
- <xref:System.ServiceModel.Configuration.MessageLoggingElement>
- <xref:System.ServiceModel.Configuration.MessageLoggingElement.Filters%2A>
- <xref:System.ServiceModel.Configuration.XPathMessageFilterElementCollection>
- <xref:System.ServiceModel.Configuration.XPathMessageFilterElement>
- <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>
- [メッセージ ログの構成](../../../wcf/diagnostics/configuring-message-logging.md)
- [\<messageLogging>](messagelogging.md)
