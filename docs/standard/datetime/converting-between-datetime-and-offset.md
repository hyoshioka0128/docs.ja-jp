---
title: DateTime と DateTimeOffset 間の変換
description: .NET の DateTimeOffset 値と DateTime 値の間で変換を行います。 DateTimeOffset 構造体は、DateTime 構造体よりも多くのタイムゾーン認識を提供します。
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTime structure, converting
- time zones [.NET Framework], conversions
- UTC times, converting
- DateTimeOffset structure, converting
- converting DateTimeOffset and DateTime values
- dates [.NET Framework], converting
- converting times
- Date data type, converting
- local time conversions
ms.assetid: b605ff97-0c45-4c24-833f-4c6a3e8be64c
ms.openlocfilehash: cf55db7c22ad2495bdbeb3202fcefb89bae42d69
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768678"
---
# <a name="converting-between-datetime-and-datetimeoffset"></a>DateTime と DateTimeOffset 間の変換

構造体は、 <xref:System.DateTimeOffset> 構造体よりも高い範囲のタイムゾーンを認識し <xref:System.DateTime> <xref:System.DateTime> ますが、メソッドの呼び出しでは、より一般的にパラメーターが使用されます。 このため、値を値に変換したり、その逆の変換を行ったりすること <xref:System.DateTimeOffset> <xref:System.DateTime> は、特に重要です。 このトピックでは、できるだけ多くのタイムゾーン情報を保持する方法でこれらの変換を実行する方法について説明します。

> [!NOTE]
> との両方の型には、 <xref:System.DateTime> <xref:System.DateTimeOffset> タイムゾーンの時刻を表すときにいくつかの制限があります。 プロパティを使用 <xref:System.DateTime.Kind%2A> すると、 <xref:System.DateTime> は世界協定時刻 (UTC) とシステムのローカルタイムゾーンのみを反映できます。 <xref:System.DateTimeOffset>UTC からの時刻のオフセットを反映しますが、そのオフセットが属する実際のタイムゾーンは反映されません。 時刻の値とタイムゾーンのサポートの詳細については、「 [DateTime、DateTimeOffset、TimeSpan、および TimeZoneInfo の使い分け](choosing-between-datetime.md)」を参照してください。

## <a name="conversions-from-datetime-to-datetimeoffset"></a>DateTime から DateTimeOffset への変換

この <xref:System.DateTimeOffset> 構造体は、 <xref:System.DateTime> <xref:System.DateTimeOffset> ほとんどの変換に適した変換に対して実行する2つの同等の方法を提供します。

- <xref:System.DateTimeOffset.%23ctor%2A>コンストラクター。 <xref:System.DateTimeOffset> 値に基づいて新しいオブジェクトを作成し <xref:System.DateTime> ます。

- 暗黙的な変換演算子。これにより、オブジェクトに値を割り当てることができ <xref:System.DateTime> <xref:System.DateTimeOffset> ます。

UTC 値とローカル <xref:System.DateTime> 値の場合、 <xref:System.DateTimeOffset.Offset%2A> 結果の値のプロパティに <xref:System.DateTimeOffset> utc またはローカルタイムゾーンオフセットが正確に反映されます。 たとえば、次のコードは、UTC 時刻をそれと等価な値に変換し <xref:System.DateTimeOffset> ます。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#1)]

この場合、`utcTime2` 変数のオフセットは 00:00 です。 同様に、次のコードは、現地時刻をそれと等価な値に変換し <xref:System.DateTimeOffset> ます。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#2)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#2)]

ただし、 <xref:System.DateTime> プロパティがである値の場合、 <xref:System.DateTime.Kind%2A> <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> これら2つの変換メソッドは、 <xref:System.DateTimeOffset> オフセットがローカルタイムゾーンの値である値を生成します。 これを次の例に示します。この例は、米国太平洋標準時ゾーンで実行されています。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#3)]

