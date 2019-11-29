---
title: Docker コンテナー用 .NET Framework を選択するタイミング
description: '.NET マイクロサービス: コンテナー化された .NET アプリケーションのアーキテクチャ | Docker コンテナー用 .NET Framework を選択するタイミング'
ms.date: 01/07/2019
ms.openlocfilehash: 9e5b18e8e3482eb86c0d9dea5de56fb12f9d6256
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73966890"
---
# <a name="when-to-choose-net-framework-for-docker-containers"></a>Docker コンテナー用 .NET Framework を選択するタイミング

.NET Core は新しいアプリケーションとアプリケーション パターンには大きな利点がありますが、既存の多くのシナリオでは引き続き .NET Framework が適切な選択肢となります。

## <a name="migrating-existing-applications-directly-to-a-windows-server-container"></a>既存アプリケーションを Windows Server コンテナーに直接移行する

マイクロサービスを作成していない場合は、デプロイメントを簡略にするためだけでも Docker コンテナーを使用できます。 たとえば、Docker に対する DevOps ワークフローを改善したいとします。コンテナーを使用すると、適切に分離されたテスト環境を確保でき、運用環境に移行したときに依存関係が失われて生じるデプロイメントの問題も解消できます。 このようなケースでは、単体のアプリケーションをデプロイする場合でも、現在の .NET Framework アプリケーションのために Docker および Windows コンテナーを使用するメリットがあります。

このシナリオのほとんどのケースでは、既存アプリケーションを .NET Core に移行する必要は生じません。従来の .NET Framework を含む Docker コンテナーを使用できます。 ただし、ASP.NET Core で新しいサービスを作成するなど、既存のアプリケーションを拡張する際には、代わりに .NET Core を使用することをお勧めします。

## <a name="using-third-party-net-libraries-or-nuget-packages-not-available-for-net-core"></a>NET Core で使用できないサードパーティ製の .NET ライブラリや NuGet パッケージを使用する

サードパーティ ライブラリでは [.NET Standard](../../../standard/net-standard.md) の採用が迅速に進められています。これにより、.NET Core を含むすべての種類の .NET でコードを共有できるようになります。 .NET Standard Library 2.0 以上では、異なるフレームワーク間での API サーフェスの互換性はかなり高くなっています。また、.NET Core 2.x では、アプリケーションは既存の .NET Framework ライブラリを直接参照することもできます ([.NET Standard 2.0 をサポートする .NET Framework 4.6.1](https://github.com/dotnet/standard/blob/master/docs/planning/netstandard-2.0/README.md#net-framework-461-supporting-net-standard-20) に関するページを参照)。

さらに、[Windows 互換機能パック](../../../core/porting/windows-compat-pack.md)は 2017 年 11 月にリリースされ、Windows の .NET Standard 2.0 で利用可能な API サーフェスを拡張しました。 このパックでは、最小限の変更か、または変更を伴わずに、.NET Standard 2.x のほとんどの既存コードを再コンパイルして、Windows 上で実行できます。

ただし、.NET Standard 2.0 および .NET Core 2.1 以降の進歩が並外れているとしても、特定の NuGet パッケージが実行に Windows を必要とし、.NET Core をサポートしていないというケースはあります。 これらのパッケージがアプリケーションに不可欠な場合は、Windows コンテナー上で .NET Framework を使用する必要があります。

## <a name="using-net-technologies-not-available-for-net-core"></a>.NET Core で使用できない .NET テクノロジを使用する

一部の .NET Framework テクノロジは、現在の .NET Core バージョン (このドキュメント作成時点のバージョン 2.2) では利用できません。 .NET Core の今後のリリース (.NET Core 2.x) で使用可能になるものもありますが、それ以外は .NET Core の対象となる新しいアプリケーション パターンには適用されず、使用可能にならない可能性があります。

.NET Core 2.x で利用できないテクノロジのほとんどを次に示します。

- ASP.NET Web フォーム。 このテクノロジは .NET Framework のみで利用できます。 現時点では、ASP.NET Web フォームを .NET Core で使用できるようにする予定はありません。

- WCF サービス。 .NET Core から WCF サービスを使用する [WCF クライアント ライブラリ](https://github.com/dotnet/wcf)が利用可能な場合でも、2017 年半ばの時点では、WCF サーバーの実装は .NET Framework でのみ可能です。 このシナリオは、.NET Core の将来のリリースで検討対象となる可能性があります。また、[Windows 互換機能パック](../../../core/porting/windows-compat-pack.md)への組み込みが検討されている API もあります。

- ワークフロー関連サービス。 Windows Workflow Foundation (WF)、ワークフロー サービス (1 つのサービスに WCF と WF) および WCF Data Services (旧称: ADO.NET Data Services) は、NET Framework でのみ使用できます。 現在、この機能を .NET Core に含める計画はありません。

公式の [.NET Core ロードマップ](https://github.com/aspnet/Home/wiki/Roadmap)に記載されているテクノロジに加え、他の機能が .NET Core に移植される可能性があります。 完全な一覧については、CoreFX GitHub サイトで [port-to-core](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aport-to-core) のタグが付いた項目をご覧ください。 この一覧は Microsoft がこれらのコンポーネントを .NET Core に提供することを約束するものではなく、単にコミュニティの要望に応じた項目であることに注意してください。 前述のコンポーネントが気になる場合には、GitHub でのディスカッションに参加して意見を述べることを検討してください。 また、何か足りないと感じた場合は、[CoreFX リポジトリで新しい案件を作成](https://github.com/dotnet/corefx/issues/new)してください。

.NET Core 3 (この記事の執筆時点では、準備中) に多数の既存の .NET Framework API サポートが含まれたとしても、これらはデスクトップ指向なので、現在のコンテナーの世界では使用されません。

## <a name="using-a-platform-or-api-that-does-not-support-net-core"></a>.NET Core をサポートしていないプラットフォームまたは API を使用する

Microsoft やサードパーティ製のプラットフォームの中には、.NET Core をサポートしないものもあります。 たとえば、一部の Azure サービスでは、.NET Core ではまだ使用できない SDK が提供されます。 すべての Azure サービスはいずれは .NET Core を使用するようになるため、これは一時的な状態です。 たとえば、[Azure DocumentDB SDK for .NET Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) は、2016 年 11 月 16 日にプレビューとしてリリースされましたが、現在は安定したバージョンである一般公開 (GA) になっています。

この間、Azure のプラットフォームまたはサービスがクライアント API で .NET Core をまだサポートしていない場合は、Azure サービスまたはクライアント SDK の同等の REST API を .NET Framework で使用できます。

### <a name="additional-resources"></a>その他の技術情報

- **.NET Core ガイド** \
  [https://docs.microsoft.com/dotnet/core/index](../../../core/index.md)

- **.NET Framework から .NET Core への移植** \
  [https://docs.microsoft.com/dotnet/core/porting/index](../../../core/porting/index.md)

- **Docker 上の .NET Core のガイド** \
  [https://docs.microsoft.com/dotnet/core/docker/introduction](../../../core/docker/introduction.md)

- **.NET コンポーネントの概要** \
  [https://docs.microsoft.com/dotnet/standard/components](../../../standard/components.md)

>[!div class="step-by-step"]
>[前へ](net-core-container-scenarios.md)
>[次へ](container-framework-choice-factors.md)
