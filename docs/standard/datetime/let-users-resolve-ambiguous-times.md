---
title: '方法: ユーザーがあいまいな時刻を解決できるようにする'
ms.date: 04/10/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- time zones [.NET Framework], ambiguous time
- ambiguous time [.NET Framework]
ms.assetid: bca874ee-5b68-4654-8bbd-3711220ef332
ms.openlocfilehash: ac723738d80a2f686a5fcaf279cec791b3c58619
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281584"
---
# <a name="how-to-let-users-resolve-ambiguous-times"></a>方法: ユーザーがあいまいな時刻を解決できるようにする

あいまいな時刻は複数の世界協定時刻 (UTC) にマップされる時刻です。 あいまいな時刻は、あるタイム ゾーンの夏時間から標準時間に移行する際など、時計の時刻を前に戻すときに発生します。 あいまいな時刻を処理する場合は、次のいずれかの操作を行います。

- あいまいな時刻が、ユーザーによって入力されたデータ項目である場合は、あいまいさの解決をユーザーに任せることができます。

- 時刻が UTC にどのようにマップされるかを想定します。 たとえば、あいまいな時刻は常にタイム ゾーンの標準時刻で表されると想定できます。

このトピックでは、ユーザーがあいまいな時刻を解決できるようにする方法について説明します。

### <a name="to-let-a-user-resolve-an-ambiguous-time"></a>ユーザーにあいまいな時刻を解決させるには

1. ユーザーによって入力された日付と時刻を取得します。

2. メソッドを呼び出して <xref:System.TimeZoneInfo.IsAmbiguousTime%2A> 、時刻があいまいであるかどうかを確認します。

3. 時刻があいまいな場合は、メソッドを呼び出して <xref:System.TimeZoneInfo.GetAmbiguousTimeOffsets%2A> オブジェクトの配列を取得し <xref:System.TimeSpan> ます。 配列の各要素には、あいまいな時刻をマップできる UTC オフセットが含まれています。

4. ユーザーに目的のオフセットを選択させます。

5. ローカル時刻からユーザーによって選択されたオフセットを減算して、UTC の日時を取得します。

6. `static`( `Shared` Visual Basic .net で) メソッドを呼び出して、 <xref:System.DateTime.SpecifyKind%2A> UTC の日付と時刻の値の <xref:System.DateTime.Kind%2A> プロパティをに設定し <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> ます。

## <a name="example"></a>例

次の例では、ユーザーに日付と時刻を入力するように求め、それがあいまいである場合は、ユーザーにあいまいな時刻をマップする UTC 時刻を選択させています。

[!code-csharp[System.TimeZone2.Concepts#11](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.Concepts/CS/TimeZone2Concepts.cs#11)]
[!code-vb[System.TimeZone2.Concepts#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.Concepts/VB/TimeZone2Concepts.vb#11)]

この例のコードの中核となるのは、オブジェクトの配列を使用して、 <xref:System.TimeSpan> UTC からのあいまいな時刻のオフセットを示すことです。 ただし、これらのオフセットは、ユーザーにとって意味がない可能性があります。 オフセットの意味を明確にするには、コードで、オフセットがローカル タイム ゾーンの標準時刻を表すか、または夏時間を表すかに注意します。 このコードでは、オフセットをプロパティの値と比較することによって、標準の時間と夏時間を判断し <xref:System.TimeZoneInfo.BaseUtcOffset%2A> ます。 このプロパティは、UTC とタイム ゾーンの標準時間の差を示します。

この例では、ローカルタイムゾーンへのすべての参照は、プロパティを使用して行われ <xref:System.TimeZoneInfo.Local%2A?displayProperty=nameWithType> ます。ローカルタイムゾーンは、オブジェクト変数に割り当てられることはありません。 メソッドを呼び出すと、 <xref:System.TimeZoneInfo.ClearCachedData%2A?displayProperty=nameWithType> ローカルタイムゾーンが割り当てられているオブジェクトが無効になるため、この方法をお勧めします。

## <a name="compiling-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- <xref:System> `using` ステートメント (C# コードでは必須) を使用して名前空間をインポートする。

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [方法: あいまいな時刻を解決する](resolve-ambiguous-times.md)
