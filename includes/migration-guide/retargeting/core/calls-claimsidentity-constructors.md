---
ms.openlocfilehash: b88f7d4a17f885b687d99ab9410a56039e176080
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614637"
---
### <a name="calls-to-claimsidentity-constructors"></a>ClaimsIdentity コンストラクターを呼び出す

#### <a name="details"></a>説明

.NET Framework 4.6.2 以降、<xref:System.Security.Claims.ClaimsIdentity> コンストラクターと <xref:System.Security.Principal.IIdentity?displayProperty=fullName> パラメーターの組み合わせで <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=fullName> プロパティが設定されるしくみに変更があります。 <xref:System.Security.Principal.IIdentity?displayProperty=fullName> 引数が <xref:System.Security.Claims.ClaimsIdentity> オブジェクトで、その <xref:System.Security.Claims.ClaimsIdentity> オブジェクトの <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=fullName> プロパティが `null` ではない場合、<xref:System.Security.Claims.ClaimsIdentity.Clone> メソッドを使用して <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=fullName> プロパティがアタッチされます。 Framework 4.6.1 以前のバージョンでは、<xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=fullName> プロパティは既存の参照として付けられます。この変更によって、.NET Framework 4.6.2 以降、新しい <xref:System.Security.Claims.ClaimsIdentity> オブジェクトの <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=fullName> プロパティはコンストラクターの <xref:System.Security.Principal.IIdentity?displayProperty=fullName> 引数の <xref:System.Security.Claims.ClaimsIdentity.Actor?displayProperty=fullName> プロパティとは等しくなくなります。 .NET Framework 4.6.1 以前のバージョンでは、等しくなります。

#### <a name="suggestion"></a>提案される解決策

この動作が望ましくない場合、アプリケーション構成ファイルで `Switch.System.Security.ClaimsIdentity.SetActorAsReferenceWhenCopyingClaimsIdentity` スイッチを `true` に設定して以前の動作を復元することができます。 この場合、web.config ファイルの `<runtime>` セクションに次を追加します。

```xml
<configuration>
  <runtime>
    <AppContextSwitchOverrides value="Switch.System.Security.ClaimsIdentity.SetActorAsReferenceWhenCopyingClaimsIdentity=true" />
  </runtime>
</configuration>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Security.Principal.IIdentity)>
- <xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Security.Principal.IIdentity,System.Collections.Generic.IEnumerable{System.Security.Claims.Claim})>
- <xref:System.Security.Claims.ClaimsIdentity.%23ctor(System.Security.Principal.IIdentity,System.Collections.Generic.IEnumerable{System.Security.Claims.Claim},System.String,System.String,System.String)>
