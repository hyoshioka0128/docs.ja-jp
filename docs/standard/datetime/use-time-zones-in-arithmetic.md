---
title: '方法: 日付と時刻の演算でタイム ゾーンを使用する'
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- time zones [.NET Framework], arithmetic operations
- arithmetic operations [.NET Framework], dates and times
- dates [.NET Framework], adding and subtracting
ms.assetid: 83dd898d-1338-415d-8cd6-445377ab7871
ms.openlocfilehash: af19145f7caa9dbe8630ae7593734769e98720d0
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84280921"
---
# <a name="how-to-use-time-zones-in-date-and-time-arithmetic"></a>方法: 日付と時刻の演算でタイム ゾーンを使用する

通常、またはの値を使用して日付と時刻の演算を実行する場合、 <xref:System.DateTime> <xref:System.DateTimeOffset> 結果にはタイムゾーン調整規則は反映されません。 これは、日付と時刻の値のタイムゾーンが明確に識別できる場合 (たとえば、 <xref:System.DateTime.Kind%2A> プロパティがに設定されている場合) にも当てはまり <xref:System.DateTimeKind.Local> ます。 このトピックでは、特定のタイムゾーンに属する日付と時刻の値に対して算術演算を実行する方法について説明します。 算術演算の結果には、タイム ゾーンの調整規則が反映されます。

### <a name="to-apply-adjustment-rules-to-date-and-time-arithmetic"></a>日付と時刻の演算に調整規則を適用するには

1. なんらかの方法を実装して、日付と時刻の値と、その値が属するタイム ゾーンを密接に結び付けます。 たとえば、日付と時刻の値とそのタイム ゾーンの両方を含む構造体を宣言します。 次の例では、この方法を使用して、値とそのタイムゾーンをリンクして <xref:System.DateTime> います。

   [!code-csharp[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#6)]
   [!code-vb[System.DateTimeOffset.Conceptual#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#6)]

2. メソッドまたはメソッドのいずれかを呼び出して、時刻を世界協定時刻 (UTC) に変換し <xref:System.TimeZoneInfo.ConvertTimeToUtc%2A> <xref:System.TimeZoneInfo.ConvertTime%2A> ます。

3. UTC 時刻で算術演算を実行します。

4. メソッドを呼び出して、時刻を UTC から元の時刻に関連付けられているタイムゾーンに変換し <xref:System.TimeZoneInfo.ConvertTime%28System.DateTime%2CSystem.TimeZoneInfo%29?displayProperty=nameWithType> ます。

## <a name="example"></a>例

次の例では、中部標準時の 2008 年 3 月 9 日午前 1 時 30 分に、2 時間 30 分を 加えます。 夏時間へのタイム ゾーンの切り替えは、30 分後の 2008 年 3 月 9 日午前 2 時に 発生します。 この例は前に示した 4 つの手順に従うため、結果は正しい時刻である 2008 年 3 月 9 日午前 5 時に 発生します。

[!code-csharp[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual8.cs#8)]
[!code-vb[System.DateTimeOffset.Conceptual#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual8.vb#8)]

<xref:System.DateTime>との <xref:System.DateTimeOffset> 値の両方が、所属するタイムゾーンとの関連付けが解除されます。 タイム ゾーンの調整規則が自動的に適用されるような方法で日付と時刻の演算を実行するには、日付と時刻の値の属するタイム ゾーンがすぐに識別できる状態でなければなりません。 つまり、日時と関連付けられているタイム ゾーンを密に結合する必要があります。 これは、次のようないくつかの方法で行うことができます。

- アプリケーションで使用されるすべての時刻が、特定のタイム ゾーンに属するものと仮定します。 この方法は、適切な場合もありますが、柔軟性が限られ、移植性が制限される可能性もあります。

- 日時と関連付けられているタイム ゾーンを型のフィールドとして組み込むことで、両者を密に結合する型を定義します。 コード例ではこの方法を使用して、日時とタイム ゾーンを 2 つのメンバー フィールドに格納する構造体を定義しています。

この例では、値に対して算術演算を実行し、 <xref:System.DateTime> タイムゾーン調整規則が結果に適用されるようにする方法を示します。 ただし、 <xref:System.DateTimeOffset> 値は簡単に使用できます。 次の例は、元の例のコードを値の代わりに使用するように調整する方法を示してい <xref:System.DateTimeOffset> <xref:System.DateTime> ます。

[!code-csharp[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/cs/Conceptual6.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual/vb/Conceptual6.vb#7)]

この加算を最初に UTC に変換せずに値に対して実行すると、結果には <xref:System.DateTimeOffset> 正しいポイントが反映されますが、その時間の指定したタイムゾーンのオフセットは反映されません。

## <a name="compiling-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- <xref:System> `using` ステートメント (C# コードでは必須) を使用して名前空間をインポートする。

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
- [日付と時刻を使用した算術演算の実行](performing-arithmetic-operations.md)
