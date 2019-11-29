---
title: WCF 開発者向けの付録-gRPC
description: 最新のマイクロサービスアーキテクチャにおける分散トランザクションとその実装について説明します。
ms.date: 09/02/2019
ms.openlocfilehash: 061aef016fd0e4303e1bbcbf0e73cec2b0c54f74
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73968218"
---
# <a name="appendix-a---transactions"></a>付録 A-トランザクション

Windows Communication Foundation (WCF) でサポートされている分散トランザクションを使用すると、複数のサービスにわたってアトミックな操作を実行できます。 この機能は、 [Microsoft 分散トランザクションコーディネーター](https://docs.microsoft.com/previous-versions/windows/desktop/ms684146(v=vs.85))に基づいています。

最新のマイクロサービスのランドスケープでは、この種類の自動化された分散トランザクション処理はできません。 1つの環境で使用できるオペレーティングシステム、プログラミング言語、およびフレームワークが混在しているとは言えませんが、多くの場合、リレーショナルデータベース、NoSQL データストア、メッセージングシステムなど、さまざまなテクノロジを利用することはできません。

WCF 分散トランザクションは、 [2 フェーズコミット (2pc)](https://en.wikipedia.org/wiki/Two-phase_commit_protocol)と呼ばれるものを実装したものです。 サービス間でメッセージを調整し、各サービス内で開いているトランザクションを作成し、成功または失敗に応じて "コミット" または "ロールバック" メッセージを送信することによって、2PC トランザクションを手動で実装することができます。 ただし、2PC の管理に関係する複雑さは、システムの進化に伴って指数関数的に増加することがあります。また、開いているトランザクションは、パフォーマンスに悪影響を及ぼす可能性があるデータベースロックを保持し、さらにはサービス間のデッドロックを引き起こす可能性があります。

可能な場合は、分散トランザクションを完全に回避することをお勧めします。 アトミックの更新を必要とするようにデータの2つの項目がリンクされている場合は、それらを同じサービスに対して処理し、単一の要求またはメッセージを使用してそのサービスに対してアトミックな変更を適用することを検討してください。

これが不可能な場合は、別の方法として、 [Saga パターン](https://microservices.io/patterns/data/saga.html)を使用する方法があります。 Saga では、更新は順番に処理されます。各更新が成功すると、次の更新がトリガーされます。 これらのトリガーは、サービスからサービスに伝達することも、saga コーディネーターまたは "orchestrator" によって管理することもできます。 プロセスのどの時点でも更新が失敗した場合、更新を既に完了しているサービスでは、元に戻すための特定のロジックが適用されます。

また、「 [.Net マイクロサービスの電子書籍](https://docs.microsoft.com/dotnet/architecture/microservices/microservice-ddd-cqrs-patterns/)」で説明されているように、ドメイン駆動設計 (DDD) とコマンド/クエリ責務分離 (CQRS) を使用する方法もあります。 特に、ドメインイベントまたは[イベントソーシング](https://martinfowler.com/eaaDev/EventSourcing.html)を使用すると、すぐ&mdash;には適用されない場合に更新が確実に&mdash;されるようにすることができます。

>[!div class="step-by-step"]
>[前へ](application-performance-management.md)
