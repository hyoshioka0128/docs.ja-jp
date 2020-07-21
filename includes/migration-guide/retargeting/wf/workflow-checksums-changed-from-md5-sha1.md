---
ms.openlocfilehash: 72d48d1daa85b6891c122f2fcc5279642253b926
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614836"
---
### <a name="workflow-checksums-changed-from-md5-to-sha1"></a>ワークフローのチェックサムが MD5 から SHA1 に変更

#### <a name="details"></a>説明

Visual Studio によるデバッグをサポートするために、ワークフロー ランタイムによって、ハッシュ アルゴリズムを使用してワークフロー インスタンスのチェックサムが生成されます。 .NET Framework 4.6.2 以前のバージョンでは、ワークフロー チェックサムのハッシュで MD5 アルゴリズムが使用され、FIPS 対応システムで問題が発生していました。 .NET Framework 4.7 以降、アルゴリズムは SHA1 になります。 コードによってチェックサムが永続化されている場合、互換性がありません。

#### <a name="suggestion"></a>提案される解決策

チェックサム エラーに起因してコードでワークフロー インスタンスを読み込めない場合、`AppContext` スイッチ &quot;Switch.System.Activities.UseMD5ForWFDebugger&quot; を true に設定してみてください。下のコードをご覧ください。

```csharp
System.AppContext.SetSwitch("Switch.System.Activities.UseMD5ForWFDebugger", true);
```

または、次のように構成します。

```xml
<configuration>
  <runtime>
    <AppContextSwitchOverrides value="Switch.System.Activities.UseMD5ForWFDebugger=true" />
  </runtime>
</configuration>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7         |
| 種類    | 再ターゲット中 |
