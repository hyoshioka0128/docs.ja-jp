---
title: '方法: プロシージャを作成する'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- Visual Basic code, reusing
- procedure declarations
- procedures [Visual Basic], about procedures
ms.assetid: 4f779247-0b50-47e8-9e5c-ab5cf39ac0d2
ms.openlocfilehash: a831814c18f97991fca8067f1c9c8e491da1b665
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74344907"
---
# <a name="how-to-create-a-procedure-visual-basic"></a>方法: プロシージャを作成する (Visual Basic)

プロシージャは、開始宣言ステートメント (`Sub` または `Function`) と終了宣言ステートメント (`End Sub` または `End Function`) で囲みます。 プロシージャのコードはすべて、これらのステートメントの間にあります。

 あるプロシージャに別のプロシージャを含めることはできないため、その開始と終了のステートメントは他のプロシージャの外部にある必要があります。

 異なる場所で同じタスクを実行するコードがある場合は、そのタスクをプロシージャとして一度記述してから、コード内の異なる場所から呼び出すことができます。

### <a name="to-create-a-procedure-that-does-not-return-a-value"></a>値を返さないプロシージャを作成するには

1. 他のプロシージャの外部で、`Sub` ステートメントを使用し、その後に `End Sub` ステートメントを使用します。

2. `Sub` ステートメントで、`Sub` キーワードの後にプロシージャの名前を指定してから、かっこで囲んだパラメーター リストを指定します。

3. `Sub` および `End Sub` ステートメントの間に、プロシージャのコード ステートメントを配置します。

### <a name="to-create-a-procedure-that-returns-a-value"></a>値を返すプロシージャを作成するには

1. 他のプロシージャの外部で、`Function` ステートメントを使用し、その後に `End Function` ステートメントを使用します。

2. `Function` ステートメントで、`Function` キーワードの後にプロシージャの名前を指定します。次に、かっこで囲んだパラメーター リストを指定し、戻り値のデータ型を指定する `As` 句を使用します。

3. `Function` および `End Function` ステートメントの間に、プロシージャのコード ステートメントを配置します。

4. `Return` ステートメントを使用して、呼び出し元のコードに値を返します。

### <a name="to-connect-your-new-procedure-with-the-old-repetitive-blocks-of-code"></a>新しいプロシージャを古い繰り返しコード ブロックに接続するには

1. 古いコードでアクセスできる場所に新しいプロシージャを定義していることを確認します。

2. 古い繰り返しコード ブロックで、繰り返しタスクを実行するステートメントを、`Sub` または `Function` プロシージャを呼び出す単一のステートメントに置き換えます。

3. プロシージャが、値を返す `Function` である場合は、呼び出し元のステートメントで確実に戻り値を持つアクション (変数に格納するなど) を実行するようにしてください。そうしないと、値が失われます。

## <a name="example"></a>例

 次の `Function` プロシージャでは、他の 2 つの辺の値を指定して、直角三角形の最も長い辺 (斜辺) を計算します。

 [!code-vb[VbVbcnProcedures#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#1)]

## <a name="see-also"></a>関連項目

- [手順](index.md)
- [Sub プロシージャ](sub-procedures.md)
- [Function プロシージャ](function-procedures.md)
- [Property プロシージャ](property-procedures.md)
- [演算子プロシージャ](operator-procedures.md)
- [プロシージャのパラメーターと引数](procedure-parameters-and-arguments.md)
- [再帰プロシージャ](recursive-procedures.md)
- [プロシージャのオーバーロード](procedure-overloading.md)
- [クラスとオブジェクト](../objects-and-classes/index.md)
- [オブジェクト指向プログラミング (Visual Basic)](../../concepts/object-oriented-programming.md)
