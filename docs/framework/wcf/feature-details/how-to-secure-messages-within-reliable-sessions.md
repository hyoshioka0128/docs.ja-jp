---
title: '方法: 信頼できるセッション内でメッセージをセキュリティで保護する'
ms.date: 03/30/2017
ms.assetid: aee33e50-936f-4486-9ca8-c1520c19a62d
ms.openlocfilehash: 306d0f96b5163fe5c24d270b4b9a7c1d3f499e7e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596956"
---
# <a name="how-to-secure-messages-within-reliable-sessions"></a>方法: 信頼できるセッション内でメッセージをセキュリティで保護する

ここでは、信頼できるセッション内で交換されるメッセージに対して、メッセージ レベルのセキュリティを有効にするために必要な手順について説明します。このとき、信頼できるセッションがオプションでサポートされているシステム指定のバインディングを使用します。 コードを使用するか、構成ファイルで宣言によって、セキュリティで保護された信頼できるセッションを強制的に有効にします。 この手順では、クライアントとサービスの構成ファイルを使用して、セキュリティで保護された信頼できるセッションを有効にします。

この手順の主な部分は、次の 3 つのタスクで構成されます。

1. クライアントとサービスのメッセージ交換は信頼できるセッション内で行うことを指定します。

1. 信頼できるセッション内でメッセージ レベルのセキュリティを要求します。

1. サービスに対する認証時にクライアントが使用する必要があるクライアント資格情報を指定します。

最初のタスクでは、エンドポイント構成要素に `bindingConfiguration` という名前のバインディング構成 (この例では) を参照する属性が含まれていることが重要です `MessageSecurity` 。 次に、 [**\<binding>**](../../configure-apps/file-schema/wcf/bindings.md) 要素の属性をに設定して、構成要素がこの名前を参照して信頼できるセッションを有効にし `enabled` [**\<reliableSession>**](https://docs.microsoft.com/previous-versions/ms731375(v=vs.90)) `true` ます。 信頼できるセッション内で使用できる順序付き配信の保証は、`ordered` 属性を `true` に設定することによって要求できます。

この構成手順の基になっている例のソースコピーについては、「 [WS Reliable Session](../samples/ws-reliable-session.md)」を参照してください。

2番目のタスクの重要な項目は、 `mode` **\<security>** クライアントとサービスの要素に含まれる要素の属性をに設定することによって実現され **\<binding>** `Message` ます。

3番目のタスクの重要な項目は、 `clientCredentialType` **\<message>** クライアントとサービスの要素に含まれる要素の属性をに設定することによって実現され **\<security>** `Certificate` ます。

> [!NOTE]
> 信頼できるセッションでメッセージセキュリティを使用する場合、信頼できるメッセージは、最初のエラー時に例外をスローするのではなく、タイムアウトが発生するまで、認証されていないクライアントの認証を試みます。

### <a name="configure-the-service-with-a-wshttpbinding-to-use-a-reliable-session"></a>信頼できるセッションを使用するようにサービスを WSHttpBinding で構成する

この手順については[、「方法: 信頼できるセッション内でメッセージを交換](how-to-exchange-messages-within-a-reliable-session.md)する」を参照してください。

### <a name="configure-the-client-with-a-wshttpbinding-to-use-a-reliable-session"></a>信頼できるセッションを使用するようにクライアントを WSHttpBinding で構成する

この手順については[、「方法: 信頼できるセッション内でメッセージを交換](how-to-exchange-messages-within-a-reliable-session.md)する」を参照してください。

### <a name="set-the-mode-and-clientcredentialtype-in-configuration"></a>構成にモードと ClientCredentialType を設定する

1. 構成ファイルの要素に適切なバインド要素を追加 [**\<bindings>**](../../configure-apps/file-schema/wcf/bindings.md) します。 次の例では、要素を追加し [**\<wsHttpBinding>**](../../configure-apps/file-schema/wcf/wshttpbinding.md) ます。

1. 要素を追加 **\<binding>** し、その `name` 属性を適切な値に設定します。 この例では、という名前を使用し `MessageSecurity` ます。

1. 要素を追加 **\<security>** し、 `mode` 属性をに設定し `Message` ます。

1. 要素内に **\<security>** 要素を追加 **\<message>** し、 `clientCredentialType` 属性をに設定し `Certificate` ます。

```xml
<wsHttpBinding>
  <binding name="MessageSecurity">
    <security mode="Message">
      <message clientCredentialType="Certificate" />
    </security>
  </binding>
</wsHttpBinding>
```
