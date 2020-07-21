---
title: Windows Communication Foundation ツール
description: WCF アプリケーションを簡単に作成、デプロイ、および管理できるように設計された WCF ツールについて説明します。 これらのツールは、コマンドプロンプトから実行します。
ms.date: 03/30/2017
helpviewer_keywords:
- WCF, tools
- Windows Communication Foundation, tools
ms.assetid: 399a47b4-bfea-434b-8e83-f76b5063d79d
ms.openlocfilehash: acc142e8e3108a827b63cf013b818d30b5dcaa52
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245971"
---
# <a name="windows-communication-foundation-tools"></a>Windows Communication Foundation ツール
Microsoft Windows Communication Foundation (WCF) ツールは、WCF アプリケーションの作成、展開、および管理を容易にするように設計されています。 このセクションには、これらのツールに関する詳細な情報があります。 ツールはサポートされていません。  
  
 すべてのツールは、コマンド ラインから実行できます。  
  
 次の表は、ツールの一覧と簡単な説明を示します。  
  
|ツール|説明|  
|----------|-----------------|  
|[ServiceModel メタデータ ユーティリティ ツール (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md)|メタデータ ドキュメントからサービス モデル コードを生成し、サービス モデル コードからメタデータ ドキュメントを生成します。|  
|[秘密キー検索ツール (FindPrivateKey.exe)](find-private-key-tool-findprivatekey-exe.md)|指定されたストアから秘密キーを取得します。|  
|[ServiceModel 登録ツール (ServiceModelReg.exe)](servicemodelreg-exe.md)|単一コンピューター上で ServiceModel の登録と登録解除を管理します。|  
|[COM+ サービス モデル構成ツール (ComSvcConfig.exe)](com-service-model-configuration-tool-comsvcconfig-exe.md)|COM+ インターフェイスを Web サービスとして公開されるように構成します。|  
|[構成エディター ツール (SvcConfigEditor.exe)](configuration-editor-tool-svcconfigeditor-exe.md)|WCF サービスの構成設定を作成および変更します。|  
|[サービス トレース ビューアー ツール (SvcTraceViewer.exe)](service-trace-viewer-tool-svctraceviewer-exe.md)|WCF サービスの問題を診断、修復、および検証できるように、トレース メッセージの表示、グループ化、およびフィルター処理を容易にします。|  
|[WS-AtomicTransaction 構成ユーティリティ (wsatConfig.exe)](ws-atomictransaction-configuration-utility-wsatconfig-exe.md)|コマンド ライン ツールを使用して、基本的な WS-AtomicTransaction サポート設定を構成します。|  
|[WS-AtomicTransaction 構成 MMC スナップイン](ws-atomictransaction-configuration-mmc-snap-in.md)|MMC スナップインを使用して、基本的な WS-AtomicTransaction サポート設定を構成します。|  
|[ワークフロー サービス登録ツール (WFServicesReg.exe)](workflow-service-registration-tool-wfservicesreg-exe.md)|Windows ワークフロー サービスを登録します。|  
|[WCF サービス ホスト (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)|ライブラリ (* .dll) ファイルに含まれる WCF サービスをホストします|  
|[WCF のテスト用クライアント (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)|任意の型のパラメーターを入力し、その入力をサービスに送信して、サービスから返される応答を表示するために使用される GUI ツールです。|  
|[コントラクト優先ツール](contract-first-tool.md)|XSD データ コントラクトからコード クラスを作成する Visual Studio のビルド タスク。|  
  
 ServiceModelReg.exe、WsatConfig.exe、および ComSvcConfig.exe を除き、これらすべてのツールは Windows SDK に付属しており、C:\Program Files\Microsoft SDKs\Windows\v6.0\Bin フォルダーにあります。  上記の 3 つのツールは、C:\Windows\Microsoft.NET\Framework\v3.0\Windows Communication Foundation にあります。
