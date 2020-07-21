---
ms.openlocfilehash: ec6724ab378dd614c55a024ede18d997d27be3a3
ms.sourcegitcommit: 34dc3c0d0d0a1cc418abff259d9daa8078d00b81
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2020
ms.locfileid: "79549600"
---
### <a name="target-framework-net-framework-support-dropped"></a>ターゲット フレームワーク: .NET Framework のサポートが廃止されました

ASP.NET Core 3.0 以降、.NET Framework はサポート対象外のターゲット フレームワークになりました。

#### <a name="change-description"></a>変更の説明

.NET Framework 4.8 は、.NET Framework の最後のメジャー バージョンです。 新しい ASP.NET Core アプリは .NET Core で構築する必要があります。 .NET Core 3.0 リリース以降、ASP.NET Core 3.0 は .NET Core の一部になっていると考えることができます。

.NET Framework で ASP.NET Core を使用しているお客様は、[2.1 LTS リリース](https://dotnet.microsoft.com/download/dotnet-core/2.1)を使用して完全にサポートされた状態で続行できます。 2\.1 のサポートとサービスは、2021 年 8 月 21 日まで継続されます。 [.NET サポート ポリシー](https://dotnet.microsoft.com/platform/support-policy)に従い、この日付は LTS リリースの宣言から 3 年後です。 **.NET Framework での**  ASP.NET Core 2.1 パッケージのサポートは、[他のパッケージ ベースの ASP.NET フレームワークのサービス ポリシー](https://dotnet.microsoft.com/platform/support/policy/aspnet)と同様に、無制限に延長されます。

.NET Framework から .NET Core への移植の詳細については、[.NET Core への移植](~/docs/core/porting/index.md)に関するページを参照してください。

`Microsoft.Extensions` パッケージ (ログ記録、依存関係の挿入、構成など) と Entity Framework Core は影響を受けません。 .NET Standard はそれらで引き続きサポートされます。

この変更の目的の詳細については、[元のブログ記事](https://devblogs.microsoft.com/aspnet/a-first-look-at-changes-coming-in-asp-net-core-3-0/)をご覧ください。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="old-behavior"></a>以前の動作

ASP.NET Core アプリは .NET Core または .NET Framework で実行できました。

#### <a name="new-behavior"></a>新しい動作

ASP.NET Core アプリは .NET Core でのみ実行できます。

#### <a name="recommended-action"></a>推奨アクション

次のうちの 1 つの行為を行ってください：

- ASP.NET Core 2.1 でアプリを保持します。
- アプリと依存関係を .NET Core に移行します。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

なし

<!-- 

#### Affected APIs

Not detectable via API analysis

-->
