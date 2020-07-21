---
title: 有効期間
ms.date: 07/20/2015
helpviewer_keywords:
- static variables [Visual Basic], lifetime
- static variables [Visual Basic], Visual Basic
- declared elements [Visual Basic], lifetime
- Shared variable lifetime [Visual Basic]
- lifetime [Visual Basic], declared elements
- lifetime [Visual Basic], Visual Basic
- lifetime [Visual Basic]
ms.assetid: bd91e390-690a-469a-9946-8dca70bc14e7
ms.openlocfilehash: 377f0e0b5240c3da931dc4af5439aba8924f1e81
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84357142"
---
# <a name="lifetime-in-visual-basic"></a>Visual Basic における有効期間
宣言された要素の *有効期間*は、それを使用できる期間です。 変数は、有効期間がある唯一の要素です。 このため、コンパイラでは、プロシージャのパラメーターと関数の戻り値が変数の特殊なケースとして扱われます。 変数の有効期間は、それが値を保持できる期間を表します。 その値は有効期間を通じて変更される可能性がありますが、常に何らかの値が保持されます。  
  
## <a name="different-lifetimes"></a>さまざまな有効期間  
 *メンバー変数* (モジュールレベルで、プロシージャの外部で宣言) には、通常、それが宣言されている要素と同じ有効期間があります。 クラスまたは構造体に宣言された非共有変数は、それが宣言されているクラスまたは構造体のインスタンスごとに個別のコピーとして存在します。 各変数には、そのインスタンスと同じ有効期間があります。 ただし、`Shared` 変数の有効期間は 1 つだけであり、アプリケーションが実行中の間ずっと存続します。  
  
 *ローカル変数* (プロシージャ内で宣言) は、それが宣言されているプロシージャが実行されている間のみ存在します。 これは、そのプロシージャのパラメーターと関数の戻り値にも適用されます。 ただし、そのプロシージャで、他のプロシージャを呼び出している場合、呼び出されたプロシージャが実行されている間、ローカル変数の値が保持されます。  
  
## <a name="beginning-of-lifetime"></a>有効期間の開始  
 ローカル変数の有効期間は、それが宣言されているプロシージャの制御が始まったときに開始されます。 すべてのローカル変数は、プロシージャの実行が開始されるとすぐに、そのデータ型の既定値に初期化されます。 プロシージャで、初期値を指定した `Dim` ステートメントが検出されると、コードで他の値を既に代入していた場合でも、それらの変数にそれらの値が設定されます。  
  
 構造体変数の各メンバーは、個別の変数であるかのように初期化されます。 同様に、配列変数の各要素は個別に初期化されます。  
  
 プロシージャ内のブロック内で宣言された変数 (`For` ループなど) は、プロシージャに入ったときに初期化されます。 これらの初期化は、コードでブロックが実行されたかどうかにかかわらず有効になります。  
  
## <a name="end-of-lifetime"></a>有効期間の終了  
 プロシージャが終了すると、そのローカル変数の値は保持されず、Visual Basic によってそれらのメモリが解放されます。 次回にプロシージャを呼び出すと、そのすべてのローカル変数が新しく作成され、再初期化されます。  
  
 クラスまたは構造体のインスタンスが終了すると、その非共有変数では、それらのメモリと値が失われます。 クラスまたは構造体の新しい各インスタンスで、その非共有変数が作成され、再初期化されます。 ただし、`Shared` 変数は、アプリケーションが実行を停止するまで保持されます。  
  
## <a name="extension-of-lifetime"></a>有効期間の延長  
 `Static` キーワードでローカル変数を宣言する場合、その有効期間は、そのプロシージャの実行時間よりも長くなります。 次の表は、プロシージャの宣言によって、`Static` 変数が存在する期間がどのように決まるかを示しています。  
  
|プロシージャの場所と共有|静的変数の有効期間の開始|静的変数の有効期間の終了|  
|------------------------------------|-------------------------------------|-----------------------------------|  
|モジュール内 (既定で共有される)|プロシージャが初めて呼び出されたとき|アプリケーションの実行が停止したとき|  
|クラス内、`Shared` (プロシージャはインスタンス メンバーではない)|特定のインスタンスか、またはクラスや構造体名自体で、プロシージャが初めて呼び出されたとき|アプリケーションの実行が停止したとき|  
|クラスのインスタンス内、`Shared` ではない (プロシージャはインスタンス メンバーである)|特定のインスタンスでプロシージャが初めて呼び出されたとき|ガベージ コレクション (GC) のためにインスタンスが解放されたとき|  
  
## <a name="static-variables-of-the-same-name"></a>同じ名前の静的変数  
 複数のプロシージャで、同じ名前の静的変数を宣言できます。 この場合、Visual Basic コンパイラでは、このような各変数が個別の要素と見なされます。 これらの変数のいずれかを初期化しても、他の値には影響しません。 一連のオーバーロードでプロシージャを定義し、各オーバーロードで同じ名前の静的変数を宣言する場合も同じことが当てはまります。  
  
## <a name="containing-elements-for-static-variables"></a>静的変数の含んでいる要素  
 静的ローカル変数は、クラス内、つまりそのクラスのプロシージャ内で宣言できます。 ただし、静的ローカル変数は、構造体内で、構造体のメンバーとして、またはその構造内のプロシージャのローカル変数として宣言することはできません。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例では、[Static](../../../language-reference/modifiers/static.md) キーワードで変数を宣言しています。 ([Dim ステートメント](../../../language-reference/statements/dim-statement.md)で `Static` などの修飾子を使用している場合は、`Dim` キーワードが不要です。)  
  
### <a name="code"></a>コード  
 [!code-vb[VbVbalrKeywords#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrKeywords/VB/class7.vb#13)]  
  
### <a name="comments"></a>コメント  
 前の例では、プロシージャ `runningTotal` が呼び出し元のコードに戻った後も、変数 `applesSold` が存在し続けます。 次回に `runningTotal` が呼び出されたときに、`applesSold` には以前に計算された値が保持されます。  
  
 `Static` を使用せずに `applesSold` を宣言している場合、以前に累積された値は `runningTotal` の呼び出し間で保持されません。 次回に `runningTotal` が呼び出されたときに、`applesSold` が再作成されて、0 に初期化され、`runningTotal` では、単にそれが呼び出されたときと同じ値が返されます。  
  
### <a name="compile-the-code"></a>コードのコンパイル  
 静的ローカル変数の値は、その宣言の一部として初期化できます。 配列を `Static` として宣言する場合は、その順位 (次元の数)、各次元の長さ、および個々の要素の値を初期化できます。  
  
### <a name="security"></a>セキュリティ  
 前の例では、モジュール レベルで `applesSold` を宣言することで、同じ有効期間を生成できます。 ただし、このように変数のスコープを変更した場合、プロシージャでそれに排他的にアクセスしなくなります。 他のプロシージャによって `applesSold` にアクセスしてその値が変更される可能性があるため、累計は信頼できず、コードの保守が困難になることがあります。  
  
## <a name="see-also"></a>関連項目

- [Shared](../../../language-reference/modifiers/shared.md)
- [Nothing](../../../language-reference/nothing.md)
- [宣言された要素の名前](declared-element-names.md)
- [宣言された要素の参照](references-to-declared-elements.md)
- [Visual Basic におけるスコープ](scope.md)
- [Visual Basic でのアクセス レベル](access-levels.md)
- [変数](../variables/index.md)
- [変数宣言](../variables/variable-declaration.md)
- [トラブルシューティング (データ型)](../data-types/troubleshooting-data-types.md)
- [Static](../../../language-reference/modifiers/static.md)
