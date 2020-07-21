---
title: DateTime、DateTimeOffset、TimeSpan、および TimeZoneInfo を比較する
description: .NET での日付と時刻の情報を表すために、DateTime、DateTimeOffset、TimeSpan、および TimeZoneInfo 型の違いについて説明します。
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DateTimeOffset structure
- TimeZoneInfo class
- time zones [.NET Framework], common uses
- date and time classes [.NET Framework]
- time zones [.NET Framework], type options
- DateTime structure
ms.assetid: 07f17aad-3571-4014-9ef3-b695a86f3800
ms.openlocfilehash: 03d00fb802032b981a5ebe80f7166eba0fb54a60
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85326048"
---
# <a name="choose-between-datetime-datetimeoffset-timespan-and-timezoneinfo"></a>DateTime、DateTimeOffset、TimeSpan、TimeZoneInfo のいずれかを選択してください

.NET アプリケーションでは、さまざまな方法で日付と時刻の情報を使用できます。 日付と時刻の情報の一般的な使用方法は次のとおりです。

- 日付のみを反映する (時刻情報は重要ではない)。

- 時刻のみを反映する (日付情報は重要ではない)。

- 特定の時刻と場所に関連付けられていない抽象日時を反映する (たとえば、国際的チェーンのほとんどのストアは週中の午前 9:00 にオープンする)。

- .NET 以外のソースから日付と時刻の情報を取得する場合は。通常、日付と時刻の情報は単純なデータ型に格納されます。

- 単一の時点を一意かつ明確に識別する。 アプリケーションによっては、ホストシステムでのみ日付と時刻を明確にする必要がある場合があります。 他のアプリでは、システム間で明確にする必要があります (つまり、あるシステムでシリアル化された日付は、世界中のどこでも別のシステムで明確に逆シリアル化して使用できます)。

- 関連する複数の時刻を保持する (要求元の現地時刻やサーバーの Web 要求受信時刻など)。

- 日付と時刻の演算を実行する (これにより、おそらく単一時点が一意かつ明確に識別される)。

.Net には、、、、およびの各型が含まれており、これらすべてを使用して <xref:System.DateTime> 、 <xref:System.DateTimeOffset> <xref:System.TimeSpan> <xref:System.TimeZoneInfo> 日付と時刻を操作するアプリケーションを構築できます。

> [!NOTE]
> このトピック <xref:System.TimeZone> では、その機能がほぼ完全にクラスに組み込まれているため、説明しません <xref:System.TimeZoneInfo> 。 可能な限り、クラス <xref:System.TimeZoneInfo> の代わりにクラスを使用し <xref:System.TimeZone> ます。

## <a name="the-datetime-structure"></a>DateTime 構造体

<xref:System.DateTime> 値は、特定の日付と時刻を定義します。 これには、 <xref:System.DateTime.Kind%2A> その日付と時刻が属するタイムゾーンに関する限られた情報を提供するプロパティが含まれます。 <xref:System.DateTimeKind> プロパティによって返される <xref:System.DateTime.Kind%2A> 値は、 <xref:System.DateTime> 値が現地時刻 (<xref:System.DateTimeKind.Local?displayProperty=nameWithType>)、世界協定時刻 (UTC) (<xref:System.DateTimeKind.Utc?displayProperty=nameWithType>)、指定されていない時刻 (<xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>) のうちのどれを表すかを示します。

この <xref:System.DateTime> 構造は、次の1つ以上の特性を持つアプリケーションに適しています。

- 日付のみを使用するアプリケーション。

- 時刻のみを使用するアプリケーション。

- 抽象日時を使用するアプリケーション。

- タイム ゾーン情報がない日時を使用するアプリケーション。

- UTC 日時のみを使用するアプリケーション。

- SQL データベースなど、.NET の外部のソースから日付と時刻の情報を取得します。 通常、これらのソースは、 <xref:System.DateTime> 構造体と互換性のある単純な形式で日時情報を格納します。

