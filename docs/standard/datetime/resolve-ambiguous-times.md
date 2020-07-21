---
title: '方法: あいまいな時刻を解決する'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], ambiguous time
- ambiguous time [.NET Framework]
ms.assetid: 2cf5fb25-492c-4875-9245-98cac8348e97
ms.openlocfilehash: ad69c0984a9d8c01ebd2198486cd0f6492a6116e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281506"
---
# <a name="how-to-resolve-ambiguous-times"></a>方法: あいまいな時刻を解決する

あいまいな時刻は複数の世界協定時刻 (UTC) にマップされる時刻です。 あいまいな時刻は、あるタイム ゾーンの夏時間から標準時間に移行する際など、時計の時刻を前に戻すときに発生します。 あいまいな時刻を処理する場合は、次のいずれかの操作を行います。

- 時刻が UTC にどのようにマップされるかを想定します。 たとえば、あいまいな時刻は常にタイム ゾーンの標準時刻で表されると想定できます。

- あいまいな時刻が、ユーザーによって入力されたデータ項目である場合は、あいまいさの解決をユーザーに任せることができます。

このトピックでは、タイムゾーンの標準時刻を表すと想定して、あいまいな時刻を解決する方法について説明します。

### <a name="to-map-an-ambiguous-time-to-a-time-zones-standard-time"></a>あいまいな時刻をタイム ゾーンの標準時刻にマップするには

1. メソッドを呼び出して <xref:System.TimeZoneInfo.IsAmbiguousTime%2A> 、時刻があいまいであるかどうかを確認します。

2. 時刻があいまいな場合は、タイム <xref:System.TimeSpan> ゾーンのプロパティによって返されたオブジェクトから時刻を減算し <xref:System.TimeZoneInfo.BaseUtcOffset%2A> ます。

3. `static`( `Shared` Visual Basic .net で) メソッドを呼び出して、 <xref:System.DateTime.SpecifyKind%2A> UTC の日付と時刻の値の <xref:System.DateTime.Kind%2A> プロパティをに設定し <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> ます。

## <a name="example"></a>例

次の例は、ローカルタイムゾーンの標準時刻を表すと想定して、あいまいな時刻を UTC に変換する方法を示しています。

[!code-csharp[System.TimeZone2.Concepts#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#10)]
[!code-vb[System.TimeZone2.Concepts#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#10)]

この例は、渡された `ResolveAmbiguousTime` 値があいまいであるかどうかを判断するという名前のメソッドで構成されてい <xref:System.DateTime> ます。 値があいまいな場合、メソッドは対応する <xref:System.DateTime> UTC 時刻を表す値を返します。 メソッドは、ローカルタイムゾーンのプロパティの値をローカル時刻から減算することによって、この変換を処理し <xref:System.TimeZoneInfo.BaseUtcOffset%2A> ます。

通常、あいまいな時刻は、メソッドを呼び出して、 <xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A> <xref:System.TimeSpan> あいまいな時刻の UTC オフセットを含むオブジェクトの配列を取得することによって処理されます。 しかし、この例は、あいまいな時刻は常にタイム ゾーンの標準時刻にマップされるという想定に基づいています。 プロパティは、 <xref:System.TimeZoneInfo.BaseUtcOffset%2A> UTC とタイムゾーンの標準時刻の間のオフセットを返します。

この例では、ローカルタイムゾーンへのすべての参照は、プロパティを使用して行われ <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> ます。ローカルタイムゾーンは、オブジェクト変数に割り当てられることはありません。 メソッドを呼び出すと、 <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=nameWithType> ローカルタイムゾーンが割り当てられているオブジェクトが無効になるため、この方法をお勧めします。

## <a name="compiling-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- <xref:System> `using` ステートメント (C# コードでは必須) を使用して名前空間をインポートする。

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [方法: ユーザーがあいまいな時刻を解決できるようにする](let-users-resolve-ambiguous-times.md)
