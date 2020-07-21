---
title: COM アプリケーションとの統合の概要
ms.date: 03/30/2017
helpviewer_keywords:
- COM [WCF], integration overview
ms.assetid: 02c5697f-6e2e-47d6-b715-f3a28aebfbd5
ms.openlocfilehash: c283e7cbc4cb4b8bc37dd1313480410df93a93bf
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596826"
---
# <a name="integrating-with-com-applications-overview"></a>COM アプリケーションとの統合の概要

Windows Communication Foundation (WCF) を使用すると、マネージコード開発者は、接続されたアプリケーションを作成するための豊富な環境を提供できます。 ただし、アンマネージ COM ベースのコードに多大な投資をしていて、移行したくない場合でも、wcf サービスモニカーを使用して、WCF Web サービスを既存のコードに直接統合できます。 サービス モニカーは Office VBA、Visual Basic 6.0、または Visual C++ 6.0 などの幅広い COM ベースの開発環境で使用可能です。

> [!NOTE]
> サービスモニカーは、すべての通信に WCF 通信チャネルを使用します。 このチャネルのセキュリティ メカニズムと識別メカニズムは、標準の COM および DCOM プロキシで使用されるものとは異なります。 また、サービスモニカーでは WCF 通信チャネルが使用されるため、すべての呼び出しで既定のタイムアウト期間は1分です。

サービスモニカーは、関数と共に使用して、 `GetObject` アンマネージ開発者に、WCF Web サービスを呼び出すための厳密に型指定された COM 固有のアプローチを提供します。 これには、WCF Web サービスコントラクトと使用するバインディングの、COM から参照できるローカルな定義が必要です。 他の WCF クライアントと同様に、サービスモニカーは、サービスへの型指定されたチャネルを構築する必要があります。ただし、このチャネルの構築は、最初のメソッド呼び出しで COM プログラマに透過的に行われます。

他の WCF クライアントとの共通点として、モニカーを使用する場合、アプリケーションは、サービスと通信するためのアドレス、バインディング、およびコントラクトを指定します。 コントラクトは、次のいずれかの方法で指定できます。

- 型指定のあるコントラクト - クライアント コンピューターで COM から参照できる型として登録されます。

- WSDL コントラクト - WSDL ドキュメントという形で供給されます。

- MEX コントラクト - 実行時に Metadata Exchange (MEX) エンドポイントから取得されます。

## <a name="parameters-supported-by-the-service-moniker"></a>サービス モニカーでサポートされるパラメーター

サービス モニカーでサポートされるパラメーターを次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`address`|サービスの URL 位置。|
|`binding`|アプリケーション構成のバインディング セクションの名前。|
|`bindingConfiguration`|名前付きバインディング セクション内の名前付きバインディング インスタンス。|
|`contract`|サービス コントラクトまたは (MEX の) コントラクト名を表すインターフェイス識別子 (IID)。|
|`wsdl`|代替形式のコントラクト定義を提供する WSDL ドキュメント。|
|`spnIdentity`|サービスとの通信に使用するサーバー プリンシパル名 (SPN) ID。|
|`upnIdentity`|サービスとの通信に使用するユーザー プリンシパル名 (UPN) ID。|
|`dnsIdentity`|サービスとの通信に使用する DNS ID。|
|`mexAddress`|サービスの Metadata Exchange (MEX) エンドポイントの URL 位置。|
|`mexBinding`|MEX エンドポイントと接続するための、アプリケーション構成のバインディング セクションの名前。|
|`mexBindingConfiguration`|MEX エンドポイントと接続する名前付きバインディング セクション内の名前付きバインディング インスタンス。|
|`bindingNamespace`|取得する MEX のバインディング セクション名の名前空間。|
|`contractNamespace`|取得する MEX のコントラクトの名前空間。|
|`mexSpnIdentity`|MEX エンドポイントとの通信に使用するサーバー プリンシパル名 (SPN) ID。|
|`mexUpnIdentity`|MEX エンドポイントとの通信に使用するユーザー プリンシパル名 (UPN) ID。|
|`mexDnsIdentity`|MEX エンドポイントとの通信に使用する DNS ID。|
|`serializer`|"XML" シリアライザーと "datacontract" シリアライザーのいずれを使用するかを指定します。|

> [!NOTE]
> すべての COM ベースのクライアントで使用されている場合でも、サービスモニカーを使用するには WCF およびサポート .NET Framework 2.0 がクライアントコンピューターにインストールされている必要があります。 また、サービス モニカーを使用するクライアント アプリケーションには、適切なバージョンの .NET Framework ランタイムが読み込まれていることが重要です。 Office アプリケーション内でモニカーを使用する場合、構成ファイルに、正しいフレームワーク バージョンが読み込まれていることを確認する必要があります。 たとえば Excel の場合、Excel.exe ファイルと同じディレクトリにある Excel.exe.config というファイルに、次のテキストが記述されている必要があります。
>
> `<?xml version="1.0" encoding="utf-8"?>`
>
> `<configuration xmlns=` `http://schemas.microsoft.com/.NetConfiguration/v2.0` `>`
>
> `<startup>`
>
> `<requiredRuntime version="v2.0.50727" />`
>
> `</startup>`
>
> `</configuration>`

## <a name="see-also"></a>関連項目

- [方法: サービス モニカーを登録および構成する](how-to-register-and-configure-a-service-moniker.md)
