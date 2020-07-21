---
ms.openlocfilehash: 863e7035827537e0f943af05c2f0232029b99db8
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617193"
---
### <a name="entity-framework-version-must-match-the-net-framework-version"></a>Entity Framework バージョンは .NET Framework バージョンに一致する必要がある

#### <a name="details"></a>説明

Entity Framework (EF) のバージョンは、.NET Framework のバージョンと一致している必要があります。 .NET Framework 4.5 には、Entity Framework 5 をお勧めします。 .NET Framework 4.5 プロジェクトの EF 4.x に <xref:System.ComponentModel.DataAnnotations> に関する既知の問題がいくつかあります。 .NET Framework 4.5 では、これらは別のアセンブリに移動されたため、どの注釈を使用するかを決めるという問題があります。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.5 の場合、Entity Framework 5 にアップグレードする

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | Major       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |
