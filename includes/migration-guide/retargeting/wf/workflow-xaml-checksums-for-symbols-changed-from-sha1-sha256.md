---
ms.openlocfilehash: 946e71f2f466664c8f9fcf4811288ce693a872eb
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616270"
---
### <a name="workflow-xaml-checksums-for-symbols-changed-from-sha1-to-sha256"></a>ワークフロー XAML のシンボルのチェックサムが SHA1 から SHA256 に変更

#### <a name="details"></a>説明

Visual Studio によるデバッグをサポートするために、ワークフロー ランタイムによって、ハッシュ アルゴリズムを使用してワークフロー XAML ファイルのチェックサムが生成されます。 .NET Framework 4.6.2 以前のバージョンでは、ワークフロー チェックサムのハッシュで MD5 アルゴリズムが使用され、FIPS 対応システムで問題が発生していました。 .NET Framework 4.7 以降では、既定のアルゴリズムが SHA1 に変更されました。 .NET Framework 4.8 以降では、既定のアルゴリズムが SHA256 に変更されました。

#### <a name="suggestion"></a>提案される解決策

チェックサム エラーに起因して、コードでワークフロー インスタンスを読み込めないか、適切なシンボルを見つけられない場合、`AppContext` スイッチ "Switch.System.Activities.UseSHA1HashForDebuggerSymbols" を `true` に設定してみてください。 コードは次のとおりです。

```csharp
System.AppContext.SetSwitch("Switch.System.Activities.UseSHA1HashForDebuggerSymbols", true);
```

または、次のように構成します。

```xml
<configuration>
  <runtime>
    <AppContextSwitchOverrides value="Switch.System.Activities.UseSHA1HashForDebuggerSymbols=true" />
  </runtime>
</configuration>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.8         |
| 種類    | 再ターゲット中 |