値に <xref:System.DateTime> ローカルタイムゾーンまたは UTC 以外の日付と時刻が反映されている場合は、オーバーロードされた <xref:System.DateTimeOffset> コンストラクターを呼び出すことによって、値を値に変換し、そのタイムゾーン情報を保持することができ <xref:System.DateTimeOffset.%23ctor%2A> ます。 たとえば、次の例では、 <xref:System.DateTimeOffset> 中部標準時を反映するオブジェクトをインスタンス化しています。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#4)]

このコンストラクターのオーバーロードに対する2番目のパラメーターは、時刻の <xref:System.TimeSpan> UTC からのオフセットを表すオブジェクトで、 <xref:System.TimeZoneInfo.GetUtcOffset%28System.DateTime%29?displayProperty=nameWithType> 時刻に対応するタイムゾーンのメソッドを呼び出すことによって取得する必要があります。 メソッドの1つのパラメーターは、 <xref:System.DateTime> 変換する日付と時刻を表す値です。 タイム ゾーンで夏時間がサポートされている場合、このパラメーターにより、このメソッドはその特定の日時に対して適切なオフセットを決定できます。

## <a name="conversions-from-datetimeoffset-to-datetime"></a>DateTimeOffset から DateTime への変換

<xref:System.DateTimeOffset.DateTime%2A>プロパティは、変換を実行するために最も一般的に使用され <xref:System.DateTimeOffset> <xref:System.DateTime> ます。 ただし、 <xref:System.DateTime> <xref:System.DateTime.Kind%2A> 次の例に示すように、このメソッドは、プロパティがである値を返し <xref:System.DateTimeKind.Unspecified> ます。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#5)]

これは、プロパティを使用するときに、値と UTC の関係に関する情報 <xref:System.DateTimeOffset> が変換によって失われることを意味し <xref:System.DateTimeOffset.DateTime%2A> ます。 これ <xref:System.DateTimeOffset> は、UTC 時刻またはシステムの現地時刻に対応する値に影響します。これは、 <xref:System.DateTimeOffset.DateTime%2A> 構造体がそのプロパティ内の2つのタイムゾーンのみを反映しているため <xref:System.DateTime.Kind%2A> です。

を値に変換するときに、できるだけ多くのタイムゾーン情報を保持するには、 <xref:System.DateTimeOffset> <xref:System.DateTime> <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=nameWithType> プロパティとプロパティを使用し <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> ます。

### <a name="converting-a-utc-time"></a>UTC 時刻の変換

変換された値が UTC 時刻であることを示すには、 <xref:System.DateTimeOffset.DateTime%2A> プロパティの値を取得し <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=nameWithType> ます。 これは、 <xref:System.DateTimeOffset.DateTime%2A> 次の2つの方法でプロパティとは異なります。

- このメソッド <xref:System.DateTime> は、プロパティがである値を返し <xref:System.DateTime.Kind%2A> <xref:System.DateTimeKind.Utc> ます。

- <xref:System.DateTimeOffset.Offset%2A>プロパティ値がと等しくない場合は、 <xref:System.TimeSpan.Zero?displayProperty=nameWithType> 時刻を UTC に変換します。

> [!NOTE]
> 変換された値が明確に単一の時点を識別するようにアプリケーションで要求される場合は、 <xref:System.DateTime> プロパティを使用して <xref:System.DateTimeOffset.UtcDateTime%2A?displayProperty=nameWithType> すべての変換を処理することを検討してください <xref:System.DateTimeOffset> <xref:System.DateTime> 。

次のコードでは、プロパティを使用して、 <xref:System.DateTimeOffset.UtcDateTime%2A> <xref:System.DateTimeOffset> オフセットがに等しい値を <xref:System.TimeSpan.Zero?displayProperty=nameWithType> 値に変換し <xref:System.DateTime> ます。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#6)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#6)]

次のコードでは、プロパティを使用して、 <xref:System.DateTimeOffset.UtcDateTime%2A> 値に対してタイムゾーン変換と型変換の両方を実行し <xref:System.DateTimeOffset> ます。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#12)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#12)]

