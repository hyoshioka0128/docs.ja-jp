---
title: ユーザー定義型
ms.date: 07/20/2015
f1_keywords:
- UserDefined
- UDT
- vb.UDT
- User-Defined
- vb.UserDefined
- vb.User-Defined
helpviewer_keywords:
- user-defined data types [Visual Basic], Visual Basic
- user-defined types
- structures [Visual Basic], as user-defined data types
- user-defined types [Visual Basic], Visual Basic
- user-defined types [Visual Basic], structure declaration
- user-defined types [Visual Basic], structures in Visual Basic
- user-defined data types [Visual Basic], structure declaration
- data types [Visual Basic], assigning
- Structure statement [Visual Basic]
- data types [Visual Basic], user-defined
- user-defined data types [Visual Basic], structures in Visual Basic
- user-defined data types
- types [Visual Basic], user-defined
ms.assetid: be913dca-a364-4a51-96a1-549a1b390b0a
ms.openlocfilehash: fbd9536a54d7fb471d6cb2e130b14a84e40a4940
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84415493"
---
# <a name="user-defined-data-type"></a>ユーザー定義型

定義した形式でデータを保持します。 `Structure` ステートメントは形式を定義します。

以前のバージョンの Visual Basic はユーザー定義型 (UDT) をサポートします。 現在のバージョンでは、UDT が*構造体*に拡張されています。 構造体は、さまざまなデータ型の 1 つ以上の*メンバー*を連結したものです。 Visual Basic は、構造体を 1 つの単位として扱いますが、そのメンバーに個別にアクセスすることもできます。

## <a name="remarks"></a>Remarks

さまざまなデータ型を 1 つの単位に結合する必要がある場合、またはニーズに応える基本データ型がない場合は、構造体のデータ型を定義して使用します。

構造体のデータ型の既定値は、各メンバーの既定値の組み合わせで構成されます。

## <a name="declaration-format"></a>宣言の形式

構造体宣言は、[Structure ステートメント](../statements/structure-statement.md)で始まり、`End Structure` ステートメントで終了します。 `Structure` ステートメントは、構造体の名前を指定します。これは、構造体で定義されるデータ型の識別子でもあります。 コードの他の部分では、この識別子を使用して、この構造体のデータ型の変数、パラメーター、および関数の戻り値を宣言できます。

`Structure` ステートメントと `End Structure` ステートメントの間の宣言では、構造体のメンバーを定義します。

## <a name="member-access-levels"></a>メンバーのアクセス レベル

すべてのメンバーを宣言するには、[Dim ステートメント](../statements/dim-statement.md)を使用するか、[Public](../modifiers/public.md)、[Friend](../modifiers/friend.md)、[Private](../modifiers/private.md) などのアクセス レベルを指定するステートメントを使用する必要があります。 `Dim` ステートメントを使用する場合、アクセス レベルの既定値はパブリックです。

## <a name="programming-tips"></a>プログラミングのヒント

- **メモリの使用量。**  他のすべての複合データ型と同様に、構造体の総メモリ使用量を計算する場合、各メンバーのストレージ割り当ての公称サイズを単に合計しただけでは安全ではありません。 さらに、メモリ内に格納される順序が宣言の順序と同じであると仮定するのも安全ではありません。 構造体のストレージ レイアウトを制御する必要がある場合は、<xref:System.Runtime.InteropServices.StructLayoutAttribute> 属性を `Structure` ステートメントに適用します。

- **相互運用の考慮事項。** オートメーション オブジェクトや COM オブジェクトのように、.NET Framework 向けに作成されていないコンポーネントとやり取りする場合、他の環境のユーザー定義型は Visual Basic の構造体型と互換性がないことに注意してください。

- **拡大変換。** 任意の構造体のデータ型との間で自動変換が行われることはありません。 [Operator ステートメント](../statements/operator-statement.md)を使用して構造体に変換演算子を定義できます。また、各変換演算子を `Widening` または `Narrowing` として宣言できます。

- **型文字。** 構造体のデータ型には、リテラルの型文字も識別子の型文字も含まれません。

- **Framework の型。** .NET Framework に対応する型はありません。 すべての構造体は .NET Framework クラス <xref:System.ValueType?displayProperty=nameWithType> から継承されますが、<xref:System.ValueType?displayProperty=nameWithType> に対応する個別の構造体はありません。

## <a name="example"></a>例

次のパラダイムは、構造体の宣言のアウトラインを示します。

```vb
[Public | Protected | Friend | Protected Friend | Private] Structure structname
    {Dim | Public | Friend | Private} member1 As datatype1
    ' ...
    {Dim | Public | Friend | Private} memberN As datatypeN
End Structure
```

## <a name="see-also"></a>関連項目

- <xref:System.ValueType>
- <xref:System.Runtime.InteropServices.StructLayoutAttribute>
- [データの種類](index.md)
- [データ型変換関数](../functions/type-conversion-functions.md)
- [変換の概要](../keywords/conversion-summary.md)
- [Structure ステートメント](../statements/structure-statement.md)
- [Widening](../modifiers/widening.md)
- [Narrowing](../modifiers/narrowing.md)
- [構造体](../../programming-guide/language-features/data-types/structures.md)
- [データ型の有効な使用方法](../../programming-guide/language-features/data-types/efficient-use-of-data-types.md)
