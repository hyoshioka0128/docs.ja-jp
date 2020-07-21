---
title: WCF Data Services 4.5
description: REST セマンティクスを使用してデータを公開および使用するためのサービスをサポートする .NET Framework コンポーネント、WCF Data Services について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- Astoria
- WCF Data Services, getting started
ms.assetid: 73d2bec3-7c92-4110-b905-11bb0462357a
ms.openlocfilehash: ca6b196e8c910f97ead6d1df5b6c0dd6c49c68a4
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85503851"
---
# <a name="wcf-data-services-45"></a>WCF Data Services 4.5

WCF Data Services (従来の "ADO.NET Data Services") は .NET Framework のコンポーネントです。これを使用すると、[Representational State Transfer (REST)](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) のセマンティクスを使用し、Open Data Protocol (OData) を使用して Web またはイントラネット上のデータを公開および使用するサービスを作成できます。 OData は、URI でアドレス指定できるリソースとしてデータを公開します。 標準的な HTTP 動詞である GET、PUT、POST、および DELETE を使用してデータにアクセスし、変更できます。 OData では、[Entity Data Model](../adonet/entity-data-model.md) のエンティティとリレーションシップの規則を使用して、アソシエーションで関連付けられた一連のエンティティとしてリソースを公開します。

WCF Data Services は、OData プロトコルを使用してリソースのアドレス指定および更新を行います。 これにより、OData をサポートする任意のクライアントからサービスにアクセスできるようになります。 OData を使用すると、XML としてデータを交換および更新するための標準のセットである Atom と、AJAX アプリケーションで広範に使用されるテキスト ベースのデータ交換形式である JavaScript Object Notation (JSON) という広く知られている転送形式を使用して、データをリソースに要求または書き込むことができます。

WCF Data Services では、さまざまなソースからのデータを OData フィードとして公開できます。 Visual Studio のツールを使用すると、ADO.NET Entity Framework データ モデルを使用して OData ベースのサービスを簡単に作成できます。 OData フィードは、共通言語ランタイム (CLR) クラスに基づいて作成できます。また、遅延バインディング データまたは型指定されていないデータに基づいて作成することもできます。

WCF Data Services には、クライアント ライブラリのセット (一般的な .NET Framework クライアント アプリケーション用と Silverlight ベースのアプリケーション用) も含まれています。 これらのクライアント ライブラリは、.NET Framework や Silverlight などの環境から OData フィードにアクセスするときにオブジェクト ベースのプログラミング モデルを提供します。

## <a name="where-should-i-start"></a>開始すべき場所

各自の興味に応じて、次のトピックのいずれかから WCF Data Services の使用を開始することを検討してください。

すぐに使用を開始する…

- [クイック スタート](quickstart-wcf-data-services.md)

- [はじめに](getting-started-with-wcf-data-services.md)

コードを見たい...

- [クイック スタート](quickstart-wcf-data-services.md)

- [方法: データ サービス クエリを実行する](how-to-execute-data-service-queries-wcf-data-services.md)

- [方法: Windows Presentation Foundation 要素にデータをバインドする](bind-data-to-wpf-elements-wcf-data-services.md)

OData について詳しく知りたい...

- [ホワイト ペーパー: OData の概要](https://download.microsoft.com/download/E/5/A/E5A59052-EE48-4D64-897B-5F7C608165B8/IntroducingOData.pdf)
- [Open Data Protocol Web サイト](https://www.odata.org/)
- [OData: SDK](https://www.odata.org/ecosystem/)

エンド ツー エンドのサンプルを見たい...

- [WCF Data Services クイックスタート](https://github.com/microsoftarchive/msdn-code-gallery-community-s-z/tree/master/WCF%20Data%20Services%20Quickstart%20(OData%20Service%20and%20WPF%20Client))
- [OData SDK - サンプル コード](https://www.odata.org/ecosystem/#sdk)

Visual Studio との統合について知りたい

- [データ サービス クライアント ライブラリの生成](generating-the-data-service-client-library-wcf-data-services.md)

- [データ サービスの作成](creating-the-data-service.md)

- [Entity Framework プロバイダー](entity-framework-provider-wcf-data-services.md)

何に使用できるかを知りたい

- [概要](wcf-data-services-overview.md)

- [アプリケーション シナリオ](application-scenarios-wcf-data-services.md)

LINQ を使用したい...

- [データ サービスに対するクエリ](querying-the-data-service-wcf-data-services.md)

- [LINQ に関する留意点](linq-considerations-wcf-data-services.md)

- [方法: データ サービス クエリを実行する](how-to-execute-data-service-queries-wcf-data-services.md)

より詳しい情報が欲しい...

- [WCF Data Services チームのブログ](https://docs.microsoft.com/archive/blogs/astoriateam/)

- [リソース](wcf-data-services-resources.md)

## <a name="in-this-section"></a>このセクションの内容

[概要](wcf-data-services-overview.md)

WCF Data Services で使用可能な機能の概要について説明します。

[WCF Data Services 5.0 の新機能](https://docs.microsoft.com/previous-versions/dotnet/wcf-data-services/ee373845(v=vs.103))

WCF Data Services の新機能と、OData の新機能のサポートについて説明します。

[はじめに](getting-started-with-wcf-data-services.md)

WCF Data Services を使用して OData フィードを公開および使用する方法について説明します。

[WCF Data Services の定義](defining-wcf-data-services.md)

OData フィードを公開するデータ サービスを作成および構成する方法について説明します。

[WCF Data Services クライアント ライブラリ](wcf-data-services-client-library.md)

クライアント ライブラリを使用して .NET Framework クライアント アプリケーションから OData フィードを使用する方法について説明します。

## <a name="see-also"></a>関連項目

- [Representational State Transfer (REST)](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
