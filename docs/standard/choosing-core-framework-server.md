---
title: サーバー アプリ用 .NET Core と .NET Framework の選択
description: サーバー アプリを構築するときに使用する .NET の実装を決定するのに役立つガイドです。
author: cartermp
ms.date: 04/28/2020
ms.openlocfilehash: 30157276bce53ed44dca5b660172e5556dab14f8
ms.sourcegitcommit: 1cb64b53eb1f253e6a3f53ca9510ef0be1fd06fe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82507443"
---
# <a name="net-core-vs-net-framework-for-server-apps"></a>サーバー アプリでの .NET Core または .NET Framework の使用

サーバー側のアプリをビルドするときにサポートされる実装は、.NET Framework と .NET Core の 2 つです。 この 2 つは多数の同じコンポーネントを共有しているため、両者でコードを共有できます。 ただし、2 つには基本的な違いがあり、どちらを選択するかは実行内容によって決まります。 この記事では、それぞれを使用するタイミングに関するガイダンスを提供します。

次のような場合、サーバー アプリケーションには .NET Core を使用します。

- クロスプラット フォームが必要である。
- マイクロサービスが対象である。
- Docker コンテナーを使用している。
- 高パフォーマンスでスケーラブルなシステムが必要である。
- 1 つのアプリケーションに複数の .NET バージョンが必要である。

次のような場合、サーバー アプリケーションには .NET Framework を使用します。

- 現在、アプリで .NET Framework を使用している (移行ではなく拡張することをお勧めします)。
- アプリが .NET Core で使用できないサードパーティ製の .NET ライブラリや NuGet パッケージを使用している。
- アプリで、.NET Core で使用できない .NET テクノロジを使用している。
- アプリで、.NET Core をサポートしていないプラットフォームを使用している。 .NET Core は Windows、macOS、Linux でサポートされています。

## <a name="when-to-choose-net-core"></a>どのような場合に .NET Core を選択すべきか

以下のセクションで、前述の .NET Core を選択する理由について詳しく説明します。

### <a name="cross-platform-needs"></a>クロスプラットフォームの必要性

複数のプラットフォーム (Windows、Linux、macOS ) で実行する必要があるアプリケーション (Web/サービス) の場合は、.NET Core を使用します。

