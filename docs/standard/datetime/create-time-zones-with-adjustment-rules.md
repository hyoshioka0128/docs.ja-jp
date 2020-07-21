---
title: '方法: 調整規則のあるタイム ゾーンを作成する'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], creating
- time zones [.NET Framework], and adjustment rules
- adjustment rule [.NET Framework]
ms.assetid: c52ef192-13a9-435f-8015-3b12eae8c47c
ms.openlocfilehash: b7e938581dfde3f1566aa2506302292686c2fc5c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84278169"
---
# <a name="how-to-create-time-zones-with-adjustment-rules"></a>方法: 調整規則のあるタイム ゾーンを作成する

アプリケーションで必要とされる正確なタイムゾーン情報は、次のような理由で特定のシステムに存在しない場合があります。

- タイムゾーンがローカルシステムのレジストリに定義されていません。

- タイムゾーンに関するデータは、レジストリから変更または削除されています。

- タイムゾーンには、特定の履歴期間のタイムゾーン調整に関する正確な情報がありません。

このような場合は、メソッドを呼び出し <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> て、アプリケーションで必要とされるタイムゾーンを定義できます。 このメソッドのオーバーロードを使用して、調整規則の有無に関係なくタイムゾーンを作成できます。 タイムゾーンで夏時間がサポートされている場合は、固定調整規則または浮動調整規則のいずれかを使用して調整を定義できます。 (これらの用語の定義については、「タイムゾーンの[概要](time-zone-overview.md)」の「タイムゾーンの用語」セクションを参照してください)。

> [!IMPORTANT]
> メソッドを呼び出すことによって作成されたカスタムタイムゾーン <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> は、レジストリには追加されません。 代わりに、メソッド呼び出しによって返されるオブジェクト参照を使用してのみアクセスでき <xref:System.TimeZoneInfo.CreateCustomTimeZone%2A> ます。

このトピックでは、調整規則を使用してタイムゾーンを作成する方法について説明します。 夏時間調整規則をサポートしていないタイムゾーンを作成するには、「[方法: 調整規則のないタイムゾーンを作成](create-time-zones-without-adjustment-rules.md)する」を参照してください。

### <a name="to-create-a-time-zone-with-floating-adjustment-rules"></a>浮動調整規則を使用してタイムゾーンを作成するには

1. それぞれの調整について (つまり、特定の期間にわたって標準時間外に移行するたびに)、次の手順を実行します。

    1. タイムゾーン調整の開始遷移時間を定義します。

       メソッドを呼び出して、遷移の時刻を定義する値、遷移の月を定義する <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=nameWithType> <xref:System.DateTime> 整数値、遷移が発生する曜日を定義する整数値、および遷移が発生する曜日を定義する値を渡す必要があります。この場合、メソッドを呼び出す必要があり <xref:System.DayOfWeek> ます。 このメソッド呼び出しは、オブジェクトをインスタンス化 <xref:System.TimeZoneInfo.TransitionTime> します。

    2. タイムゾーン調整の終了遷移時間を定義します。 これには、メソッドの別の呼び出しが必要です <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A?displayProperty=nameWithType> 。 このメソッド呼び出しは、2番目のオブジェクトをインスタンス化 <xref:System.TimeZoneInfo.TransitionTime> します。

    3. メソッドを呼び出し、 <xref:System.TimeZoneInfo.AdjustmentRule.CreateAdjustmentRule%2A> 調整の有効な開始日と終了日、 <xref:System.TimeSpan> 遷移の時間を定義するオブジェクト、および夏時間との <xref:System.TimeZoneInfo.TransitionTime> 間の切り替えが発生するタイミングを定義する2つのオブジェクトを渡します。 このメソッド呼び出しは、オブジェクトをインスタンス化 <xref:System.TimeZoneInfo.AdjustmentRule> します。

    4. オブジェクトを <xref:System.TimeZoneInfo.AdjustmentRule> オブジェクトの配列に割り当て <xref:System.TimeZoneInfo.AdjustmentRule> ます。

