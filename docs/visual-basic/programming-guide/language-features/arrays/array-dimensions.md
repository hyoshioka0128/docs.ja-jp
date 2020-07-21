---
title: 配列の次元
ms.date: 07/20/2015
helpviewer_keywords:
- dimensions, arrays
- arrays [Visual Basic], dimensions
- arrays [Visual Basic], rectangular
- arrays [Visual Basic], rank
- rectangular arrays
- ranking, arrays
ms.assetid: 385e911b-18c1-4e98-9924-c6d279101dd9
ms.openlocfilehash: f971f0c3693177adbcb8869d487e3ad41d49ddc2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413105"
---
# <a name="array-dimensions-in-visual-basic"></a>Visual Basic における配列の次元

1 つの "*次元*" は、配列の要素の指定を変更できる 1 つの方向です。 月の毎日の売上合計を保持する配列には、1 つの次元 (月の日付) が含まれます。 月の毎日の部門別売上合計を保持する配列には、2 つの次元 (部門番号と日付) が含まれます。 配列の次元数は、その次元の "*ランク*" と呼ばれます。

> [!NOTE]
> <xref:System.Array.Rank%2A> プロパティを使用すると、配列の次元数を確認できます。

## <a name="working-with-dimensions"></a>次元の使用

配列の要素を指定するには、その次元ごとに "*インデックス*" つまり "*添字*" を指定します。 要素は、インデックス 0 からその次元の最大インデックスまで、各次元に沿って連続しています。

次の図は、さまざまなランクの配列の概念的な構造を示しています。 図の各要素は、その要素にアクセスするインデックス値を示しています。 たとえば、インデックス `(1, 0)` を指定すると、2 次元配列の 2 行目の最初の要素にアクセスできます。

![1 次元配列のダイアグラム。](./media/array-dimensions/one-dimensional-array.gif)

![2 次元配列のダイアグラム。](./media/array-dimensions/two-dimensional-array.gif)

![3 次元配列のダイアグラム。](./media/array-dimensions/three-dimensional-array.gif)

### <a name="one-dimension"></a>1 次元

配列の多くには、各年齢の人数など、1 つの次元しか含まれません。 要素を指定するために必要なのは年齢のみで、その年齢の人数が要素に保持されています。 したがって、このような配列では 1 つのインデックスのみが使用されます。 次の例で宣言する変数には、0 から 120 までの年齢を示す "*1 次元配列*" が保持されます。

```vb
Dim ageCounts(120) As UInteger
```

### <a name="two-dimensions"></a>2 次元

配列の中には、キャンパスの各建物の各階にあるオフィスの数など、2 つの次元を持つものがあります。 要素を指定するには建物番号と階数の両方が必要で、各要素には、建物と階数の組み合わせに対応する数が保持されます。 したがって、このような配列では 2 つのインデックスが使用されます。 次の例で宣言する変数には、建物 0 から建物 40 までの 0 階から 5 階にあるオフィス数を示す "*2 次元配列* "が保持されます。

```vb
Dim officeCounts(40, 5) As Byte
```

2 次元配列は "*矩形配列*" とも呼ばれます。

### <a name="three-dimensions"></a>3 次元

配列の中には、3 次元空間の値など、3 つの次元を持つものもあります。 このような配列では 3 つのインデックスが使用されます。ここでは、インデックスは物理空間の x、y、z 座標です。 次の例で宣言する変数には、3 次元ボリュームのさまざまなポイントの気温を示す "*3 次元配列*" が保持されます。

```vb
Dim airTemperatures(99, 99, 24) As Single
```

### <a name="more-than-three-dimensions"></a>多次元 (3 次元超)

配列の次元は最大 32 次元ですが、3 次元を超えることはほとんどありません。

> [!NOTE]
> 配列に次元を追加すると、配列に必要なストレージの合計が大幅に増えるので、多次元配列を使うときは気を付けてください。

## <a name="using-different-dimensions"></a>さまざまな次元の使用

今月の毎日の売上高を追跡するとします。 次の例に示すように、31 の要素が含まれる 1 次元配列を宣言できます。各要素が 1 か月の毎日を示します。

```vb
Dim salesAmounts(30) As Double
```

次に、1 か月の毎日だけでなく、1 年のすべての月の毎日についても同じ情報を追跡するとします。 次の例に示すように、12 行 (月)、31 列 (日) の 2 次元配列を宣言できます。

```vb
Dim salesAmounts(11, 30) As Double
```

次は、複数年にわたる情報を配列で保持することにします。 5 年間の売上高を追跡する場合は、次の例に示すように、5 レイヤー、12 行、31 列の 3 次元配列を宣言できます。

```vb
Dim salesAmounts(4, 11, 30) As Double
```

各インデックスは 0 から最大値の間で変化するため、`salesAmounts` の各次元は、その次元に必要な長さよりも 1 つ小さい値として宣言されていることに注意してください。 また、新しい次元ごとに配列のサイズが増加することにも注意してください。 上記の例の 3 つのサイズは、それぞれ 31、372、および 1,860 要素です。

> [!NOTE]
> `Dim` ステートメントまたは `New` 句を 使用せずに、すべての配列を作成できます。 たとえば、<xref:System.Array.CreateInstance%2A> メソッドを呼び出すか、別のコンポーネントでこの方法で作成した配列をコードに渡すことができます。 このような配列には、0 以外の下限を設定できます。 <xref:System.Array.GetLowerBound%2A> メソッドまたは `LBound` 関数を使用すると、次元の下限をいつでもテストできます。

## <a name="see-also"></a>関連項目

- [配列](index.md)
- [配列のトラブルシューティング](troubleshooting-arrays.md)