.NET Core は、開発ワークステーションとして前述のオペレーティング システムをサポートしています。 Visual Studio では、Windows および macOS 用の統合開発環境 (IDE) が用意されています。 また、macOS、Linux、および Windows 上で動作する Visual Studio Code も使用できます。 Visual Studio Code は、IntelliSense、デバッグなどの .NET Core をサポートしています。 Sublime、Emacs、VI など、ほとんどのサード パーティ製エディターは、.NET Core で動作します。 これらのサード パーティ製エディターでは、[Omnisharp](https://www.omnisharp.net/) を使用して、エディターを IntelliSense にします。 また、コード エディターをまったく使用せずに、サポートされているすべてのプラットフォームで利用可能な [.NET Core CLI](../core/tools/index.md) を直接使用することもできます。

### <a name="microservices-architecture"></a>マイクロサービス アーキテクチャ

マイクロサービス アーキテクチャでは、サービスの境界を越えて、複数のテクノロジを組み合わせて使用できます。 このテクノロジの組み合わせによって、他のマイクロサービスやサービスと連携する新しいマイクロサービスに .NET Core を段階的に採用することができます。 たとえば、.NET Framework、Java、Ruby などのモノリシックなテクノロジを使用して開発されたマイクロサービスまたはサービスを組み合わせることができます。

使用できるインフラストラクチャ プラットフォームは多数あります。 [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) は、大規模で複雑なマイクロサービス システム向けに設計されています。 [Azure App Service](https://azure.microsoft.com/services/app-service/) は、ステートレス マイクロサービスに推奨されます。 「[コンテナー](#containers)」セクションで説明するように、Docker ベースのマイクロサービスの代替手段は、どのような種類のマイクロサービスのアプローチにも適しています。 これらすべてのプラットフォームでは .NET Core がサポートされるため、マイクロサービスをホストするには最適です。

マイクロサービス アーキテクチャの詳細については、「[.NET マイクロサービス:コンテナー化された .NET アプリケーションのアーキテクチャ](../architecture/microservices/index.md)」を参照してください。

### <a name="containers"></a>コンテナー

通常、コンテナーは、マイクロサービス アーキテクチャと組み合わせて使用されます。 コンテナーは、任意のアーキテクチャ パターンに従う Web アプリやサービスをコンテナー化するためにも使用できます。 Windows コンテナーで .NET Framework を使用できますが、モジュール方式で軽量である .NET Core はコンテナーに適しています。 コンテナーを作成して展開する場合、そのイメージのサイズは .NET Framework より .NET Core の方がはるかに小さくなります。 また、クロスプラットフォームであるため、Linux Docker コンテナーなどにサーバー アプリを展開することができます。

Docker コンテナーは、オンプレミスの Linux または Windows インフラストラクチャ、または [Azure Kubernetes Service](https://azure.microsoft.com/services/kubernetes-service/) などのクラウド サービスでホストできます。 Azure Kubernetes Service は、コンテナーベースのアプリケーションの管理、調整、およびスケールをクラウドで行うことができます。

### <a name="high-performance-and-scalable-systems"></a>高パフォーマンスでスケーラブルなシステム

システムで考えられる最高のパフォーマンスとスケーラビリティが必要な場合、NET Core と ASP.NET Core が最適です。 .NET は Windows Server および Linux 向けの高パフォーマンスなサーバー ランタイムであり、[TechEmpower のベンチマーク](https://www.techempower.com/benchmarks/#hw=ph&test=plaintext)で高パフォーマンスの Web フレームワークとして上位に評価されました。

何百ものマイクロサービスが実行される可能性があるマイクロサービス アーキテクチャの場合は特に、パフォーマンスとスケーラビリティが重要です。 ASP.NET Core では、少数のサーバー/仮想マシン (VM) 数でシステムが動作します。 サーバー/VM が減るので、インフラストラクチャとホスティングにかかるコストを節約できます。

### <a name="side-by-side-net-versions-per-application-level"></a>アプリケーション レベルでの複数の .NET バージョン

複数バージョンの .NET に依存するアプリケーションをインストールする場合は、.NET Core をお勧めします。 .NET Core では、同じコンピューター上に、複数バージョンの .NET Core ランタイムをインストールできます。 サイド バイ サイド インストールによって、同じサーバー上で、使用する .NET Core バージョンが異なる複数のサービスを実行できるようになります。 また、アプリケーションのアップグレードと IT 運用に関係するリスクとコストを軽減できます。

.NET Framework では、複数のバージョンをインストールできません。 これは Windows のコンポーネントであり、1 台のコンピューターには同時に 1 つのバージョンしか存在させることができません。 .NET Framework の前のバージョンは、各バージョンに置き換えられます。 新しいバージョンの .NET Framework を対象とする新しいアプリをインストールすると、以前のバージョンが置き換えられてしまうために、そのコンピューターで実行されている既存のアプリが破損してしまう場合があります。

## <a name="when-to-choose-net-framework"></a>どのような場合に .NET Framework を選択すべきか

新しいアプリケーションやアプリケーション パターンの場合は特に .NET Core の利点があります。 ただし、既存の多くのシナリオで .NET Framework が一般的に選択されているため、すべてのサーバー アプリケーションで .NET Framework を .NET Core で置き換えることはできません。

### <a name="current-net-framework-applications"></a>現在の .NET Framework アプリケーション

ほとんどの場合、既存のアプリケーションを .NET Core に移行する必要はありません。 ASP.NET Core で新しい Web サービスを作成するなど、既存のアプリケーションを拡張する際には、代わりに .NET Core を使用することをお勧めします。

### <a name="aspnet-core-on-net-framework"></a>.NET Framework 上の ASP.NET Core

.NET Framework での ASP.NET Core のサポートの詳細については、[.NET Core のサポート ポリシー](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)に関するページを参照してください。

### <a name="third-party-libraries-or-nuget-packages-not-available-for-net-core"></a>NET Core でサードパーティ製のライブラリや NuGet パッケージを使用できない

ライブラリは、短期間で .NET Standard を採用しています。 .NET Standard を使用すると、.NET Core を含め、すべての .NET 実装全体でコードを共有できます。 .NET Standard 2.0 を使用すれば、さらに簡単です。

- API サーフェスがはるかに大きくなりました。
- .NET Framework 互換モードが導入されました。

  この互換モードにより、.NET Standard および .NET Core プロジェクトは .NET Framework ライブラリを参照できます。 互換モードの詳細については、「[Announcing .NET Standard 2.0](https://devblogs.microsoft.com/dotnet/announcing-net-standard-2-0/)」(.NET Standard 2.0 のお知らせ) を参照してください。

ライブラリまたは NuGet パッケージが、.NET Standard や .NET Core にないテクノロジを使用している場合にのみ、.NET Framework を使用する必要があります。

### <a name="net-technologies-not-available-for-net-core"></a>.NET Core で使用できない .NET のテクノロジ

一部の .NET Framework テクノロジは .NET Core では使用できません。 その一部は、.NET Core の今後のリリースで使用できるようになる可能性があります。 それ以外は .NET Core の対象となる新しいアプリケーション パターンには適用されず、使用可能にならない可能性があります。 .NET Core にはない最も一般的なテクノロジを、以下のリストに示します。

- ASP.NET Web フォーム アプリケーション:ASP.NET Web フォームは、.NET Framework でのみ使用できます。 ASP.NET Core は、ASP.NET Web フォームに使用できません。 ASP.NET Web フォームが .NET Core で使用できるようになる予定はありません。

- ASP.NET Web ページ アプリケーション:ASP.NET Web ページは、ASP.NET Core に含まれていません。

- WCF サービスの実装。 現在、.NET Core から WCF サービスを利用する [WCF クライアント ライブラリ](https://github.com/dotnet/wcf)があっても、WCF サーバーの実装は .NET Framework でのみ利用可能です。 このシナリオは .NET Core の現在の計画に含まれていませんが、将来的には検討中です。

- ワークフローに関連するサービス:Windows Workflow Foundation (WF)、ワークフロー サービス (1 つのサービスに WCF と WF) および WCF Data Services (旧称: ADO.NET Data Services) は、NET Framework でのみ使用できます。 これらのテクノロジが .NET Core で使用できるようになる予定はありません。

- 言語のサポート:Visual Basic と F# は現在 .NET Core でサポートされていますが、サポートされないプロジェクトの種類もあります。 サポートされるプロジェクト テンプレートの一覧については、[dotnet new のテンプレート オプション](../core/tools/dotnet-new.md#arguments)に関するセクションを参照してください。

### <a name="platform-doesnt-support-net-core"></a>.NET Core がプラットフォームでサポートされない

Microsoft やサードパーティ製のプラットフォームの中には、.NET Core をサポートしないものもあります。 一部の Azure サービスでは、.NET Core ではまだ使用できない SDK が提供されます。 すべての Azure サービスでは .NET Core を使用しているために、これは過渡的な状況です。 その間、クライアント SDK の代わりに同等の REST API を使用できます。

## <a name="see-also"></a>関連項目

- [ASP.NET と ASP.NET Core の選択](/aspnet/core/choose-aspnet-framework)
- [.NET Framework を対象とする ASP.NET Core](/aspnet/core/introduction-to-aspnet-core#aspnet-core-targeting-net-framework)
- [ターゲット フレームワーク](frameworks.md)
- [.NET Core のガイド](../core/index.yml)
- [.NET Framework から .NET Core への移植](../core/porting/index.md)
- [.NET および Docker の概要](../core/docker/introduction.md)
- [.NET コンポーネントの概要](components.md)
- [.NET マイクロサービス:コンテナー化された .NET アプリケーションのアーキテクチャ](../architecture/microservices/index.md)
