---
title: Protobuf スカラーデータ型-gRPC (WCF 開発者向け)
description: .NET Core の Protobuf と gRPC でサポートされている基本的なデータ型と既知のデータ型について説明します。
ms.date: 09/09/2019
ms.openlocfilehash: ae7f5f48099000dff0eefb36e23cb9b9f2ac517c
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73971545"
---
# <a name="protobuf-scalar-data-types"></a>Protobuf スカラー データ型

Protobuf は、ネイティブスカラー値型の範囲をサポートしています。 次の表に、それらのすべてのC#型に対応する型を示します。

| Protobuf 型 | C# 型      | 説明 |
| ------------- | ------------ | ----- |
| `double`      | `double`     |       |
| `float`       | `float`      |       |
| `int32`       | `int`        | 1     |
| `int64`       | `long`       | 1     |
| `uint32`      | `uint`       |       |
| `uint64`      | `ulong`      |       |
| `sint32`      | `int`        | 1     |
| `sint64`      | `long`       | 1     |
| `fixed32`     | `uint`       | 2     |
| `fixed64`     | `ulong`      | 2     |
| `sfixed32`    | `int`        | 2     |
| `sfixed64`    | `long`       | 2     |
| `bool`        | `bool`       |       |
| `string`      | `string`     | 3     |
| `bytes`       | `ByteString` | 4     |

## <a name="notes"></a>説明

1. `int32` および `int64` の標準エンコードは、署名された値を使用する場合には非効率的です。 フィールドに負の数値が含まれている可能性がある場合は、代わりに `sint32` または `sint64` を使用します。 両方の型はC# 、それぞれ `int` と `long` 型にマップされます。
2. `fixed` のフィールドでは、値が何であるかにかかわらず、常に同じバイト数を使用します。 この動作により、シリアル化と逆シリアル化がより大きな値に対して高速化されます。
3. Protobuf 文字列は UTF-8 (または7ビット ASCII) でエンコードされ、エンコードされた長さは 2<sup>32</sup>を超えることはできません。
4. Protobuf ランタイムには、`byte[]` 配列との間C#で簡単にマップできる `ByteString` 型が用意されています。

## <a name="other-net-primitive-types"></a>その他の .NET プリミティブ型

### <a name="dates-and-times"></a>日付と時刻

ネイティブスカラー型では、日付と時刻の値が提供さC#れません。これは、の <xref:System.DateTimeOffset>、<xref:System.DateTime>、および <xref:System.TimeSpan>と同じです。 これらの型は、Google の "既知の型" 拡張機能の一部を使用して指定できます。これにより、サポートされているプラットフォーム全体で、より複雑なフィールド型に対するコード生成とランタイムサポートが提供されます。 次の表は、日付と時刻の型を示しています。

| C# 型 | Protobuf 既知の型 |
| ------- | ------------------------ |
| `DateTimeOffset` | `google.protobuf.Timestamp` |
| `DateTime` | `google.protobuf.Timestamp` |
| `TimeSpan` | `google.protobuf.Duration` |

```protobuf  
syntax = "proto3"

import "google/protobuf/duration.proto";  
import "google/protobuf/timestamp.proto";

message Meeting {

    string subject = 1;
    google.protobuf.Timestamp time = 2;
    google.protobuf.Duration duration = 3;

}  
```

C#クラスで生成されるプロパティは、.net の日付型と時刻型ではありません。 プロパティは、`DateTimeOffset`、`DateTime`、および `TimeSpan`との間で変換を行うためのメソッドを提供する、`Google.Protobuf.WellKnownTypes` 名前空間の `Timestamp` クラスと `Duration` クラスを使用します。

```csharp
// Create Timestamp and Duration from .NET DateTimeOffset and TimeSpan
var meeting = new Meeting
{
    Time = Timestamp.FromDateTimeOffset(meetingTime), // also FromDateTime()
    Duration = Duration.FromTimeSpan(meetingLength)
};

// Convert Timestamp and Duration to .NET DateTimeOffset and TimeSpan
DateTimeOffset time = meeting.Time.ToDateTimeOffset();
TimeSpan? duration = meeting.Duration?.ToTimeSpan();
```

> [!NOTE]
> `Timestamp` 型は UTC 時刻で動作します。`DateTimeOffset` 値は常に0のオフセットを持ち、`DateTime.Kind` プロパティは常に `DateTimeKind.Utc`になります。

### <a name="systemguid"></a>System.Guid

他のプラットフォームで `UUID` として知られている <xref:System.Guid> の種類は、Protobuf によって直接サポートされておらず、既知の型もありません。 最適な方法は、標準 `8-4-4-4-12` 16 進数形式 (`45a9fda3-bd01-47a9-8460-c1cd7484b0b3`など) を使用して `Guid` 値を `string` フィールドとして処理することです。これは、すべての言語とプラットフォームで解析できます。 `Guid` 値には `bytes` フィールドを使用しないでください。これにより、エンディアンの問題により、Java などの他のプラットフォームとの対話で動作が不安定になる可能性があります。

