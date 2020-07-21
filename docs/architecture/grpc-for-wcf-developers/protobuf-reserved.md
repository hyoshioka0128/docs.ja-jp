---
title: プロトブーフ予約フィールド - WCF 開発者向け gRPC
description: バージョン間の互換性のために予約済みのフィールドについて説明します。
ms.date: 09/09/2019
ms.openlocfilehash: f89513c4659a02cbc94e1c659baecb9e750acbdc
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111037"
---
# <a name="protobuf-reserved-fields"></a>Protobuf 予約フィールド

プロトコル バッファ (Protobuf) の下位互換性保証は、常に同じデータ項目を表すフィールド番号に依存します。 新しいバージョンのサービスでメッセージからフィールドを削除した場合、そのフィールド番号は再利用されません。 キーワードを使用`reserved`して、これを適用できます。

フィールドと`displayName``marketId`フィールドが、前に`Stock`定義したメッセージから削除された場合、フィールド番号は次の例のように予約する必要があります。

```protobuf
syntax "proto3";

message Stock {

    reserved 3, 4;
    int32 id = 1;
    string symbol = 2;

}
```

また、キーワードは`reserved`、将来追加される可能性のあるフィールドのプレースホルダーとして使用することもできます。 `to`キーワードを使用して、連続するフィールド番号を範囲として表現できます。

```protobuf
syntax "proto3";

message Info {

    reserved 2, 9 to 11, 15;
    // ...
}
```

>[!div class="step-by-step"]
>[前次](protobuf-repeated.md)
>[Next](protobuf-any-oneof.md)
