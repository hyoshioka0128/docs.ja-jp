---
title: 'インポート宣言: open キーワード'
description: F# インポート宣言と、完全修飾名を使用せずに参照できる要素を持つモジュールまたは名前空間を指定する方法について説明します。
ms.date: 04/04/2019
ms.openlocfilehash: 0baef27c7dc3181b9da0defb1c793fec04269c09
ms.sourcegitcommit: 348bb052d5cef109a61a3d5253faa5d7167d55ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "82021533"
---
# <a name="import-declarations-the-open-keyword"></a>インポート宣言: `open` キーワード

> [!NOTE]
> この記事の API リファレンスのリンクをクリックすると MSDN に移動します。  docs.microsoft.com API リファレンスは完全ではありません。

*インポート宣言*は、完全修飾名を使用せずに参照できる要素を持つモジュールまたは名前空間を指定します。

## <a name="syntax"></a>構文

```fsharp
open module-or-namespace-name
```

## <a name="remarks"></a>解説

毎回完全修飾名前空間またはモジュール パスを使用してコードを参照すると、記述、読み取り、保守が困難なコードが作成される場合があります。 代わりに、頻繁に`open`使用されるモジュールや名前空間にキーワードを使用すると、そのモジュールまたは名前空間のメンバーを参照するときに、完全修飾名の代わりに短い形式の名前を使用できます。 このキーワードは、C# `using` 、Visual C++、`using namespace`および Visual `Imports` Basic のキーワードに似ています。

提供されるモジュールまたは名前空間は、同じプロジェクト内、または参照先のプロジェクトまたはアセンブリ内になければなりません。 参照が指定されていない場合は、プロジェクトへの参照を追加するか、`-reference`コマンド ライン オプション (または省略形`-r`) を使用できます。 詳細については、「[コンパイラ オプション](compiler-options.md)」を参照してください。

インポート宣言では、外側の名前空間、モジュール、またはファイルの末尾まで、宣言の後に記述されているコードで名前を使用できるようになります。

複数のインポート宣言を使用する場合は、個別の行に表示されます。

次のコードは、コードを簡略化`open`するためにキーワードを使用する方法を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6801.fs)]

F# コンパイラは、複数の開いているモジュールまたは名前空間で同じ名前が発生したときにあいまいさが発生した場合に、エラーや警告を生成しません。 あいまいさが発生した場合、F# は、最近開いたモジュールまたは名前空間を優先します。 たとえば、次のコード`empty`では、 と`Seq.empty``empty``List``Seq`モジュールの両方に存在する場合でも、 を意味します。

```fsharp
open List
open Seq
printfn "%A" empty
```

したがって、同じ名前を持つメンバーを含む`List`、または`Seq`同じ名前を持つメンバーを含むモジュールまたは名前空間を開くときは注意が必要です。代わりに、修飾名の使用を検討してください。 コードがインポート宣言の順序に依存する状況は避けてください。

## <a name="namespaces-that-are-open-by-default"></a>既定で開かれている名前空間

一部の名前空間は F# コードで頻繁に使用されるため、明示的なインポート宣言を必要とせずに暗黙的に開かれます。 次の表は、既定で開かれている名前空間を示しています。

|名前空間|説明|
|---------|-----------|
|`Microsoft.FSharp.Core`|などの組み込み型の基本的な F#`int`型`float`定義が含まれています。|
|`Microsoft.FSharp.Core.Operators`|および などの`+`基本的な算術演算`*`が含まれています。|
|`Microsoft.FSharp.Collections`|および などの`List`変更できないコレクション クラスが`Array`含まれています。|
|`Microsoft.FSharp.Control`|遅延評価や非同期ワークフローなどのコントロール構成体の型が含まれています。|
|`Microsoft.FSharp.Text`|書式付き IO 関数 (関数`printf`など) を格納します。|

## <a name="autoopen-attribute"></a>自動オープン属性

アセンブリが`AutoOpen`参照されるときに名前空間またはモジュールを自動的に開く場合は、アセンブリに属性を適用できます。 また、親モジュールまたは`AutoOpen`名前空間を開いたときに、そのモジュールを自動的に開く属性をモジュールに適用することもできます。 詳細については[、「Core.AutoOpenAttribute クラス](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.autoopenattribute-class-%5bfsharp%5d)」を参照してください。

## <a name="requirequalifiedaccess-attribute"></a>必須アクセス属性が必要です

一部のモジュール、レコード、または共用体の`RequireQualifiedAccess`型では、属性を指定できます。 これらのモジュール、レコード、または共用体の要素を参照する場合は、インポート宣言を含めるかどうかに関係なく、修飾名を使用する必要があります。 この属性を、よく使用される名前を定義する型に戦略的に使用すると、名前の競合を避け、ライブラリの変更に対するコードの弾力性を高めます。 詳細については、「[クラスを必要とする」](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.requirequalifiedaccessattribute-class-%5Bfsharp%5D)を参照してください。

## <a name="see-also"></a>関連項目

- [F# 言語リファレンス](index.md)
- [名前空間](namespaces.md)
- [モジュール](modules.md)