2. タイムゾーンの表示名を定義します。 表示名は、標準形式に準拠しています。この形式では、世界協定時刻 (UTC) からのタイムゾーンのオフセットがかっこで囲まれ、タイムゾーンの1つまたは複数の都市を識別する文字列、またはタイムゾーンの1つ以上の国または地域が続きます。

3. タイムゾーンの標準時刻の名前を定義します。 通常、この文字列はタイムゾーンの識別子としても使用されます。

4. タイムゾーンの夏時間の名前を定義します。

5. タイムゾーンの標準名とは異なる識別子を使用する場合は、タイムゾーン識別子を定義します。

6. <xref:System.TimeSpan>タイムゾーンの UTC からのオフセットを定義するオブジェクトをインスタンス化します。 時刻が UTC より遅いタイムゾーンには、正のオフセットがあります。 時刻が UTC より前のタイムゾーンでは、負のオフセットが使用されます。

7. メソッドを呼び出して <xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=nameWithType> 、新しいタイムゾーンをインスタンス化します。

## <a name="example"></a>例

次の例では、1918から現在のまでのさまざまな時間間隔の調整規則を含む米国の中部標準時のタイムゾーンを定義します。

[!code-csharp[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#5)]
[!code-vb[System.TimeZone2.CreateTimeZone#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#5)]

この例で作成したタイムゾーンには、複数の調整規則があります。 調整規則の有効な開始日と終了日が、別の調整規則の日付と重複しないように注意する必要があります。 重複がある場合は、 <xref:System.InvalidTimeZoneException> がスローされます。

浮動調整規則では、値5がメソッドのパラメーターに渡され、 `week` <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A> 特定の月の最後の週に移行が行われることを示します。

<xref:System.TimeZoneInfo.AdjustmentRule>メソッド呼び出しで使用するオブジェクトの配列を作成する <xref:System.TimeZoneInfo.CreateCustomTimeZone%28System.String%2CSystem.TimeSpan%2CSystem.String%2CSystem.String%2CSystem.String%2CSystem.TimeZoneInfo.AdjustmentRule%5B%5D%29?displayProperty=nameWithType> 場合、コードは、タイムゾーンに対して作成される調整の数に必要なサイズに配列を初期化できます。 代わりに、このコード例ではメソッドを呼び出して、 <xref:System.Collections.Generic.List%601.Add%2A> オブジェクトのジェネリックコレクションに各調整規則を追加し <xref:System.Collections.Generic.List%601> <xref:System.TimeZoneInfo.AdjustmentRule> ます。 次に、メソッドを呼び出して、 <xref:System.Collections.Generic.List%601.CopyTo%2A> このコレクションのメンバーを配列にコピーします。

また、この例では、メソッドを使用して、 <xref:System.TimeZoneInfo.TransitionTime.CreateFixedDateRule%2A> 固定日付の調整を定義しています。 これは、メソッドの呼び出しに似ていますが、 <xref:System.TimeZoneInfo.TransitionTime.CreateFloatingDateRule%2A> 移行パラメーターの時刻、月、および日のみが必要です。

この例は、次のようなコードを使用してテストできます。

[!code-csharp[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#7)]
[!code-vb[System.TimeZone2.CreateTimeZone#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#7)]

## <a name="compiling-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- 次の名前空間がインポートされます。

  [!code-csharp[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/cs/System.TimeZone2.CreateTimeZone.cs#6)]
  [!code-vb[System.TimeZone2.CreateTimeZone#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.TimeZone2.CreateTimeZone/vb/System.TimeZone2.CreateTimeZone.vb#6)]

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [タイム ゾーンの概要](time-zone-overview.md)
- [方法: 調整規則のないタイム ゾーンを作成する](create-time-zones-without-adjustment-rules.md)
