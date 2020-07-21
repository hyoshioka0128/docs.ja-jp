---
title: 探索プロキシの実装
ms.date: 03/30/2017
ms.assetid: dda20e79-8df3-438e-a281-69d779d978ec
ms.openlocfilehash: 382df95fef2108d338e4ea327da9185c856eca5a
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84579242"
---
# <a name="implementing-a-discovery-proxy"></a>探索プロキシの実装
ここでは、探索プロキシの実装に必要な手順について説明します。 探索プロキシは、サービスのリポジトリを格納するスタンドアロンのサービスです。 クライアントは探索プロキシに対し、そのプロキシで認識される探索可能なサービスを問い合わせることができます。 プロキシにサービスを登録する方法は、実装手段によって異なります。 たとえば、探索プロキシが既存のサービス リポジトリに接続でき、その情報を探索可能にできる場合、管理者は管理 API を使用して探索可能なサービスをプロキシに追加することができます。または、探索プロキシにアナウンス機能を使用し、内部キャッシュを更新できます。  
  
 WCF 実装は、プロキシを簡単にビルドできる基本クラスを提供します。 これらの API を利用して、既存のリポジトリの上に探索プロキシをビルドできます。  
  
 ここで実装される探索プロキシは、探索可能にしてクライアントからエンドポイントを検索できるという点で、他の WCF サービスと似ています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: 探索プロキシを実装する](how-to-implement-a-discovery-proxy.md)  
 探索プロキシを実装する方法について説明します。  
  
 [方法: 探索プロキシで登録される探索可能なサービスの実装する](discoverable-service-that-registers-with-the-discovery-proxy.md)  
 探索プロキシに登録する探索可能な WCF サービスを実装する方法について説明します。  
  
 [方法: 探索プロキシを使用してサービスを検索するクライアント アプリケーションを実装する](client-app-discovery-proxy-to-find-a-service.md)  
 探索プロキシを使用してサービスを検索する WCF クライアントアプリケーションを実装する方法について説明します。  
  
 [方法: 探索プロキシをテストする](how-to-test-the-discovery-proxy.md)  
 前の 3 つのトピックに記述されたコードのテスト方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [WCF Discovery](wcf-discovery.md)
- [方法: プログラムを使用して探索可能性に WCF サービスとクライアントを追加する](how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)
