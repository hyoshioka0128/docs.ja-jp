---
ms.openlocfilehash: e4d9efe7d2a06a1e501b070c23184dcd913dba71
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621284"
---
### <a name="persian-calendar-now-uses-the-hijri-solar-algorithm"></a>ペルシャ暦でイスラム暦の太陽アルゴリズムが使用されるようになった

#### <a name="details"></a>説明

.NET Framework 4.6 以降では、<xref:System.Globalization.PersianCalendar?displayProperty=fullName> クラスでイスラム暦の太陽アルゴリズムが使用されます。 <xref:System.Globalization.PersianCalendar?displayProperty=fullName> と他のカレンダーの間で日付を変換すると、.NET Framework 4.6 以降では、1800 年より前か 2023 年 (グレゴリオ暦) よりも後の日付について、わずかに異なる結果になることがあります。また、<xref:System.Globalization.PersianCalendar.MinSupportedDateTime?displayProperty=nameWithType> は <code>March 21, 0622</code> ではなく <code>March 22, 0622</code> になります。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.6 で PersianCalendar を使用するときには、一部の早い日付または遅い日付に若干の差が生じる場合があることに注意してください。 また、異なるバージョンの .NET Framework で実行する可能性のあるプロセス間で日付をシリアル化するときには、PersianCalendar の日付文字列として格納しないでください (これらの値が異なる場合があるため)。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.6|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Globalization.PersianCalendar?displayProperty=nameWithType></li></ul>|
