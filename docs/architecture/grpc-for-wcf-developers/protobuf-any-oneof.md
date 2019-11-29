---
title: Protobuf variant 型のフィールドと、WCF 開発者向け gRPC の組み合わせ
description: Any 型および Oneof キーワードを使用して、メッセージ内のバリアントオブジェクト型を表す方法について説明します。
ms.date: 09/09/2019
ms.openlocfilehash: af3ba22c238aa80a8c6119f62d5d8914770cad68
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73971617"
---
# <a name="protobuf-any-and-oneof-fields-for-variant-types"></a>Protobuf variant 型のフィールドをすべて使用します。

WCF での動的プロパティ型 (`object`型のプロパティ) の処理は複雑です。 シリアライザーを指定する必要があります。また、 [Knowntype](xref:System.Runtime.Serialization.KnownTypeAttribute)属性を指定する必要があります。

Protobuf には、複数の型の値を処理するための2つの簡単なオプションが用意されています。 `Any` 型は既知の Protobuf メッセージ型を表すことができますが、`oneof` キーワードを使用すると、特定のメッセージで設定できるフィールドの範囲が1つだけであることを指定できます。

## <a name="any"></a>任意

`Any` は、Protobuf の "既知の型" の1つです。サポートされているすべての言語の実装で、便利で再利用可能なメッセージ型のコレクションです。 `Any` の種類を使用するには、`google/protobuf/any.proto` 定義をインポートする必要があります。

```protobuf
syntax "proto3"

import "google/protobuf/any.proto"

message Stock {
    // Stock-specific data
}

message Currency {
    // Currency-specific data
}

message ChangeNotification {
    int32 id = 1;
    google.protobuf.Any instrument = 2;
}
```

C#コードでは、`Any` クラスに、フィールドの設定、メッセージの抽出、および型のチェックを行うメソッドが用意されています。

```csharp
public void FormatChangeNotification(ChangeNotification change)
{
    if (change.Instrument.Is(Stock.Descriptor))
    {
        FormatStock(change.Instrument.Unpack<Stock>());
    }
    else if (change.Instrument.Is(Currency.Descriptor))
    {
        FormatCurrency(change.Instrument.Unpack<Currency>());
    }
    else
    {
        throw new ArgumentException("Unknown instrument type");
    }
}
```

生成された各型の `Descriptor` 静的フィールドは、`Any` フィールド型を解決するために Protobuf の内部リフレクションコードによって使用されます。 `TryUnpack<T>` メソッドもありますが、`T` の初期化されていないインスタンスは失敗した場合でも作成されるため、上記のように `Is` メソッドを使用することをお勧めします。

## <a name="oneof"></a>うち

Oneof フィールドは言語機能です。 `oneof` キーワードは、メッセージクラスを生成するときにコンパイラによって処理されます。 `oneof` を使用して `ChangeNotification` メッセージを指定する場合は、次のようになります。

```protobuf
message Stock {
    // Stock-specific data
}

message Currency {
    // Currency-specific data
}

message ChangeNotification {
  int32 id = 1;
  oneof instrument {
    Stock stock = 2;
    Currency currency = 3;
  }
}
```

`oneof` セット内のフィールドは、メッセージの宣言全体で一意のフィールド番号を持つ必要があります。

`oneof`を使用すると、生成C#されるコードには、どのフィールドが設定されているかを指定する列挙が含まれます。 列挙をテストして、どのフィールドが設定されているかを調べることができます。 設定されていないフィールドは、例外をスローするのではなく、`null` または既定値を返します。

```csharp
public void FormatChangeNotification(ChangeNotification change)
{
    switch (change.InstrumentCase)
    {
        case ChangeNotification.InstrumentOneofCase.None:
            return;
        case ChangeNotification.InstrumentOneofCase.Stock:
            FormatStock(change.Stock);
            break;
        case ChangeNotification.InstrumentOneofCase.Currency:
            FormatCurrency(change.Currency);
            break;
        default:
            throw new ArgumentException("Unknown instrument type");
    }
}
```

`oneof` セットの一部であるフィールドを設定すると、セット内の他のすべてのフィールドが自動的にクリアされます。 `oneof`で `repeated` を使用することはできません。 代わりに、この制限を回避するために、繰り返しフィールドまたは `oneof` 設定を使用して、入れ子になったメッセージを作成できます。

>[!div class="step-by-step"]
>[前へ](protobuf-reserved.md)
>[次へ](protobuf-enums.md)
