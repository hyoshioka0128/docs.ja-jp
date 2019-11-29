---
title: Protobuf の予約済みフィールド-WCF 開発者向け gRPC
description: バージョン間の互換性のために予約されているフィールドについて説明します。
ms.date: 09/09/2019
ms.openlocfilehash: e589cd38a712ce014fa2c4d847fbde359d538dd0
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967314"
---
# <a name="protobuf-reserved-fields"></a>Protobuf 予約フィールド

Protobuf の下位互換性の保証は、常に同じデータ項目を表すフィールド番号に依存しています。 新しいバージョンのサービスでメッセージからフィールドが削除された場合、そのフィールド番号は再利用しないでください。 これは、`reserved` キーワードを使用して適用できます。 `displayName` フィールドと `marketId` フィールドが、前に定義した `Stock` メッセージから削除された場合は、次の例のようにフィールド番号を予約する必要があります。

```protobuf
syntax "proto3";

message Stock {

    reserved 3, 4;
    int32 id = 1;
    string symbol = 2;

}
```

`reserved` キーワードは、今後追加される可能性のあるフィールドのプレースホルダーとして使用することもできます。 連続したフィールド番号は、`to` キーワードを使用して範囲として表すことができます。

```protobuf
syntax "proto3";

message Info {

    reserved 2, 9 to 11, 15;
    // ...
}
```

>[!div class="step-by-step"]
>[前へ](protobuf-repeated.md)
>[次へ](protobuf-any-oneof.md)
