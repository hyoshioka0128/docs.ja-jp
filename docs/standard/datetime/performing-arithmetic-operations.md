---
title: 日付と時刻を使用した算術演算の実行
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- times [.NET Framework], arithmetic operations
- dates [.NET Framework], arithmetic operations
- time zones [.NET Framework], arithmetic operations
- arithmetic operations [.NET Framework], dates and times
- dates [.NET Framework], comparing
- DateTime structure, arithmetic operations
- DateTimeOffset structure, arithmetic operations
ms.assetid: 87c7ddf2-f15e-48af-8602-b3642237e6d0
ms.openlocfilehash: c212397f99bd09195f298d7d704c879705b14f02
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281545"
---
# <a name="performing-arithmetic-operations-with-dates-and-times"></a>日付と時刻を使用した算術演算の実行

との構造体はどちらも、 <xref:System.DateTime> <xref:System.DateTimeOffset> 値に対して算術演算を実行するメンバーを提供しますが、算術演算の結果は大きく異なります。 このトピックでは、これらの相違点を確認し、日付と時刻のデータのタイムゾーン認識の程度に関連付けて、日付と時刻のデータを使用して完全なタイムゾーン対応操作を実行する方法について説明します。

## <a name="comparisons-and-arithmetic-operations-with-datetime-values"></a>DateTime 値を使用した比較と算術演算

<xref:System.DateTime.Kind%2A?displayProperty=nameWithType>プロパティを使用する <xref:System.DateTimeKind> と、日付と時刻に値を割り当てて、現地時刻、世界協定時刻 (UTC)、または指定されていないタイムゾーンの時刻を表すかどうかを示すことができます。 ただし、この限られたタイムゾーン情報は、値に対して日付と時刻の演算を比較または実行するときには無視され <xref:System.DateTimeKind> ます。 次の例では、現在の現地時刻と現在の UTC 時刻を比較することで、この問題を示しています。

