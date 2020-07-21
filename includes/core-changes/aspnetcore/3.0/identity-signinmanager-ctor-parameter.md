---
ms.openlocfilehash: ed5a90063b8963d79f412ec1c5c0b9030f980f83
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/13/2020
ms.locfileid: "81275396"
---
### <a name="identity-signinmanager-constructor-accepts-new-parameter"></a>ID: SignInManager コンストラクターは新しいパラメーターを受け入れる

ASP.NET Core 3.0 以降、`SignInManager` コンストラクターに新しい `IUserConfirmation<TUser>` パラメーターが追加されました。 詳細については、[dotnet/aspnetcore#8356](https://github.com/dotnet/aspnetcore/issues/8356) を参照してください。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="reason-for-change"></a>変更理由

変更の動機は、ID での新しいメール/確認フローのサポートを追加するためでした。

#### <a name="recommended-action"></a>推奨アクション

手動で `SignInManager` を構築している場合は、`IUserConfirmation` の実装を提供するか、依存関係の挿入から 1 つを取得して提供します。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:Microsoft.AspNetCore.Identity.SignInManager%601.%23ctor%2A>

<!--

#### Affected APIs

`Overload:Microsoft.AspNetCore.Identity.SignInManager`1.#ctor`

-->
