---
title: DateTimeOffset オブジェクトのインスタンス化
description: .NET で DateTimeOffset オブジェクトをインスタンス化 (インスタンスを作成) する方法について説明します。 日付 & 時刻リテラル、コンストラクター、暗黙の型変換、& について説明します。
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- instantiating time zone objects
- time zone objects [.NET Framework], instantiation
- DateTimeOffset structure, converting to DateTime
- DateTimeOffset structure, instantiating
ms.assetid: 9648375f-d368-4373-a976-3332ece00c0a
ms.openlocfilehash: c2b71a2a98353a4ec9ed249acf18939dd4740e99
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768899"
---
# <a name="instantiating-a-datetimeoffset-object"></a>DateTimeOffset オブジェクトのインスタンス化

<xref:System.DateTimeOffset>構造体には、新しい値を作成するためのさまざまな方法が用意されて <xref:System.DateTimeOffset> います。 これらの多くは、新しい値をインスタンス化するために使用できるメソッドに直接対応し <xref:System.DateTime> ています。拡張機能を使用すると、世界協定時刻 (UTC) からの日付と時刻の値のオフセットを指定できます。 特に、 <xref:System.DateTimeOffset> 次の方法で値をインスタンス化できます。

- 日付と時刻のリテラルを使用する。

- コンストラクターを呼び出し <xref:System.DateTimeOffset> ます。

- 値を値に暗黙的に変換する <xref:System.DateTimeOffset> 。

- 日付と時刻の文字列形式を解析する。

このトピックでは、新しい値をインスタンス化するこれらのメソッドを示す、より詳細なコード例を示し <xref:System.DateTimeOffset> ます。

## <a name="date-and-time-literals"></a>日付および時刻のリテラル

これをサポートする言語では、値をインスタンス化する最も一般的な方法の1つ <xref:System.DateTime> は、ハードコーディングされたリテラル値として日付と時刻を指定することです。 たとえば、次の Visual Basic コードでは、 <xref:System.DateTime> 10:00 AM で2008年1月1日の値を持つオブジェクトを作成します。