[!code-csharp[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual2.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual2.vb#2)]

メソッドは、 <xref:System.DateTime.CompareTo%28System.DateTime%29> 現地時刻が utc 時刻よりも前 (またはそれ未満) であることを報告します。減算演算は、utc と米国太平洋標準時ゾーンのシステムの現地時刻との差が7時間であることを示します。 ただし、これらの2つの値は、1つの時点の異なる表現を提供するため、この場合は、時間間隔が UTC からのローカルタイムゾーンのオフセットに完全に含まれていることがわかります。

一般に、プロパティは、 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 比較および算術メソッドによって返される結果には影響しません <xref:System.DateTime.Kind> (2 つの同じ時点の比較が示すため)。ただし、これらの結果の解釈に影響する可能性があります。 次に例を示します。

- プロパティが両方とも等しい2つの日付と時刻の値に対して実行される算術演算の結果は、 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> <xref:System.DateTimeKind> 2 つの値の間の実際の時間間隔を反映します。 同様に、そのような 2 つの日付と時刻の値を比較した結果には、2 つの時間の関係が正確に反映されます。

- 2つの日付と時刻の値が異なるプロパティ値を持つ2つの日付と時刻の値に対して実行される算術演算または比較演算の結果は、 <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> <xref:System.DateTimeKind> <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> 2 つの値の間のクロック時間の差を反映しています。

- ローカルの日付と時刻の値に対する算術演算または比較操作では、特定の値があいまいであるかや、無効であるかどうかは考慮されず、ローカル タイム ゾーンでの夏時間の開始や終了による調整規則の影響についても考慮されません。

- UTC と現地時刻の差を比較または計算する操作の結果には、UTC を基準としたローカル タイム ゾーンのオフセットに等しい時間差が含まれます。

- タイム ゾーンが指定されていない時刻と UTC または現地時刻との差を比較または計算する操作では、単純な時刻差が反映されます。 タイム ゾーンの違いは考慮されず、結果にはタイム ゾーン調整規則の適用が反映されません。

- タイム ゾーンが指定されていない 2 つの時刻の差を比較または計算する操作の結果には、2 つの異なるタイム ゾーンの時刻の差を反映した未知の時間差が含まれる場合があります。

タイムゾーンの違いが日付と時刻の計算に影響しないシナリオは多数あります (これらのいくつかについては、「 [DateTime、DateTimeOffset、TimeSpan、TimeZoneInfo の選択](choosing-between-datetime.md)」を参照してください)。または、日付と時刻のデータのコンテキストによって比較や算術演算の意味が定義されている場合もあります。

## <a name="comparisons-and-arithmetic-operations-with-datetimeoffset-values"></a>DateTimeOffset 値を使用した比較と算術演算

値には、 <xref:System.DateTimeOffset> 日付と時刻だけでなく、UTC を基準とする日付と時刻を明確に定義するオフセットも含まれます。 これにより、値の場合とは異なる方法で等しいかどうかを定義でき <xref:System.DateTimeOffset> ます。 一方、 <xref:System.DateTime> 値は同じ日付と時刻の値を持つ場合は等しいのに対し、両方とも <xref:System.DateTimeOffset> 同じ時点を参照している場合、値は等しいと見なされます。 これにより、 <xref:System.DateTimeOffset> 比較で使用する場合の解釈や、2つの日付と時刻の間隔を決定するほとんどの算術演算において、値の精度が向上し、解釈が不要になります。 次の例は、 <xref:System.DateTimeOffset> ローカル値と UTC 値を比較した前の例と同等のもので <xref:System.DateTimeOffset> あり、動作の違いを示しています。

[!code-csharp[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual3.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual3.vb#3)]

この例では、 <xref:System.DateTimeOffset.CompareTo%2A> メソッドは現在の現地時刻と現在の UTC 時刻が等しいことを示し、値の減算 <xref:System.DateTimeOffset.CompareTo(System.DateTimeOffset)> は2つの時刻の差がであることを示してい <xref:System.TimeSpan.Zero?displayProperty=nameWithType> ます。

日付と時刻の演算で値を使用する場合の上限は、 <xref:System.DateTimeOffset> 値がタイムゾーンに対応しているにもかかわらず、タイムゾーンを <xref:System.DateTimeOffset> 完全に認識していないことです。 <xref:System.DateTimeOffset>値のオフセットには、変数に最初に値が割り当てられたときの UTC からのタイムゾーンのオフセットが反映 <xref:System.DateTimeOffset> されますが、それ以降はタイムゾーンとの関連付けが解除されます。 特定可能な時刻との直接の関連付けは失われるため、日付と時刻の間隔に対して加算や減算を行っても、タイム ゾーンの調整規則は考慮されません。

例として、米国中部標準時ゾーンの夏時間への移行は午前2:00 に行われます。 発生します。 つまり、中部標準時の 2008 年 3 月 9 日の午前 1 時 30 分に 2 時間 30 分の間隔を加算すると、日付と時刻は 2008 年 3 月 9 日の 発生します。 しかし、次の例に示すように、加算の結果は 2008 年 3 月 9 日の 発生します。 この操作の結果は正しい時点を表していることに注意してください。ただし、目的のタイムゾーンの時刻ではありません (つまり、予想されるタイムゾーンオフセットがありません)。

[!code-csharp[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual4.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual4.vb#4)]

## <a name="arithmetic-operations-with-times-in-time-zones"></a>タイムゾーンの時刻を使用した算術演算

クラスには <xref:System.TimeZoneInfo> 、あるタイムゾーンから別のタイムゾーンに時刻を変換するときに調整を自動的に適用する多くの変換メソッドが含まれています。 次に例を示します。

- <xref:System.TimeZoneInfo.ConvertTime%2A>メソッドと <xref:System.TimeZoneInfo.ConvertTimeBySystemTimeZoneId%2A> メソッド。2つのタイムゾーン間で時刻を変換します。

- <xref:System.TimeZoneInfo.ConvertTimeFromUtc%2A>メソッドと <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> メソッド。特定のタイムゾーンの時刻を utc に変換するか、utc を特定のタイムゾーンの時刻に変換します。

詳細については、「[タイムゾーン間での時刻の変換](converting-between-time-zones.md)」を参照してください。

<xref:System.TimeZoneInfo>クラスには、日付と時刻の演算を実行するときに調整規則を自動的に適用するメソッドは用意されていません。 ただし、あるタイム ゾーンの時刻を UTC に変換してから算術演算を実行し、その後 UTC から元のタイム ゾーンの時刻に再変換することで、調整規則を適用したときと同じ結果を得ることができます。 詳細については、「[方法: 日付と時刻の演算でタイムゾーンを使用する](use-time-zones-in-arithmetic.md)」を参照してください。

たとえば、次のコードは、2008 年 3 月 9 日の午前 2 時に 2 時間 30 分を加算する 発生します。 ただし、中部標準時を UTC に変換した後に日付と時刻の算術演算を実行し、その結果を UTC から中部標準時に変換するため、得られた時刻は中部標準時タイム ゾーンの夏時間への移行を反映しています。

[!code-csharp[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual5.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual5.vb#5)]

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [方法: 日付と時刻の演算でタイム ゾーンを使用する](use-time-zones-in-arithmetic.md)
