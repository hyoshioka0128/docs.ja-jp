---
title: 複数の IIS サイト バインディングのサポート
description: IIS で WCF サービスをホストするときに同じサイトで同じプロトコルを使用している複数のベースアドレスを指定する方法について説明します。
ms.date: 03/30/2017
ms.assetid: 40440495-254d-45c8-a8c6-b29f364892ba
ms.openlocfilehash: 290dca03dbed7d0a7442a3903b735eb189929ed1
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244869"
---
# <a name="supporting-multiple-iis-site-bindings"></a>複数の IIS サイト バインディングのサポート
インターネットインフォメーションサービス (IIS) 7.0 で Windows Communication Foundation (WCF) サービスをホストする場合、同じサイトで同じプロトコルを使用する複数のベースアドレスを指定することができます。 これにより、同じサービスで多数の異なる URI に応答できます。 これは、とでリッスンするサービスをホストする場合に便利です `http://www.contoso.com` `http://contoso.com` 。 また、内部ユーザー用に 1 つのベース アドレスを持ち、外部ユーザー用に別のベース アドレスを持つサービスを作成するのにも役立ちます。 たとえば、`http://internal.contoso.com` と `http://www.contoso.com` などです。  
  
> [!NOTE]
> この機能は、HTTP プロトコルを使用してのみ、使用可能です。  
  
## <a name="multiple-base-addresses"></a>複数のベース アドレス  
 この機能は、IIS でホストされている WCF サービスでのみ使用できます。 この機能は、既定では有効にされません。 これを有効にするには、 `multipleSiteBindingsEnabled` `serviceHostingEnvironment` 次の `true` 例に示すように、属性を Web.config ファイルの <> 要素に追加し、に設定する必要があります。  
  
```xml  
<serviceHostingEnvironment multipleSiteBindingsEnabled="true"/>  
```  
  
 IIS で WCF サービスをホストする場合、IIS は、アプリケーションを含む仮想ディレクトリへの URI に基づいて、1つのベースアドレスを作成します。 インターネット インフォメーション サービス マネージャーを使用して、同じプロトコルを使用するベース アドレスを追加し、1 つ以上のバインディングを Web サイトに追加できます。 それぞれのバインディングに対して、プロトコル (HTTP または HTTPS)、IP アドレス、ポート、およびホスト名を指定します。 インターネットインフォメーションサービス Manager の使用方法の詳細については、「 [Iis マネージャー (iis 7)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753842(v=ws.10))」を参照してください。 サイトにバインドを追加する方法の詳細については、「 [Web サイトを作成する (IIS 7)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772350(v=ws.10)) 」を参照してください。  
  
 同じサイトに複数のベースアドレスを指定すると、WCF ヘルプページの内容、インポートスキーマ、およびサービスによって生成される WSDL/MEX 情報が影響を受けます。 WCF ヘルプページには、サービスと通信できる WCF クライアントを生成するために使用するコマンドラインが表示されます。 このコマンド ラインには、その Web サイト用の IIS バインディングで指定された最初のアドレスだけが含まれています。 同様に、スキーマをインポートするときには、IIS バインディングで指定された最初のベース アドレスだけが使用されます。 WSDL および MEX データには、IIS バインディングで指定されたすべてのベース アドレスが含まれています。  
  
> [!WARNING]
> つまり、サービスに 2 つのベース アドレス (1 つは内部ユーザー用、もう 1 つは外部ユーザー用) がある場合、サービスによって生成される WSDL/MEX 情報では、両方のベース アドレスが指定されます。