- 日付と時刻の演算を実行しますが、これは一般的な結果に関するものです。 たとえば、6 カ月を特定の日付と時刻に加算する加算演算では、多くの場合、結果を夏時間に合わせて調整するかどうかは重要ではありません。

特定の <xref:System.DateTime> 値が UTC を表さない場合、通常、その日付と時刻の値は、あいまいであるか、その移植性に限定されます。 たとえば、 <xref:System.DateTime> 値が現地時刻を表す場合、そのローカル タイム ゾーン内で移植することができます (つまり、同じタイム ゾーンにある別のシステムで値が逆シリアル化されると、その値は明確に単一時点を識別します)。 ローカル タイム ゾーン外では、その <xref:System.DateTime> 値は複数の意味を持つ場合があります。 値の <xref:System.DateTime.Kind%2A> プロパティが <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType>の場合、移植性は低くなります。同じタイム ゾーン内であいまいになり、最初にシリアル化したのと同じシステムにおいてさえもあいまいになる可能性があります。 <xref:System.DateTime> 値が UTC を表す場合のみ、値が使用されるシステムまたはタイム ゾーンに関係なく、その値は明確に単一時点を識別します。

> [!IMPORTANT]
> <xref:System.DateTime> データを保存または共有する際、UTC を使用する必要があり、 <xref:System.DateTime> 値の <xref:System.DateTime.Kind%2A> プロパティを <xref:System.DateTimeKind.Utc?displayProperty=nameWithType>に設定する必要があります。

## <a name="the-datetimeoffset-structure"></a>DateTimeOffset 構造体

<xref:System.DateTimeOffset> 構造体は、日付と時刻の値、およびその値と UTC との差異を示すオフセットを表します。 そのため、値は常に明確に単一時点を識別します。

<xref:System.DateTimeOffset> 型には、 <xref:System.DateTime> 型のすべての機能に加え、タイム ゾーンの処理機能が含まれます。 これにより、次のようなアプリケーションに適しています。

- 単一の時点を一意かつ明確に識別する。 <xref:System.DateTimeOffset> 型を使用して、「現在」の意味を明確に定義し、トランザクションの時刻を記録し、システム イベントまたはアプリケーション イベントの時刻を記録し、ファイル作成時刻とファイル変更時刻を記録することができます。

- 一般的な日付と時刻の演算を実行する。

- その時刻が 2 つの別々の値または構造体の 2 つのメンバーである場合、関連する複数の時刻を保持する。

> [!NOTE]
> <xref:System.DateTimeOffset> 値のこの用途は、 <xref:System.DateTime> 値の用途と比べてはるかに一般的です。 そのため、 <xref:System.DateTimeOffset> アプリケーション開発の既定の日付と時刻の型として考慮してください。

<xref:System.DateTimeOffset>値は特定のタイムゾーンに関連付けられていませんが、さまざまなタイムゾーンから発生することがあります。 次の例では、複数の <xref:System.DateTimeOffset> 値 (ローカルの太平洋標準時を含む) が属することができるタイムゾーンを一覧表示します。

