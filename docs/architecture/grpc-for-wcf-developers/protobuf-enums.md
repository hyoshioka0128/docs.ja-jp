---
title: Protobuf 列挙型-WCF 開発者向け gRPC
description: Protobuf で列挙型を宣言して使用する方法について説明します。
ms.date: 09/09/2019
ms.openlocfilehash: 4ea4d03bede2a9ebfd1f2c3ee56f299e918800e9
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73971576"
---
# <a name="protobuf-enumerations"></a>Protobuf 列挙型

Protobuf は列挙型をサポートしています。前のセクションでは、列挙型を使用して `oneof` フィールドの型を決定しています。 独自の列挙型を定義すると、Protobuf は列挙型C#にコンパイルします。 Protobuf は異なる言語で使用できるため、列挙型の名前付け規則は規則とC#は異なります。 ただし、コードジェネレーターは巧妙で、名前を従来C#のケースに変換します。 フィールド名に対応する Pascal 形式が列挙名で始まる場合は、その名前が削除されます。

たとえば、この Protobuf 列挙型では、フィールドの先頭に `ACCOUNT_STATUS`が付きます。これは、Pascal 形式の enum name: `AccountStatus`と同じです。

```protobuf
enum AccountStatus {
  ACCOUNT_STATUS_UNKNOWN = 0;
  ACCOUNT_STATUS_PENDING = 1;
  ACCOUNT_STATUS_ACTIVE = 2;
  ACCOUNT_STATUS_SUSPENDED = 3;
  ACCOUNT_STATUS_CLOSED = 4;
}
```

そのため、ジェネレーターは、 C#次のコードと同等の列挙型を作成します。

```csharp
public enum AccountStatus
{
    Unknown = 0,
    Pending = 1,
    Active = 2,
    Suspended = 3,
    Closed = 4
}
```

Protobuf 列挙型の定義には、最初のフィールドとして0の定数を**指定しなければなりません**。 C#と同様に、同じ値を持つ複数のフィールドを宣言できますが、列挙型の `allow_alias` オプションを使用して、このオプションを明示的に有効にする必要があります。

```protobuf
enum AccountStatus {
  option allow_alias = true;
  ACCOUNT_STATUS_UNKNOWN = 0;
  ACCOUNT_STATUS_PENDING = 1;
  ACCOUNT_STATUS_ACTIVE = 2;
  ACCOUNT_STATUS_SUSPENDED = 3;
  ACCOUNT_STATUS_CLOSED = 4;
  ACCOUNT_STATUS_CANCELLED = 4;
}
```

列挙は、`.proto` ファイルの最上位レベルで宣言することも、メッセージ定義内で入れ子にすることもできます。 入れ子になったメッセージと同様に、入れ子になった列挙型は、生成された message クラスの `.Types` 静的クラス内で宣言されます。

Protobuf で生成された列挙型に[[Flags]](xref:System.FlagsAttribute)属性を適用する方法はありません。 Protobuf はビットごとの列挙の組み合わせを認識しません。 次の例を見てみましょう。

```protobuf
enum Region {
  REGION_NONE = 0;
  REGION_NORTH_AMERICA = 1;
  REGION_SOUTH_AMERICA = 2;
  REGION_EMEA = 4;
  REGION_APAC = 8;
}

message Product {
  Region available_in = 1;
}
```

`product.AvailableIn` を `Region.NorthAmerica | Region.SouthAmerica`に設定すると、`3`整数値としてシリアル化されます。 クライアントまたはサーバーが値を逆シリアル化しようとすると、`3` の列挙型の定義に一致するものが見つからず、結果が `Region.None`されます。

Protobuf で複数の列挙値を操作する最善の方法は、列挙型の `repeated` フィールドを使用することです。

>[!div class="step-by-step"]
>[前へ](protobuf-any-oneof.md)
>[次へ](protobuf-maps.md)