[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#1)]

<xref:System.DateTimeOffset>リテラルをサポートする言語を使用する場合は、日付と時刻のリテラルを使用して値を初期化することもでき <xref:System.DateTime> ます。 たとえば、次の Visual Basic コードはオブジェクトを作成し <xref:System.DateTimeOffset> ます。

[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#2)]

コンソール出力に示されているよう <xref:System.DateTimeOffset> に、この方法で作成された値には、ローカルタイムゾーンのオフセットが割り当てられます。 つまり、 <xref:System.DateTimeOffset> コードが別のコンピューターで実行されている場合、文字リテラルを使用して割り当てられた値は、単一の時点を識別しません。

## <a name="datetimeoffset-constructors"></a>DateTimeOffset コンストラクター

この <xref:System.DateTimeOffset> 型は6つのコンストラクターを定義します。 これらの4つはコンストラクターに直接対応し <xref:System.DateTime> て <xref:System.TimeSpan> おり、UTC からの日付と時刻のオフセットを定義する型の追加パラメーターがあります。 これにより、 <xref:System.DateTimeOffset> 個々の日付と時刻のコンポーネントの値に基づいて値を定義できます。 たとえば、次のコードでは、これらの4つのコンストラクターを使用し <xref:System.DateTimeOffset> て、7/1/2008 12:05 AM + 01:00 と同じ値を持つオブジェクトをインスタンス化しています。

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#3)]

オブジェクトを <xref:System.DateTimeOffset> コンストラクターに渡す引数の1つとして使用してインスタンス化されたオブジェクトの値がコンソールに表示される場合は、 <xref:System.Globalization.PersianCalendar> ペルシャ暦ではなく、グレゴリオ暦の日付として表現されます。 ペルシャ暦を使用して日付を出力するには、「」の例を参照してください <xref:System.Globalization.PersianCalendar> 。

他の2つのコンストラクターは、 <xref:System.DateTimeOffset> 値からオブジェクトを作成し <xref:System.DateTime> ます。 最初のパラメーターには1つのパラメーターがあり、値は <xref:System.DateTime> 値に変換され <xref:System.DateTimeOffset> ます。 結果の値のオフセットは、 <xref:System.DateTimeOffset> <xref:System.DateTime.Kind%2A> コンストラクターの単一のパラメーターのプロパティによって異なります。 値がの場合 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> 、オフセットはに等しい値に設定され <xref:System.TimeSpan.Zero?displayProperty=nameWithType> ます。 それ以外の場合、オフセットはローカル タイム ゾーンのオフセットと等しい値に設定されます。 次の例は、このコンストラクターを使用して、 <xref:System.DateTimeOffset> UTC とローカルタイムゾーンを表すオブジェクトをインスタンス化する方法を示しています。

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#4)]

> [!NOTE]
> <xref:System.DateTimeOffset>1 つのパラメーターを持つコンストラクターのオーバーロードを呼び出すことは、値 <xref:System.DateTime> <xref:System.DateTime> から値への暗黙的な変換を実行することと同じです <xref:System.DateTimeOffset> 。

値からオブジェクトを作成する2つ目のコンストラクター <xref:System.DateTimeOffset> <xref:System.DateTime> には、 <xref:System.DateTime> 変換する値と <xref:System.TimeSpan> UTC からの日付と時刻のオフセットを表す値の2つのパラメーターがあります。 このオフセット値は、 <xref:System.DateTime.Kind%2A> コンストラクターの最初のパラメーターのプロパティに対応している必要があります。指定しないと、 <xref:System.ArgumentException> がスローされます。 <xref:System.DateTime.Kind%2A>最初のパラメーターのプロパティがの場合 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> 、2番目のパラメーターの値はである必要があり <xref:System.TimeSpan.Zero?displayProperty=nameWithType> ます。 <xref:System.DateTime.Kind%2A>最初のパラメーターのプロパティがの場合 <xref:System.DateTimeKind.Local?displayProperty=nameWithType> 、2番目のパラメーターの値は、ローカルシステムのタイムゾーンのオフセットである必要があります。 <xref:System.DateTime.Kind%2A>最初のパラメーターのプロパティがの場合 <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> 、オフセットには任意の有効な値を指定できます。 次のコードは、値に変換するこのコンストラクターの呼び出しを示してい <xref:System.DateTime> <xref:System.DateTimeOffset> ます。

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#5)]

## <a name="implicit-type-conversion"></a>暗黙の型変換

型は、 <xref:System.DateTimeOffset> <xref:System.DateTime> 値から値への暗黙的な型変換を1つサポートします。 <xref:System.DateTimeOffset> (暗黙的な型変換とは、明示的なキャスト (C# の場合) または変換 (Visual Basic の場合) を必要とせず、情報を失わない 1 つの型から別の型への変換です)。 これにより、次のようなコードが可能となります。

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#6)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#6)]

結果の値のオフセットは、 <xref:System.DateTimeOffset> プロパティ値によって異なり <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> ます。 値がの場合 <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> 、オフセットはに等しい値に設定され <xref:System.TimeSpan.Zero?displayProperty=nameWithType> ます。 値が <xref:System.DateTimeKind.Local?displayProperty=nameWithType> またはの場合 <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> 、オフセットはローカルタイムゾーンのオフセットと同じに設定されます。

## <a name="parsing-the-string-representation-of-a-date-and-time"></a>日付と時刻の文字列形式の解析

型では、 <xref:System.DateTimeOffset> 日付と時刻の文字列形式を値に変換できる4つのメソッドがサポートされてい <xref:System.DateTimeOffset> ます。

- <xref:System.DateTimeOffset.Parse%2A>。日付と時刻の文字列形式を値に変換しよう <xref:System.DateTimeOffset> とし、変換に失敗した場合は例外をスローします。

- <xref:System.DateTimeOffset.TryParse%2A>。日付と時刻の文字列形式を値に変換しよう <xref:System.DateTimeOffset> とし、変換に失敗した `false` 場合はを返します。

- <xref:System.DateTimeOffset.ParseExact%2A>。指定した形式の日付と時刻の文字列形式を値に変換しようとし <xref:System.DateTimeOffset> ます。 変換が失敗すると、メソッドは例外をスローします。

- <xref:System.DateTimeOffset.TryParseExact%2A>。指定した形式の日付と時刻の文字列形式を値に変換しようとし <xref:System.DateTimeOffset> ます。 変換が失敗すると、メソッドは `false` を返します。

次の例では、これらの4つの文字列変換メソッドを呼び出して値をインスタンス化してい <xref:System.DateTimeOffset> ます。

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#7)]

## <a name="see-also"></a>関連項目

- [日付、時刻、およびタイム ゾーン](index.md)
