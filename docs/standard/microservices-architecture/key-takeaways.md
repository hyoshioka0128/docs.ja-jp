---
title: 重要な習得事項
description: コンテナー化された .NET アプリケーションの .NET マイクロサービス アーキテクチャ | 重要な習得事項
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.openlocfilehash: d6e09b9856396e99c9b03d595c1896e2451724fe
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2018
ms.locfileid: "53152262"
---
# <a name="key-takeaways"></a>重要な習得事項

概要および重要な習得事項として、次にこのガイドの最も重要な結論を示します。

**コンテナーを使用するメリット** コンテナーは、実稼働環境での依存関係の欠如のために発生する導入の問題の解決策であるため、コンテナーベースのソリューションはコストの節約の重要な利点を提供します。 コンテナーは、DevOps および運用操作を大幅に向上させます。

**コンテナーは、至る所で使用されます。** Docker ベースのコンテナーは、コンテナー業界では事実上の標準になりつつあり、Windows と Linux のエコシステムで最も重要なベンダーでサポートされています。 これには、Microsoft、Amazon AWS、Google、および IBM が含まれます。 将来、Docker は、クラウドとオンプレミスの両方のデータセンターで広く使用されるようになるでしょう。

**配置の展開の単位。** Docker コンテナーは、サーバー ベースのアプリケーションまたはサービスの配置の標準的な単位になっています。

**マイクロサービス。** マイクロサービス アーキテクチャは、自律的なサービスの形式の複数の独立したサブシステムを基にした、分散された大規模または複雑なミッションクリティカルなアプリケーションに対して推奨されるアプローチになりつつあります。 マイクロサービスベースのアーキテクチャでは、アプリケーションは、個別に開発、テスト、展開、バージョン管理、拡張が可能なサービスのコレクションとして構築され、これには関連する自律的なデータベースが含まれます。

**ドメイン駆動設計と SOA。** マイクロサービス アーキテクチャ パターンは、サービス指向アーキテクチャ (SOA) とドメイン駆動設計 (DDD) から派生します。 特定のドメインを成形する進化するビジネス ルールを使用して、環境用のマイクロサービスを設計および開発するときには、DDD アプローチとパターンを考慮することが重要です。

**マイクロサービスの課題。** マイクロサービスは、独立した展開、強力なサブシステムの境界などの多くの強力な機能とテクノロジの多様性を提供します。 ただし、断片化と独立したデータ モデル、マイクロサービス間の回復力のある通信、最終的な一貫性、ログ情報と監視情報を複数のマイクロサービスから収集する結果としての運用の複雑さなどの分散アプリケーションの開発に関連する多くの新しい課題も発生させます。 これらの要素は、従来のモノリシック アプリケーションより高いレベルの複雑さを発生させます。 その結果、特定のシナリオだけが、マイクロサービスベースのアプリケーションに適しています。 これには、複数の進化するサブシステムを含む大規模で複雑なアプリケーションが含まれます。これらのケースでは、より複雑なソフトウェア アーキテクチャに投資する価値があります。それは長期的な機敏性とアプリケーションのメンテナスを提供するためです。

**任意のアプリケーションのコンテナー。** コンテナーは、マイクロサービスにとって便利ですが、それら専用ではありません。 コンテナーは、従来の .NET Framework に基づき、Windows コンテナーを介して最新化されたレガシ アプリケーションを含む、モノリシック アプリケーションにも使用できます。 展開から実稼働に関する多くの問題の解決、最先端の開発およびテストの環境の提供など、Docker を使用することの利点は、さまざまな種類のアプリケーションに適用されます。

**CLI と IDE の比較。** Microsoft のツールを使用し、優先されるアプローチを使用して、コンテナー化された .NET アプリケーションを開発できます。 Docker CLI と Visual Studio Code を使用し、CLI とエディター ベースの環境を使用して開発できます。 または、マルチコンテナー アプリケーションをデバッグできる機能など、Visual Studio の IDE 中心のアプローチや Docker の独自の機能を使用できます。

**回復力のあるクラウド アプリケーション。** クラウド ベースのシステムおよび分散システムでは一般的に、部分的な障害のリスクがあります。 クライアントとサービスは別のプロセス (コンテナー) であるため、サービスが、クライアントの要求に迅速に応答できないことがあります。 たとえば、部分的な障害またはメンテナンスのためにサービスが停止したり、サービスが過負荷状態で要求に対する応答が非常に遅くなったり、または、単にネットワークの問題のために短時間アクセスできない場合があります。 したがって、クラウド ベースのアプリケーションはそのような障害を受け入れ、そのような障害に対応するための戦略を用意する必要があります。 これらの戦略には、再試行ポリシー (メッセージの再送信または要求を再試行) を含めることができ、繰り返しの要求の急増を回避する遮断器パターンを実装できます。 基本的には、クラウドベースのアプリケーションは、回復メカニズムを搭載している必要があります。カスタム メカニズムまたはオーケストレーターやサービス バスからの高レベルのフレームワークなどのクラウド インフラストラクチャに基づくメカニズムがあります。

**セキュリティ。** コンテナーとマイクロサービスによる新しい世界では、新たな脆弱性が公開される可能性があります。 基本的なアプリケーションのセキュリティは、認証および承認を基にし、これらを実装するいくつかの方法が存在します。 ただし、コンテナーのセキュリティには、追加の主要コンポーネントが含まれ、その結果を本質的により安全なアプリケーションになります。 コンテナー アプリケーションを構築するための重要な要素は、他のアプリケーションやシステムとの通信を安全に行うことです。多くの場合このためには、資格情報、トークン、パスワード、およびその他の種類の機密情報 (通常はアプリケーション シークレットと呼ばれます) が必要です。 セキュリティで保護されたソリューションは、送信中の機密情報の暗号化、保存時の機密情報の暗号化、アプリケーションで使用されるときに機密情報が誤って漏洩することの防止など、セキュリティのベスト プラクティスに従う必要があります。 これらの機密情報は、別の場所を安全に保管して維持する必要があります。 セキュリティを強化するために、選択したオーケストレーターのインフラストラクチャ、または Azure Key Vault などクラウド インフラストラクチャおよび使用時のアプリケーション コードの提供方法を活用できます。

**オーケストレーター。** Azure Container Service (Kubernetes、Mesos DC/OS、Docker Swarm) および Azure Service Fabric で提供されるようなコンテナーベースのオーケストレーターは、実稼働の準備ができたマイクロサービスベースのアプリケーション、および非常に複雑で拡張性のニーズがあり、絶えず進化しているマルチコンテナー アプリケーションに不可欠なものになっています。 このガイドでは、オーケストレーターの概要と、マイクロサービスベースおよびコンテナーベースのソリューションでのその役割を紹介しました。 アプリケーションで複雑なコンテナー化されたアプリケーションに移行する必要がある場合は、オーケストレーターについて学習するための追加のリソースを探すと役に立ちます。

>[!div class="step-by-step"]
>[前へ](secure-net-microservices-web-applications/azure-key-vault-protects-secrets.md)