[!code-csharp[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual1.cs#1)]
[!code-vb[System.DateTimeOffset.Conceptual#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual1.vb#1)]

この例の日付と時刻の値はそれぞれ少なくとも 3 つの異なるタイム ゾーンに属することができることを出力は示しています。 <xref:System.DateTimeOffset>6/10/2007 の値は、日付と時刻の値が夏時間を表す場合、utc からのオフセットは必ずしも元のタイムゾーンの基本 UTC オフセット、またはその表示名で見つかった utc からのオフセットに対応していないことを示しています。 単一の <xref:System.DateTimeOffset> 値はそのタイムゾーンと密接に結び付いていないため、夏時間との間のタイムゾーンの遷移を反映することはできません。 日付と時刻の演算を使用して値を操作すると、問題が発生する可能性があり <xref:System.DateTimeOffset> ます。 タイムゾーンの調整規則を考慮する方法で日付と時刻の演算を実行する方法については、「[日付と時刻を使用](performing-arithmetic-operations.md)した算術演算の実行」を参照してください。

## <a name="the-timespan-structure"></a>TimeSpan 構造体

<xref:System.TimeSpan> 構造体は、時間間隔を表します。 その 2 つの一般的な用途は、次のとおりです。

- 2 つの日付と時刻の値の間の時間を反映する。 たとえば、ある値から <xref:System.DateTime> 値を減算すると、 <xref:System.TimeSpan> 値が返されます。

- 経過時間を測定する。 たとえば、プロパティは、 <xref:System.Diagnostics.Stopwatch.Elapsed%2A?displayProperty=nameWithType> <xref:System.TimeSpan> <xref:System.Diagnostics.Stopwatch> 経過時間の計測を開始するメソッドの1つを呼び出した後に経過した時間間隔を反映する値を返します。

値が <xref:System.TimeSpan> <xref:System.DateTime> 特定の日を参照せずに時間を反映している場合は、値の置換として値を使用することもできます。 この使用方法は、プロパティとプロパティに似てい <xref:System.DateTime.TimeOfDay%2A?displayProperty=nameWithType> <xref:System.DateTimeOffset.TimeOfDay%2A?displayProperty=nameWithType> ます。このプロパティは、 <xref:System.TimeSpan> 日付への参照なしで時間を表す値を返します。 たとえば、 <xref:System.TimeSpan> 構造体を使用して、ストアの開店時刻または閉店時刻を反映したり、標準イベントが発生したときの時刻を表したりするために使用できます。

以下の例では、開店時刻と閉店時刻用の `StoreInfo` オブジェクト、およびストアのタイム ゾーンを表す <xref:System.TimeSpan> オブジェクトを含む <xref:System.TimeZoneInfo> 構造体を定義します。 構造体には、 `IsOpenNow` 、 `IsOpenAt`という 2 つのメソッドも含まれます。これは、ローカル タイム ゾーンにいると想定されるユーザーによって指定された時刻にストアがオープンするかどうかを示します。

[!code-csharp[Conceptual.ChoosingDates#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#1)]
[!code-vb[Conceptual.ChoosingDates#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#1)]

`StoreInfo` 構造体をクライアント コードで次のように使用できます。

[!code-csharp[Conceptual.ChoosingDates#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.choosingdates/cs/datetimereplacement1.cs#2)]
[!code-vb[Conceptual.ChoosingDates#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.choosingdates/vb/datetimereplacement1.vb#2)]

## <a name="the-timezoneinfo-class"></a>TimeZoneInfo クラス

<xref:System.TimeZoneInfo> class represents any of the Earth's time zones, and enables the conversion of any date and time in one time zone to its equivalent in another time zone. <xref:System.TimeZoneInfo> クラスにより、日付と時刻を使用して、どの日付と時刻の値も明確に単一時点を識別できるようにすることができます。 <xref:System.TimeZoneInfo> クラスを拡張することもできます。 Windows システムで提供され、レジストリで定義されているタイム ゾーン情報に依存していますが、カスタムのタイム ゾーンの作成もサポートされています。 また、タイム ゾーン情報のシリアル化と逆シリアル化もサポートされています。

場合によっては、 <xref:System.TimeZoneInfo> クラスをフル活用するために、開発作業をさらに実行する必要が生じることもあります。 日付と時刻の値が属するタイムゾーンと密接に結び付いていない場合は、さらに作業が必要になります。 アプリケーションで、日付と時刻を関連付けられたタイムゾーンとリンクするメカニズムが提供されていない限り、特定の日付と時刻の値がそのタイムゾーンとの関連付けを解除するのは簡単です。 この情報をリンクする 1 つの方法は、日付と時刻の値とその関連タイム ゾーン オブジェクトの両方を含むクラスまたは構造体を定義するという方法です。

.NET でタイムゾーンのサポートを利用するには、日付と時刻のオブジェクトがインスタンス化されるときに、日付と時刻の値が属するタイムゾーンを把握しておく必要があります。 タイムゾーンは、特に web アプリやネットワークアプリでは不明です。

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
