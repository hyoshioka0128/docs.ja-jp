---
ms.openlocfilehash: c7500550cd9714a9788a7dea68af04823f000f7f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614794"
---
### <a name="stack-traces-obtained-when-using-portable-pdbs-now-include-source-file-and-line-information-if-requested"></a>ポータブル PDB の使用時に取得されるスタック トレースに、必要に応じてソース ファイルと行情報が含まれるようになった

#### <a name="details"></a>説明

.NET Framework 4.7.2 以降では、ポータブル PDB の使用時に取得されるスタック トレースに、要求に応じてソース ファイルと行情報が含まれます。 .NET Framework 4.7.2 より前のバージョンでは、明示的に要求された場合でもポータブル PDB の使用時にソース ファイルと行情報は利用できません。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.2 を対象とするアプリケーションでは、望ましくない場合、`app.config` ファイルの `<runtime>` セクションに以下を追加することで、ポータブル PDB の使用時にソース ファイルと行情報の選択を解除できます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Diagnostics.IgnorePortablePDBsInStackTraces=true" />
</runtime>
```

以前のバージョンの .NET Framework を対象とするが、.NET Framework 4.7.2 以降で実行するアプリケーションの場合は、`app.config` ファイルの `<runtime>` セクションに以下を追加することで、ポータブル PDB の使用時にソース ファイルと行情報を選択できます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Diagnostics.IgnorePortablePDBsInStackTraces=false" />
</runtime>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Diagnostics.StackTrace.%23ctor(System.Boolean)>
- <xref:System.Diagnostics.StackTrace.%23ctor(System.Exception,System.Boolean)>
- <xref:System.Diagnostics.StackTrace.%23ctor(System.Exception,System.Int32,System.Boolean)>
