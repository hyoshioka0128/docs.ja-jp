---
ms.openlocfilehash: 424e8ff704b888aa3d2c1254ac712da4034f59b8
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616120"
---
### <a name="obsoleteattribute-exports-as-both-obsoleteattribute-and-deprecatedattribute-in-winmd-scenarios"></a>ObsoleteAttribute は、WinMD のシナリオで、ObsoleteAttribute と DeprecatedAttribute の両方としてエクスポートする

#### <a name="details"></a>説明

Windows メタデータ ライブラリ (.winmd ファイル) を作成するとき、<xref:System.ObsoleteAttribute?displayProperty=fullName> 属性は <xref:System.ObsoleteAttribute?displayProperty=fullName> および [Windows.Foundation.DeprecatedAttribute](https://docs.microsoft.com/uwp/api/windows.foundation.metadata.deprecatedattribute) の両方としてエクスポートされます。

#### <a name="suggestion"></a>提案される解決策

<xref:System.ObsoleteAttribute?displayProperty=fullName> 属性を使用する既存のソース コードを再コンパイルするとき、C++/CX または JavaScript からそのコードを使用するとき、警告が生成されることがあります。マネージド アセンブリのコードを記述するとき、<xref:System.ObsoleteAttribute?displayProperty=fullName> と [Windows.Foundation.DeprecatedAttribute](https://docs.microsoft.com/uwp/api/windows.foundation.metadata.deprecatedattribute) の両方を適用することはお勧めしません。ビルドで警告が生成されることがあります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.5.1       |
| 種類    | 再ターゲット中 |
