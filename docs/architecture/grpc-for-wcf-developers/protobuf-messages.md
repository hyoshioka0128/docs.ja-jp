---
title: Protobuf messages-WCF 開発者向け gRPC
description: Protobuf メッセージを IDL で定義し、C# で生成する方法について説明します。
ms.date: 09/09/2019
ms.openlocfilehash: 6fc7b9c34810abaa8d674af56d1517a5cf87521b
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325037"
---
# <a name="protobuf-messages"></a>Protobuf メッセージ

このセクションでは、ファイルでプロトコルバッファー (Protobuf) メッセージを宣言する方法について説明し `.proto` ます。 ここでは、フィールドの数値と型の基本的な概念について説明し、コンパイラによって生成される C# コードを見ていき `protoc` ます。

この章の残りの部分では、Protobuf でさまざまな種類のデータがどのように表現されるかについて詳しく説明します。

## <a name="declaring-a-message"></a>メッセージの宣言

Windows Communication Foundation (WCF) では、 `Stock` 株式市場取引アプリケーションのクラスが次の例のように定義されている場合があります。

```csharp
namespace TraderSys
{
    [DataContract]
    public class Stock
    {
        [DataMember]
        public int Id { get; set;}
        [DataMember]
        public string Symbol { get; set;}
        [DataMember]
        public string DisplayName { get; set;}
        [DataMember]
        public int MarketId { get; set; }
    }
}
```

Protobuf で同等のクラスを実装するには、ファイルでそれを宣言する必要があり `.proto` ます。 コンパイラは、 `protoc` ビルド処理の一部として .net クラスを生成します。

```protobuf
syntax = "proto3";

option csharp_namespace = "TraderSys";

message Stock {

    int32 id = 1;
    string symbol = 2;
    string display_name = 3;
    int32 market_id = 4;

}  
```

最初の行は、使用されている構文のバージョンを宣言します。 言語のバージョン3は2016でリリースされました。 これは、gRPC サービスに推奨されるバージョンです。

行は、生成された `option csharp_namespace` C# 型に使用される名前空間を指定します。 このオプションは、 `.proto` ファイルが他の言語用にコンパイルされるときには無視されます。 Protobuf ファイルには、多くの場合、複数の言語の言語固有のオプションが含まれています。

メッセージ定義では、 `Stock` 4 つのフィールドを指定します。 各には、型、名前、およびフィールド番号があります。

## <a name="field-numbers"></a>フィールド番号

フィールド番号は Protobuf の重要な部分です。 これらは、バイナリエンコードデータ内のフィールドを識別するために使用されます。つまり、サービスのバージョンごとに変更することはできません。 長所は、下位互換性と上位互換性が可能であることです。 クライアントとサービスは、不足値が処理される可能性がある限り、認識していないフィールド番号を無視します。

バイナリ形式では、フィールド番号が型識別子と結合されます。 1 ~ 15 のフィールド番号は、その型で1バイトとしてエンコードできます。 16から2047の数値は2バイトになります。 何らかの理由でメッセージに2047を超えるフィールドが必要な場合は、より高い値にすることができます。 フィールド番号が 1 ~ 15 の1バイト識別子ではパフォーマンスが向上します。そのため、最も基本的で頻繁に使用されるフィールドで使用する必要があります。

## <a name="types"></a>型

型宣言は、Protobuf のネイティブスカラーデータ型を使用しています。詳細については、[次のセクション](protobuf-data-types.md)で説明します。 この章の残りの部分では、Protobuf の組み込み型について説明し、一般的な .NET 型にどのように関連しているかを示します。

> [!NOTE]
> Protobuf は型をネイティブでサポートしていない `decimal` ため、 `double` 代わりにを使用します。 完全な10進数の有効桁数を必要とするアプリケーションについては、この章の次の部分にある10進数[に関するセクション](protobuf-data-types.md#decimals)を参照してください。

## <a name="the-generated-code"></a>生成されたコード

アプリケーションをビルドすると、Protobuf はメッセージごとにクラスを作成し、ネイティブな型を C# 型にマップします。 生成された `Stock` 型のシグネチャは次のようになります。

```csharp
public class Stock
{
    public int Id { get; set; }
    public string Symbol { get; set; }
    public string DisplayName { get; set; }
    public int MarketId { get; set; }
}
```

生成される実際のコードは、これよりもはるかに複雑です。 その理由は、各クラスには、それ自体をバイナリワイヤ形式にシリアル化および逆シリアル化するために必要なすべてのコードが含まれているからです。

### <a name="property-names"></a>プロパティ名

Protobuf コンパイラはプロパティ名に適用されることに注意して `PascalCase` ください。ただし、これらは `snake_case` ファイルに含まれてい `.proto` ます。 [Protobuf スタイルガイド](https://developers.google.com/protocol-buffers/docs/style)では、メッセージ定義でを使用して、 `snake_case` 他のプラットフォームのコード生成によって意図した規約のケースが生成されるようにすることを推奨しています。

>[!div class="step-by-step"]
>[前へ](protocol-buffers.md)
>[次へ](protobuf-data-types.md)
