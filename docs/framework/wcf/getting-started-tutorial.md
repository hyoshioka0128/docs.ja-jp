---
title: 'チュートリアル: Windows コミュニケーション ファウンデーション アプリケーションの使用を開始する'
description: これらのチュートリアルでは、WCF アプリケーションを作成するための概要を提供します。
ms.date: 01/25/2019
helpviewer_keywords:
- WCF [WCF], get started
- Windows Communication Foundation [WCF], get started
- get started [WCF]
ms.assetid: df939177-73cb-4440-bd95-092a421516a1
ms.openlocfilehash: df73f953372202796cebce9d3e3f28bd617c67ef
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79184120"
---
# <a name="tutorial-get-started-with-windows-communication-foundation-applications"></a>チュートリアル: Windows コミュニケーション ファウンデーション アプリケーションの使用を開始する
次の一連のチュートリアルでは、Windows 通信基盤 (WCF) プログラミングエクスペリエンスを紹介します。 これらのチュートリアルを順番に操作すると、WCF アプリケーションの作成に必要な手順を理解できます。 完了すると、実行中の WCF サービスと、サービスを呼び出す WCF クライアントが作成されます。

このチュートリアルでは、開発環境として Visual Studio を使用していることを前提としています。 別の開発環境を使用している場合は、Visual Studio 固有の手順を無視します。

ダウンロードして実行できるサンプル WCF アプリケーションについては[、「Windows コミュニケーション ファウンデーションのサンプル](samples/index.md)」を参照してください。 サンプルの概要については、「[はじめにのサンプル](samples/getting-started-sample.md)」を参照してください。

サービスとクライアントの作成の詳細については、「[基本 WCF プログラミング](basic-wcf-programming.md)」を参照してください。

## <a name="wcf-tutorials"></a>WCF チュートリアル

最初の 3 つのチュートリアルでは、WCF サービス コントラクトを定義する方法、実装する方法、およびそれをホストする方法について説明します。 作成するサービスは、コンソール アプリケーション内で自己ホストされます。 また、Microsoft インターネット インフォメーション サービス (IIS) でサービスをホストすることもできます。 詳細については、「[方法 : IIS で WCF サービスをホストする](feature-details/how-to-host-a-wcf-service-in-iis.md)」を参照してください。 チュートリアルでは、コードを使用してサービスを構成しますが、[構成ファイル内でサービスを構成](configuring-services-using-configuration-files.md)することもできます。

- [チュートリアル: サービス コントラクトの定義](how-to-define-a-wcf-service-contract.md)

    ユーザー定義のインターフェイスを使用して WCF コントラクトを作成します。 このコントラクトは、サービスが公開する機能を定義します。

- [チュートリアル: サービス コントラクトの実装](how-to-implement-a-wcf-contract.md)

    コントラクトを定義したら、サービス クラスを使用してコントラクトを実装する必要があります。

- [チュートリアル: 基本サービスをホストして実行する](how-to-host-and-run-a-basic-wcf-service.md)

    サービスのエンドポイントを構成し、コンソール アプリケーションでサービスをホストします。 サービスをアクティブにするには、サービスを構成し、ランタイム環境内でホストする必要があります。 このランタイム環境は、サービスを作成し、そのコンテキストと有効期間を制御します。

次の 2 つのチュートリアルでは、クライアント アプリケーションを作成、構成、および使用して、サービスが公開する操作を呼び出す方法について説明します。 サービスは、クライアント アプリケーションがサービスと通信するために必要な情報を定義したメタデータを公開します。 Visual Studio は、このメタデータにアクセスするプロセスを自動化し、サービスのクライアント アプリケーションを構築するために使用します。 Visual Studio を使用しない場合は、代わりに[サービス モデル メタデータ ユーティリティ ツール (*Svcutil.exe*) を](servicemodel-metadata-utility-tool-svcutil-exe.md)使用できます。

- [チュートリアル: クライアントの作成](how-to-create-a-wcf-client.md)

    WCF サービスから WCF クライアント プロキシを作成するためのメタデータを取得します。 メタデータを取得するには、Visual Studio を使用してサービス参照を追加するか、サービス モデル メタデータ ユーティリティ ツールを使用できます。 クライアントがサービスにアクセスするために使用するエンドポイントを指定します。

- [チュートリアル: クライアントを使用する](how-to-use-a-wcf-client.md)

    WCF クライアント プロキシを使用して、サービス操作を呼び出します。

## <a name="reference"></a>リファレンス

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>

## <a name="see-also"></a>関連項目

- [概念の概要](conceptual-overview.md)
- [ドキュメントのガイド](guide-to-the-documentation.md)
- [Windows コミュニケーション ファウンデーションとは](whats-wcf.md)
- [WCF 機能の詳細](feature-details/index.md)
- [基本的なプログラミングライフサイクル](basic-programming-lifecycle.md)
- [クライアントの構築](building-clients.md)
- [基本的な WCF プログラミング](basic-wcf-programming.md)
- [方法: 双方向コントラクトを作成する](feature-details/how-to-create-a-duplex-contract.md)
- [方法: 双方向コントラクトでサービスにアクセスする](feature-details/how-to-access-services-with-a-duplex-contract.md)
- [サービスモデル メタデータ ユーティリティ ツール (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md)
- [方法: Svcutil.exe を使用してメタデータ ドキュメントをダウンロードする](feature-details/how-to-use-svcutil-exe-to-download-metadata-documents.md)
- [[方法] 構成ファイルを使用してサービスのメタデータを公開する](feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)
- [バインディングを使用したサービスとクライアントの構成](using-bindings-to-configure-services-and-clients.md)
- [はじめにのサンプル](samples/getting-started-sample.md)
- [Windows コミュニケーション ファウンデーションのサンプル](samples/index.md)
- [自己ホスト](samples/self-host.md)
