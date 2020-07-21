---
ms.openlocfilehash: c5a061dffa1deb66e1769d6ec70dfa2155ac6a31
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85615709"
---
### <a name="calling-createdefaultauthorizationcontext-with-a-null-argument-has-changed"></a>null 引数を指定した CreateDefaultAuthorizationContext の呼び出しが変更されました

#### <a name="details"></a>説明

null の authorizationPolicies 引数を指定した <xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext(System.Collections.Generic.IList{System.IdentityModel.Policy.IAuthorizationPolicy})?displayProperty=fullName> の呼び出しによって返される <xref:System.IdentityModel.Policy.AuthorizationContext?displayProperty=fullName> の実装が、.NET Framework 4.6 で変更されました。

#### <a name="suggestion"></a>提案される解決策

まれに、カスタム認証を使用する WCF アプリの動作に違いが生じる可能性があります。 このような場合は、2 つの方法のいずれかで、以前の動作を復元できます。

- 4\.6 よりも前のバージョンの .NET Framework を対象とするようにアプリを再コンパイルする。 IIS でホストされるサービスでは、`<httpRuntime targetFramework="x.x">` の要素を使用して、以前のバージョンの .NET Framework を対象とするようにします。
- app.config ファイルの `<appSettings>` セクションに以下の行を追加します。

    ```xml
    <add key="appContext.SetSwitch:Switch.System.IdentityModel.EnableCachedEmptyDefaultAuthorizationContext" value="true" />
    ```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.IdentityModel.Policy.AuthorizationContext.CreateDefaultAuthorizationContext(System.Collections.Generic.IList{System.IdentityModel.Policy.IAuthorizationPolicy})?displayProperty=nameWithType>
