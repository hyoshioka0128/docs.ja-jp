---
title: 構造体
description: F# 構造体について説明します。
ms.date: 05/16/2016
ms.openlocfilehash: 1e9652cc4776e4d1d52eb20e41b6dd87a6c5ba05
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "79401125"
---
# <a name="structures"></a>構造体

*構造体*は、データ量が少なく単純な動作を持つ型のクラスよりも効率的なコンパクト オブジェクト型です。

## <a name="syntax"></a>構文

```fsharp
[ attributes ]
type [accessibility-modifier] type-name =
    struct
        type-definition-elements-and-members
    end
// or
[ attributes ]
[<StructAttribute>]
type [accessibility-modifier] type-name =
    type-definition-elements-and-members
```

## <a name="remarks"></a>解説

構造体は*値型*です。 クラスやレコードとは異なり、構造体のセマンティクスは値渡しです。 これは、主にアクセスおよびコピーが頻繁に行われるデータの小規模な集約に有用であることを意味します。

上記の構文では、2 つの形式が示されています。 1 番目のものは軽量構文ではないものの、頻繁に使用されます。これは、`struct` キーワードと `end` キーワードを使用する場合に、2 番目のものに出現する `StructAttribute` 属性を省略できるためです。 `StructAttribute` は省略して単に `Struct` とすることができます。

前*の構文の型定義要素とメンバー*は、メンバーの宣言と定義を表します。 構造体にはコンス トラクター、可変フィールド、および不変フィールドを含めることができ、メンバーとインターフェイス実装を宣言できます。 詳細については、「[メンバー](./members/index.md)」を参照してください。

構造体は、継承に参加することも、`let` または `do` バインディングを含めることも、それ自身の型のフィールドを再帰的に含めることもできません (ただし、それ自身の型を参照する参照セルを含めることができます)。

構造体では `let` バインディングは使用できないため、`val` キーワードを使用して構造体のフィールドを宣言する必要があります。 `val` キーワードではフィールドとその型が定義されますが、初期化は実行できません。 代わりに、`val` 宣言がゼロまたは null に初期化されます。 このため、暗黙のコンストラクター (宣言で構造体名の直後に指定されるパラメーター) を含む構造体では、`val` 宣言に `DefaultValue` 属性で注釈を付ける必要があります。 定義されたコンストラクターを含む構造体でも、ゼロ初期化がサポートされます。 したがって、`DefaultValue` 属性は、このようなゼロ値がフィールドに対して有効であることの宣言になります。 構造体の暗黙的なコンストラクターでは動作は実行されません。これは、`let` バインディングと `do` バインディングがその型では許可されていないためですが、渡された暗黙のコンストラクターのパラメーター値はプライベート フィールドとして使用できます。

明示的なコンストラクターにフィールド値の初期化が含まれる場合があります。 明示的なコンストラクターを含む構造体がある場合も、ゼロ初期化がサポートされます。ただし、明示的なコンストラクターと競合するため、`DefaultValue` 宣言では `val` 属性を使用しません。 宣言の詳細`val`については、「[明示的なフィールド:`val`キーワード](./members/explicit-fields-the-val-keyword.md)」を参照してください。

構造体では属性およびアクセシビリティ修飾子が許可されており、その他の型と同じ規則に従います。 詳細については、「[属性](attributes.md)と[アクセス制御](access-control.md)」を参照してください。

次のコード例は構造体の定義を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2501.fs)]

## <a name="byreflike-structs"></a>構造体

like セマンティクスに`byref`準拠できる独自の構造体を定義できます。 [Byrefs](byrefs.md) これは<xref:System.Runtime.CompilerServices.IsByRefLikeAttribute>属性で行われます。

```fsharp
open System
open System.Runtime.CompilerServices

[<IsByRefLike; Struct>]
type S(count1: Span<int>, count2: Span<int>) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsByRefLike`は を`Struct`意味しません。 両方とも型に存在する必要があります。

F#`byref`の "-like" 構造体は、スタックにバインドされた値型です。 マネージ ヒープには割り当てが行きまとい。 `byref`-like 構造体は、有効期間と非キャプチャに関する強力なチェックのセットで実施される、高性能プログラミングに役立ちます。 ルールは次のとおりです。

- 関数パラメーター、メソッドパラメーター、ローカル変数、メソッドの戻り値として使用できます。
- クラスの静的メンバーまたはインスタンス メンバー、または通常の構造体にはできません。
- これらの関数は、どのクロージャ構造`async`(メソッドまたはラムダ式) でもキャプチャできません。
- ジェネリック パラメーターとして使用することはできません。

これらのルールは、使用を非常に強く制限しますが、安全な方法で高性能コンピューティングの約束を果たすために行います。

## <a name="readonly-structs"></a>ReadOnly 構造体

属性を使用して構造体にアコーズを<xref:System.Runtime.CompilerServices.IsReadOnlyAttribute>付けることができます。 次に例を示します。

```fsharp
[<IsReadOnly; Struct>]
type S(count1: int, count2: int) =
    member x.Count1 = count1
    member x.Count2 = count2
```

`IsReadOnly`は を`Struct`意味しません。 構造体を持つには、両方`IsReadOnly`を追加する必要があります。

この属性を使用すると、F# と C# がそれぞれと`inref<'T>`を扱うように`in ref`知らせるメタデータが生成されます。

読み取り専用構造体の中で変更可能な値を定義すると、エラーが発生します。

## <a name="struct-records-and-discriminated-unions"></a>構造体レコードと判別共用体

この`[<Struct>]`属性を使用して[、レコード](records.md)および[判別共用体](discriminated-unions.md)を構造体として表すことができます。  詳細については、各記事をご覧ください。

## <a name="see-also"></a>関連項目

- [F# 言語リファレンス](index.md)
- [クラス](classes.md)
- [レコード](records.md)
- [メンバー](./members/index.md)