### <a name="nullable-types"></a>Null 許容型

のC# Protobuf コード生成では、`int32`の `int` などのネイティブ型を使用します。 つまり、値は常に含まれ、null にすることはできません。 C#コードで `int?` を使用するなど、明示的な null を必要とする値の場合、Protobuf の "既知の型" にはC# 、null 許容型にコンパイルされるラッパーが含まれます。 これらを使用するには、次のように `wrappers.proto` を `.proto` ファイルにインポートします。

```protobuf  
syntax = "proto3"

import "google/protobuf/wrappers.proto"

message Person {

    ...
    google.protobuf.Int32Value age = 5;

}
```

Protobuf は、生成されたメッセージプロパティに simple `T?` (`int?`など) を使用します。

次の表に、ラッパー型とそれに対応C#する型の完全な一覧を示します。

| C# 型   | 既知の型ラッパー       |
| --------- | ----------------------------- |
| `double?` | `google.protobuf.DoubleValue` |
| `float?`  | `google.protobuf.FloatValue`  |
| `int?`    | `google.protobuf.Int32Value`  |
| `long?`   | `google.protobuf.Int64Value`  |
| `uint?`   | `google.protobuf.UInt32Value` |
| `ulong?`  | `google.protobuf.UInt64Value` |

既知の型 `Timestamp` と `Duration` は、クラスとして .NET で表現されるため、null 許容バージョンを必要としませんが `DateTimeOffset` または `TimeSpan`に変換するときに、これらの型のプロパティで null をチェックすることが重要です。

## <a name="decimals"></a>10 進

Protobuf は、.NET `decimal` 型をネイティブでサポートしていません。 `double` と `float`だけです。 Protobuf プロジェクトでは、標準 `Decimal` 型を既知の型に追加することができますが、それをサポートする言語とフレームワークはプラットフォームでサポートされていますが、まだ実装されていません。

.NET クライアントとサーバー間の安全なシリアル化に使用できる `decimal` 型を表すメッセージ定義を作成することはできますが、他のプラットフォームの開発者は、使用されている形式を理解し、独自の処理を実装する必要があります。

### <a name="creating-a-custom-decimal-type-for-protobuf"></a>Protobuf のカスタム Decimal 型の作成

非常に単純な実装は、一部の Google Api で使用される非標準の `Money` 型に似ていますが、`currency` フィールドはありません。

```protobuf
package CustomTypes;

// Example: 12345.6789 -> { units = 12345, nanos = 678900000 }
message Decimal {

    // Whole units part of the amount
    int64 units = 1;

    // Nano units of the amount (10^-9)
    // Must be same sign as units
    sfixed32 nanos = 2;
}
```

`nanos` フィールドは、`0.999_999_999` から `-0.999_999_999`までの値を表します。 たとえば、`decimal` 値 `1.5m` は `{ units = 1, nanos = 500_000_000 }` として表されます (この例の `nanos` フィールドでは、より大きな値に対して `sfixed32` よりも効率的にエンコードされる `int32` 型を使用しています)。 `units` フィールドが負の値の場合、`nanos` フィールドにも負の値を指定する必要があります。

> [!NOTE]
> `decimal` 値をバイト文字列としてエンコードするためのアルゴリズムは他にもいくつかありますが、このメッセージはどのようなものでも理解しやすく、異なるプラットフォームの *[エンディアン](https://en.wikipedia.org/wiki/Endianness)* の影響を受けません。

この型と BCL `decimal` 型の間の変換は、次C#のようにで実装できます。

```csharp
namespace CustomTypes
{
    public partial class GrpcDecimal
    {
        private const decimal NanoFactor = 1_000_000_000;
        public GrpcDecimal(long units, int nanos)
        {
            Units = units;
            Nanos = nanos;
        }

        public long Units { get; }
        public int Nanos { get; }

        public static implicit operator decimal(CustomTypes.Decimal grpcDecimal)
        {
            return grpcDecimal.Units + grpcDecimal.Nanos / NanoFactor;
        }

        public static implicit operator CustomTypes.Decimal(decimal value)
        {
            var units = decimal.ToInt64(value);
            var nanos = decimal.ToInt32((value - units) * NanoFactor);
            return new CustomTypes.Decimal(units, nanos);
        }
    }
}
```

> [!IMPORTANT]
> このようなカスタムユーティリティメッセージ型を使用する場合は常に、他の開発者が独自の言語またはフレームワークで同等の型との間で変換を実装できるように、`.proto` にコメントを付けて文書化**する必要があり**ます。

>[!div class="step-by-step"]
>[前へ](protobuf-messages.md)
>[次へ](protobuf-nested-types.md)
