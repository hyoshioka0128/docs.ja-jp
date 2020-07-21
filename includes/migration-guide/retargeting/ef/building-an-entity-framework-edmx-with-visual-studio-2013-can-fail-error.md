---
ms.openlocfilehash: c5099f610569f7788bb829a2153006d20d8a4ea2
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85615686"
---
### <a name="building-an-entity-framework-edmx-with-visual-studio-2013-can-fail-with-error-msb4062-if-using-the-entitydeploysplit-or-entityclean-tasks"></a>Visual Studio 2013 で Entity Framework edmx をビルドすると、EntityDeploySplit または EntityClean タスクを使用している場合、エラー MSB4062 で失敗することがある

#### <a name="details"></a>説明

MSBuild 12.0 ツール (Visual Studio 2013 に含まれる) は、MSBuild ファイルの位置を変更したため、古い Entity Framework のターゲット ファイルは無効になります。 その結果、`EntityDeploySplit` および `EntityClean` タスクは、`Microsoft.Data.Entity.Build.Tasks.dll` を見つけられないために失敗します。 このエラーは、ツールセット (MSBuild/VS) の変更によるものであり、.NET Framework の変更によるものではないことに注意してください。 開発者ツールをアップグレードしたときにのみ発生し、.NET Framework をアップグレード下だけでは発生しません。

#### <a name="suggestion"></a>提案される解決策

Entity Framework のターゲット ファイルは、.NET Framework 4.6 以降の新しい MSBuild レイアウトで機能するように修正されます。 このバージョンの Framework にアップグレードすることで、この問題は修正されます。 または、[この回避策](https://stackoverflow.com/a/24249247/131944)を使用して、ターゲット ファイルに直接パッチを当てることができます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.5.1       |
| 種類    | 再ターゲット中 |
