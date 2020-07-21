---
title: 冗語構文
description: F# プログラミング言語での詳細構文と軽量構文の違いについて説明します。
ms.date: 05/16/2016
ms.openlocfilehash: 722807695c56beb0d681b95a78ed8cb8c1df3ddf
ms.sourcegitcommit: 927b7ea6b2ea5a440c8f23e3e66503152eb85591
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81463904"
---
# <a name="verbose-syntax"></a>冗語構文

F# 言語の多くの構文には、*詳細な構文*と*簡易構文*の 2 種類の構文が用意されています。 詳細な構文は、一般的には使用されませんが、インデントに対する感度が低いという利点があります。 軽量構文は短く、インデントを使用して、 `begin`、`end`などの`in`追加のキーワードではなく、コンストラクトの先頭と末尾を通知します。 既定の構文は、簡易構文です。 このトピックでは、簡易構文が有効でない場合の F# コンストラクトの構文について説明します。 詳細構文は常に有効であるため、簡易構文を有効にしても、一部の構文では詳細構文を使用できます。 ディレクティブを使用して、簡易構文を`#light "off"`無効にすることができます。

## <a name="table-of-constructs"></a>コンストラクトの表

次の表は、2 つの形式の間に違いがあるコンテキストでの F# 言語構成要素の軽量構文と詳細構文を示しています。 この表では、山かっこ (&lt;&gt;) でユーザーが指定した構文要素を囲みます。 これらの構文で使用される構文の詳細については、各言語構成要素のドキュメントを参照してください。

<table>
<tr>
<th>言語構成</th>
<th>軽量構文</th>
<th>詳細構文</th>
</tr>
<tr>
<td>
複合式
</td>
<td>

```xml
<expression1 />
<expression2 />
```

</td><td>

```fsharp
<expression1>; <expression2>
```

</td>
</tr>
<tr><td>

ネストされた`let`バインディング

</td><td>

```fsharp
let f x =
    let a = 1
    let b = 2
    x + a + b
```

</td><td>

```fsharp
let f x =
    let a = 1 in
    let b = 2 in
    x + a + b
```

</td>
</tr>
<tr><td>
コード ブロック
</td><td>

```fsharp
(
    <expression1>
    <expression2>
)
```

</td><td>

```fsharp
begin
    <expression1>;
    <expression2>;
end
```

</td>
</tr>
<tr><td>
`for...do`
</td><td>

```fsharp
for counter = start to finish do
    ...
```

</td><td>

```fsharp
for counter = start to finish do
    ...
done
```

</td>
</tr>
<tr><td>
`while...do`
</td><td>

```fsharp
while <condition> do
    ...
```

</td><td>

```fsharp
while <condition> do
    ...
done
```

</td>
</tr>
<tr><td>
`for...in`
</td><td>

```fsharp
for var in start .. finish do
    ...
```

</td><td>

```fsharp
for var in start .. finish do
    ...
done
```

</td>
</tr>
<tr><td>
`do`
</td><td>

```fsharp
do
    ...
```

</td><td>

```fsharp
do
    ...
in
```

</td>
</tr>
<tr><td>レコード (record)
</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    <value-or-member-definitions>
```

</td><td>

```fsharp
type <record-name> =
    {
        <field-declarations>
    }
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>class
</td><td>

```fsharp
type <class-name>(<params>) =
    ...
```

</td><td>

```fsharp
type <class-name>(<params>) =
    class
        ...
    end
```

</td>
</tr>
<tr><td>structure</td><td>

```fsharp
[<StructAttribute>]
type <structure-name> =
    ...
```

</td><td>

```fsharp
type <structure-name> =
    struct
        ...
    end
```

</td>
</tr>
<tr><td>差別化組合</td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    <value-or-member definitions>
```

</td><td>

```fsharp
type <union-name> =
    | ...
    | ...
    ...
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>interface</td><td>

```fsharp
type <interface-name> =
    ...
```

</td><td>

```fsharp
type <interface-name> =
    interface
        ...
    end
```

</td>
</tr>
<tr><td>オブジェクト式</td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
        <interface-implementations>
}
```

</td><td>

```fsharp
{ new <type-name>
    with
        <value-or-member-definitions>
    end
    <interface-implementations>
}
```

</td>
</tr>
<tr><td>インターフェイスの実装</td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
interface <interface-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>型拡張子</td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
```

</td><td>

```fsharp
type <type-name>
    with
        <value-or-member-definitions>
    end
```

</td>
</tr>
<tr><td>name</td><td>

```fsharp
module <module-name> =
    ...
```

</td><td>

```fsharp
module <module-name> =
    begin
        ...
    end
```

</td>
</tr>
</table>

## <a name="see-also"></a>関連項目

- [F# 言語リファレンス](index.md)
- [コンパイラ ディレクティブ](compiler-directives.md)
- [コードのフォーマットに関するガイドライン](../style-guide/formatting.md)
