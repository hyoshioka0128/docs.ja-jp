---
title: F# 4.7 の新機能 - F# ガイド
description: F# 4.7 で利用可能な新機能の概要を取得します。
ms.date: 11/27/2019
ms.openlocfilehash: 7a6e744a398719bcb55d168dd700459e0b122dd6
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185869"
---
# <a name="whats-new-in-f-47"></a>F# 4.7 の新機能

F# 4.7 では、F# 言語に複数の改良が加えました。

## <a name="get-started"></a>はじめに

F# 4.7 は、すべての .NET コアディストリビューションと Visual Studio ツールで使用できます。 [F# の使用を開始](../get-started/index.md)して、詳細を確認してください。

## <a name="language-version"></a>言語バージョン

F# 4.7 コンパイラでは、プロジェクト ファイルのプロパティを使用して、有効な言語バージョンを設定する機能が導入されています。

```xml
<PropertyGroup>
    <LangVersion>preview</LangVersion>
</PropertyGroup>
```

値`4.6`、 、 、`4.7``latest`および`preview`に設定できます。 既定では、 `latest`です。

に`preview`設定すると、コンパイラは、コンパイラに実装されているすべての F# プレビュー機能をアクティブ化します。

## <a name="implicit-yields"></a>暗黙的な利回り

配列、リスト、シーケンス、または`yield`計算式で、型を推論できる場合にキーワードを適用する必要がなくなりました。 次の例では、F# 4.7 より前の`yield`各エントリに対して、両方の式にステートメントが必要でした。

```fsharp
let s = seq { 1; 2; 3; 4; 5 }

let daysOfWeek includeWeekend =
    [
        "Monday"
        "Tuesday"
        "Wednesday"
        "Thursday"
        "Friday"
        if includeWeekend then
            "Saturday"
            "Sunday"
    ]
```

単一`yield`のキーワードを導入する場合は、他のすべての項目`yield`もそのキーワードに適用されている必要があります。

暗黙的な利回りは、シーケンスの平坦化などの処理`yield!`にも使用される式で使用される場合はアクティブ化されません。 このような場合は、今日`yield`も使用し続ける必要があります。

## <a name="wildcard-identifiers"></a>ワイルドカード識別子

クラスを含む F# コードでは、メンバー宣言では自己識別子を常に明示的に指定する必要があります。 しかし、自己識別子が使用されていない場合、伝統的に、名前のない自己識別子を示すためにダブルアンダースコアを使用することが慣例でした。 下線を 1 つ使用できるようになりました。

```fsharp
type C() =
    member _.M() = ()
```

これは`for`ループにも当てはまります。

```fsharp
for _ in 1..10 do printfn "Hello!"
```

## <a name="indentation-relaxations"></a>インデントの緩和

F# 4.7 より前のバージョンでは、プライマリ コンストラクターと静的メンバー引数のインデント要件に過剰なインデントが必要でした。 これで、1 つのインデント スコープのみが必要になります。

```fsharp
type OffsideCheck(a:int,
    b:int, c:int,
    d:int) = class end

type C() =
    static member M(a:int,
        b:int, c:int,
        d:int) = 1
```