### <a name="converting-a-local-time"></a>現地時刻の変換

値が現地時刻を表すことを示すには、 <xref:System.DateTimeOffset> <xref:System.DateTime> プロパティによって返された値 <xref:System.DateTimeOffset.DateTime%2A?displayProperty=nameWithType> を `static` ( `Shared` Visual Basic) メソッドに渡すことができ <xref:System.DateTime.SpecifyKind%2A> ます。 メソッドは、最初のパラメーターとして渡された日付と時刻を返しますが、プロパティは、 <xref:System.DateTime.Kind%2A> 2 番目のパラメーターで指定した値に設定されます。 次のコードでは、 <xref:System.DateTime.SpecifyKind%2A> <xref:System.DateTimeOffset> オフセットがローカルタイムゾーンのオフセットに対応する値を変換するときに、メソッドを使用しています。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#7)]

また、プロパティを使用して、 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> 値をローカル値に変換することもでき <xref:System.DateTimeOffset> <xref:System.DateTime> ます。 <xref:System.DateTime.Kind%2A>戻り値のプロパティ <xref:System.DateTime> が <xref:System.DateTimeKind.Local> です。 次のコードでは、 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> <xref:System.DateTimeOffset> オフセットがローカルタイムゾーンのオフセットに対応する値を変換するときに、プロパティを使用しています。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#10)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#10)]

<xref:System.DateTime>プロパティを使用して値を取得すると <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> 、プロパティのアクセサーは、 `get` 最初に値を <xref:System.DateTimeOffset> UTC に変換してから、メソッドを呼び出して現地時刻に変換し <xref:System.DateTimeOffset.ToLocalTime%2A> ます。 これは、プロパティから値を取得して、型変換を実行するときと同時にタイムゾーン変換を実行できることを意味し <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> ます。 また、変換の実行にローカル タイム ゾーンの調整規則が適用されることも意味します。 次のコードは、プロパティを使用して、 <xref:System.DateTimeOffset.LocalDateTime%2A?displayProperty=nameWithType> 型とタイムゾーン変換の両方を実行する方法を示しています。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#11)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#11)]

### <a name="a-general-purpose-conversion-method"></a>汎用変換メソッド

次の例では、 `ConvertFromDateTimeOffset` 値を値に変換するという名前のメソッドを定義して <xref:System.DateTimeOffset> <xref:System.DateTime> います。 オフセットに基づいて、 <xref:System.DateTimeOffset> 値が UTC 時刻、現地時刻、またはその他の時刻であるかどうかを判断し、返された日付と時刻の値のプロパティをそれに応じて定義し <xref:System.DateTime.Kind%2A> ます。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#8)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#8)]

次の例では、メソッドを呼び出して、 `ConvertFromDateTimeOffset` <xref:System.DateTimeOffset> UTC 時刻、現地時刻、および米国中部標準時ゾーンの時刻を表す値を変換します。

[!code-csharp[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/cs/Conversions.cs#9)]
[!code-vb[System.DateTimeOffset.Conceptual.Conversions#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Conversions/vb/Conversions.vb#9)]

このコードは次の 2 つのことを前提としますが、アプリケーションおよびその日時値のソースによっては常に有効とは限らないことに注意してください。

- オフセットが UTC を表す日付と時刻の値であることを前提としてい <xref:System.TimeSpan.Zero?displayProperty=nameWithType> ます。 実際には、UTC は特定のタイム ゾーンの時刻ではなく、世界のタイム ゾーンの時刻を標準化する際に基準となる時刻です。 タイムゾーンには、のオフセットを設定することもでき <xref:System.TimeSpan.Zero> ます。

- オフセットがローカル タイム ゾーンのオフセットと等しい日時が、ローカル タイム ゾーンを表すことを前提とします。 日時値は元のタイム ゾーンとの関連付けが解除されているので、これは該当しない場合があります。日時は、同じオフセットを持つ別のタイム ゾーンに由来する可能性があります。

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
