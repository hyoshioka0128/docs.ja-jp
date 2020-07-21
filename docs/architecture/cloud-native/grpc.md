---
title: gRPC
description: GRPC、クラウドネイティブアプリケーションでのその役割、および HTTP RESTful 通信との違いについて説明します。
author: robvet
no-loc:
- Blazor
- Blazor WebAssembly
ms.date: 05/13/2020
ms.openlocfilehash: 6b41363008405032f4233448f134a8a602dbd26a
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173160"
---
# <a name="grpc"></a>gRPC

ここまでは、 [REST ベース](https://docs.microsoft.com/azure/architecture/best-practices/api-design)の通信に重点を置いてきました。 REST は、エンティティリソースに対する CRUD ベースの操作を定義する柔軟なアーキテクチャスタイルであることがわかりました。 クライアントは、要求/応答通信モデルを使用して、HTTP を介してリソースと対話します。 REST は広く実装されていますが、新しい通信テクノロジである gRPC は、クラウドネイティブコミュニティ全体で大きな勢いを獲得しています。

## <a name="what-is-grpc"></a>GRPC とは

gRPC は、古い[リモートプロシージャコール (RPC)](https://en.wikipedia.org/wiki/Remote_procedure_call)プロトコルを進化させる最新の高パフォーマンスフレームワークです。 アプリケーションレベルでは、gRPC によって、クライアントとバックエンドサービス間のメッセージングが合理化されます。 Google から提供される gRPC はオープンソースであり、クラウドネイティブオファリングの[クラウドネイティブコンピューティングファンデーション (CNCF)](https://www.cncf.io/)エコシステムの一部です。 CNCF は gRPC を[incubating プロジェクト](https://github.com/cncf/toc/blob/master/process/graduation_criteria.adoc)と見なします。 Incubating は、エンドユーザーが実稼働アプリケーションでテクノロジを使用しており、プロジェクトの共同作成者の数が正常であることを意味します。

一般的な gRPC クライアントアプリは、ビジネス操作を実装する、ローカルのインプロセス関数を公開します。 内部的には、ローカル関数は、リモートコンピューター上で別の関数を呼び出します。 ローカル呼び出しとして表示されるのは、リモートサービスへの透過的なアウトプロセス呼び出しです。 RPC のプラミングは、コンピューター間のポイントツーポイントのネットワーク通信、シリアル化、および実行を抽象化します。

クラウドネイティブアプリケーションでは、開発者は多くの場合、プログラミング言語、フレームワーク、およびテクノロジに対して機能します。 この*相互運用性*により、メッセージコントラクトと、クロスプラットフォーム通信に必要なプラミングが複雑になります。  gRPC には、これらの問題を抽象化する "均一な水平方向のレイヤー" が用意されています。 開発者は、ビジネス機能に重点を置いたネイティブプラットフォームでコードを記述し、gRPC は通信の組み込みを処理します。

gRPC は、Java、JavaScript、C#、ゴー、Swift、NodeJS など、最も人気のある開発スタックで包括的なサポートを提供します。

## <a name="grpc-benefits"></a>gRPC の特典

gRPC は、トランスポートプロトコルとして HTTP/2 を使用します。 Http/2 は HTTP 1.1 と互換性がありますが、多くの高度な機能を備えています。

- データトランスポート用のバイナリプロトコル-データをクリアテキストとして送信する HTTP 1.1 とは異なります。
- 同一の接続で複数の並列要求を送信するための多重化サポート-HTTP 1.1 は、一度に1つの要求/応答メッセージに処理を制限します。
- クライアント要求とサーバー応答の両方を同時に送信するための双方向の全二重通信。
- 要求と応答を有効にして、大きなデータセットを非同期的にストリーム配信できる組み込みのストリーミング。

gRPC は軽量で高いパフォーマンスを備えています。 メッセージ数が60-80% 小さい JSON シリアル化よりも最大8x 倍の速度で実現できます。 Microsoft [Windows Communication Foundation (WCF)](https://docs.microsoft.com/dotnet/framework/wcf/whats-wcf)用語では、grpc のパフォーマンスは、高度に最適化された[nettcp バインド](https://docs.microsoft.com/dotnet/api/system.servicemodel.nettcpbinding?view=netframework-4.8)の速度と効率を超えています。 Microsoft stack を優先する NetTCP とは異なり、gRPC はクロスプラットフォームです。

## <a name="protocol-buffers"></a>プロトコル バッファー

gRPC は、[プロトコルバッファー](https://developers.google.com/protocol-buffers/docs/overview)と呼ばれるオープンソーステクノロジを採用しています。 サービスが相互に送信する構造化メッセージをシリアル化するために、非常に効率的でプラットフォームに依存しないシリアル化形式を提供します。 開発者は、クロスプラットフォームインターフェイス定義言語 (IDL) を使用して、マイクロサービスごとにサービスコントラクトを定義します。 コントラクトは、テキストベースのファイルとして実装され、 `.proto` 各サービスのメソッド、入力、および出力を記述します。 同じコントラクトファイルは、さまざまな開発プラットフォーム上に構築された gRPC クライアントおよびサービスに使用できます。

Protobuf コンパイラである proto ファイルを使用する `protoc` と、ターゲットプラットフォームのクライアントとサービスコードの両方が生成されます。 このコードには、次のコンポーネントが含まれています。

- クライアントとサービスによって共有される、厳密に型指定されたオブジェクト。メッセージのサービス操作とデータ要素を表します。
- リモート gRPC サービスが継承および拡張できる必要なネットワークの組み込みを持つ、厳密に型指定された基本クラス。
- リモート gRPC サービスを呼び出すために必要な構成を含むクライアントスタブ。

実行時には、各メッセージが標準の Protobuf 表現としてシリアル化され、クライアントとリモートサービスの間で交換されます。 JSON や XML とは異なり、Protobuf メッセージはコンパイル済みバイナリバイトとしてシリアル化されます。

Microsoft アーキテクチャサイトから入手できる「 [grpc FOR WCF 開発者](https://docs.microsoft.com/dotnet/architecture/grpc-for-wcf-developers/)」という書籍では、grpc とプロトコルバッファーの詳細について説明しています。

## <a name="grpc-support-in-net"></a>.NET での gRPC のサポート

gRPC は .NET Core 3.0 SDK 以降に統合されています。 次のツールでサポートされています。

- Web 開発ワークロードがインストールされた Visual Studio 2019、バージョン16.3 以降。
- Visual Studio Code
- dotnet CLI

SDK には、エンドポイントルーティング、組み込み IoC、およびログ記録用のツールが含まれています。 オープンソースの Kestrel web サーバーは、HTTP/2 接続をサポートしています。 図4-20 は、gRPC サービスのスケルトンプロジェクトをスキャフォールディングする Visual Studio 2019 テンプレートを示しています。 .NET Core が Windows、Linux、および macOS を完全にサポートしていることに注意してください。

![Visual Studio 2019 での gRPC のサポート](./media/visual-studio-2019-grpc-template.png)

**図 4-20** Visual Studio 2019 での gRPC のサポート
  
図4-21 は、Visual Studio 2019 に含まれる組み込みスキャフォールディングから生成されたスケルトン gRPC サービスを示しています。  

![Visual Studio 2019 の gRPC プロジェクト](./media/grpc-project.png  )

**図 4-21** Visual Studio 2019 の gRPC プロジェクト

前の図では、proto description ファイルとサービスコードに注意してください。 すぐにわかるように、Visual Studio では、スタートアップクラスと基になるプロジェクトファイルの両方に追加の構成が生成されます。

## <a name="grpc-usage"></a>gRPC の使用

次のシナリオで gRPC を優先します。

- 同期バックエンドマイクロサービスからマイクロサービスへの通信。処理を続行するために即時応答が必要です。
- 混合プログラミングプラットフォームをサポートする必要がある多言語環境。
- 低待機時間と高スループット通信で、パフォーマンスが重要です。
- ポイントツーポイントのリアルタイム通信-gRPC は、ポーリングせずにリアルタイムでメッセージをプッシュでき、双方向ストリーミングが優れたサポートを備えています。
- ネットワークの制約付き環境–バイナリ gRPC のメッセージは、常に同等のテキストベースの JSON メッセージよりも小さくなります。

このドキュメントの執筆時点では、gRPC は主にバックエンドサービスで使用されています。 ほとんどの最新のブラウザーでは、フロントエンドの gRPC クライアントをサポートするために必要な HTTP/2 コントロールのレベルを提供できません。 ただし、JavaScript またはテクノロジで構築されたブラウザーベースのアプリから gRPC 通信を可能にする[初期のイニシアチブ](https://devblogs.microsoft.com/aspnet/grpc-web-experiment/)があり Blazor WebAssembly ます。 [Grpc-Web for .net](https://github.com/grpc/grpc/blob/master/doc/PROTOCOL-WEB.md)を使用すると、ASP.NET Core grpc アプリで、ブラウザーアプリで grpc 機能をサポートできます。

- 厳密に型指定された、コード生成クライアント
- Compact Protobuf メッセージ
- サーバー ストリーミング。

## <a name="grpc-implementation"></a>gRPC の実装

Microsoft からの[コンテナーである](https://github.com/dotnet-architecture/eShopOnContainers)、マイクロサービス参照アーキテクチャは、.net Core アプリケーションで grpc サービスを実装する方法を示しています。 図4-22 は、バックエンドアーキテクチャを示しています。

![コンテナーの eShop のバックエンドアーキテクチャ](./media/eshop-with-aggregators.png)

**図 4-22** コンテナーの eShop のバックエンドアーキテクチャ

前の図では、eShop が複数の API ゲートウェイを公開することによって、フロントエンド pattern (bff)[のバックエンド](https://docs.microsoft.com/azure/architecture/patterns/backends-for-frontends)を採用していることに注意してください。 BFF パターンについては、この章で前に説明しました。 Web ショッピング API ゲートウェイとバックエンドショッピングマイクロサービスの間にあるアグリゲーターマイクロサービス (灰色) に細心の注意を払ってください。 アグリゲーターは、クライアントから1つの要求を受信し、それをさまざまなマイクロサービスにディスパッチし、結果を集計して、要求元のクライアントに送信します。 このような操作では、通常、即時応答を生成するために同期通信が必要です。 EShop では、アグリゲーターからのバックエンド呼び出しは、図4-23 に示すように gRPC を使用して実行されます。

![コンテナーの eShop にある gRPC](./media/grpc-implementation.png)

**図 4-23**.  コンテナーの eShop にある gRPC

gRPC 通信には、クライアントコンポーネントとサーバーコンポーネントの両方が必要です。 前の図で、ショッピングアグリゲーターが gRPC クライアントを実装する方法に注目してください。 クライアントは、同期 gRPC 呼び出し (赤) をバックエンドマイクロサービスに対して実行し、それぞれが gRPC サーバーを実装します。 クライアントとサーバーの両方で、.NET Core SDK から組み込まれている gRPC の組み込み機能を利用します。 クライアント側*スタブ*は、リモート grpc 呼び出しを呼び出すための機構を提供します。 サーバー側コンポーネントは、カスタムサービスクラスが継承して使用できる gRPC の組み込み機能を提供します。

RESTful API と gRPC 通信の両方を公開するマイクロサービスでは、複数のエンドポイントでトラフィックを管理する必要があります。 RESTful 呼び出しの場合は HTTP トラフィックをリッスンし、gRPC 呼び出しの場合は別のエンドポイントを開きます。 Grpc 通信に必要な HTTP/2 プロトコル用に gRPC エンドポイントを構成する必要があります。

マイクロサービスと非同期通信パターンを分離することに努めていますが、一部の操作では直接呼び出しが必要です。 gRPC は、マイクロサービス間の直接同期通信に主な選択肢となります。 HTTP/2 とプロトコルバッファーに基づく高パフォーマンスの通信プロトコルによって、最適な選択肢になります。

## <a name="looking-ahead"></a>今後の予定

今後、gRPC は引き続きクラウドネイティブシステムの牽引力を獲得します。 パフォーマンスの利点と開発の容易さは説得力を持っています。 ただし、残りの時間は長くなる可能性があります。 パブリックに公開されている Api および旧バージョンとの互換性のために適しています。

>[!div class="step-by-step"]
>[前へ](service-to-service-communication.md)
>[次へ](service-mesh-communication-infrastructure.md)
