---
title: Windows Communication Foundation の採用
ms.date: 03/30/2017
ms.assetid: 49ba71e2-9468-4082-84c5-cf8daf95e34a
ms.openlocfilehash: a31bd5382e67565bd54272c5c7f400eacd5297d6
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84576539"
---
# <a name="adopt-windows-communication-foundation"></a>Windows Communication Foundation を採用する

ASP.NET を使用して開発した既存のアプリケーションを引き続き維持しながら、新しい開発に Windows Communication Foundation (WCF) を使用することもできます。 WCF は、任意のシナリオで .NET Framework で構築されたアプリケーションとの通信を容易にするために最適な選択肢となることを目的としているため、ASP.NET ができない方法でさまざまなソフトウェア通信の問題を解決するための標準ツールとして使用できます。

新しい WCF アプリケーションは、既存の ASP.NET Web サービスと同じコンピューターにデプロイできます。 既存の ASP.NET Web サービスがバージョン2.0 より前のバージョンの .NET Framework を使用する場合は、ASP.NET IIS 登録ツールを使用して、新しい WCF アプリケーションがホストされる IIS アプリケーションに .NET Framework 2.0 を選択的に展開できます。 このツールは、 [ASP.NET Iis Registration tool (Aspnet_regiis)](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/k6h9cz8h(v=vs.90))に記載されており、iis 6.0 管理コンソールにはユーザーインターフェイスが組み込まれています。

ASP.NET 互換モードで実行するように構成されている WCF サービスを IIS の既存の ASP.NET Web サービスアプリケーションに追加することにより、WCF を使用して、既存の ASP.NET Web サービスに新しい機能を追加できます。 ASP.NET 互換モードのため、新しい WCF サービスのコードは、クラスを使用して、既存の ASP.NET コードと同じアプリケーション状態情報にアクセスし、更新することができ <xref:System.Web.HttpContext> ます。 また、アプリケーションは同じクラス ライブラリを共有することもできます。

WCF クライアントでは、ASP.NET Web サービスを使用できます。 で構成されている WCF サービスは、 <xref:System.ServiceModel.BasicHttpBinding> ASP.NET Web サービスクライアントで使用できます。 ASP.NET Web サービスは、WCF アプリケーションと共存できます。また、WCF を使用して、既存の ASP.NET Web サービスに機能を追加することもできます。 これらの方法で WCF と ASP.NET Web サービスを一緒に使用できるようになった場合は、ASP.NET Web サービスではなく、WCF によって提供される機能が必要な場合にのみ、ASP.NET Web サービスを WCF に移行することをお勧めします。

場合によっては、あるテクノロジから別のテクノロジにコードを移行する方法はほとんどありません。 新しいテクノロジを採用する理由は、以前のテクノロジでは満たすことができない新しい要件を満たすことであり、その場合は、新しく展開された一連の要件を満たす新しいソリューションを設計することです。 新しい設計では、既存のシステムでの経験とそのシステムを設計して以来、獲得した知識を活用できます。 また、新しい設計は、新しいプラットフォーム上で古い設計を再制作するのではなく、新しいテクノロジの機能を十分に活用することができます。 新しいデザインの重要な要素をプロトタイプ作成した後は、新しい設計の既存のシステムからコードを再利用しやすくなります。

## <a name="see-also"></a>関連項目

- [方法: メタデータの取得および準拠サービスの実装をする](how-to-retrieve-metadata-and-implement-a-compliant-service.md)
