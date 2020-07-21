---
title: 定数の概要
ms.date: 07/20/2015
helpviewer_keywords:
- constants [Visual Basic]
ms.assetid: 29016fe8-78b3-4dc8-90b8-1cfec2fa8ac9
ms.openlocfilehash: f45cb12c6ef0f90b9c90190f30ce8600fec80947
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414519"
---
# <a name="constants-overview-visual-basic"></a>定数の概要 (Visual Basic)
定数とは、不変の数値または文字列の代わりとなるわかりやすい名前です。 定数に格納された値は、その名が示すとおり、アプリケーションの実行中に変わることはありません。 定数を使用することで、コードの可読性を大きく高め、管理を容易にすることができます。 これらは、繰り返し現れる値を含むコードや、覚えにくい数値または意味のわかりにくい数値に依存するコードで使用します。  
  
## <a name="how-to-create-and-use-constants"></a>定数の作成方法と使用方法  
 Visual には定義済みの定数が多数含まれており、その大部分は印刷や表示に使用されています。 変数名を作成するときと同じガイドラインに従い、`Const` ステートメントによって独自の定数を作成することもできます。 `Option Strict` に `On` を指定した場合、定数の型を明示的に宣言する必要があります。  
  
 定数のスコープは、定数の名前を修飾しなくても参照可能なすべてのコードであり、同一の場所で宣言された変数のものと同じになります。 特定のプロシージャのスコープ内に存在する定数を作成するには、該当するプロシージャ内で宣言します。 アプリケーション全体で利用可能な定数を作成するには、クラスの宣言セクションで `Public` キーワードを使用して宣言します。  
  
> [!NOTE]
> 定数は変数にやや似ていますが、定数を変更したり、変数のように新しい値を割り当てたりすることはできません。  
  
 コードで使用する定数は、利用するコントロールまたはコンポーネントのオブジェクト モデルにより定義できます。また、ユーザー定義定数 (つまり、独自に作成した定数) を使用することもできます。  
  
## <a name="compile-time-and-run-time-constants"></a>コンパイル時定数と実行時定数  
 コンパイル時定数はコードのコンパイル時に計算されますが、実行時定数はアプリケーションの実行中にしか計算できません。 コンパイル時定数には、アプリケーションを実行するたびに同じ値が割り当てられますが、実行時定数は実行のたびに変わる可能性があります。 配列の範囲、Case 式、列挙子の初期化子などにはコンパイル時定数を使用する必要があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|定義|用語|  
|---|---|  
|[方法: 定数を宣言する](how-to-declare-a-constant.md)|`Const` ステートメントを使用して定数とその値を宣言する方法について説明します。定数を宣言することで、値にわかりやすい名前を付けることができます。|  
|[ユーザー定義定数](user-defined-constants.md)|独自の定数の作成方法について、スコープの設定や循環参照の回避方法なども含めて説明します。|  
|[定数とリテラルのデータ型](constant-and-literal-data-types.md)|`Option Explicit` が Off の場合に Visual Basic コンパイラが定数を初期化するしくみについて説明します。|  
|[方法: 関連する定数値をまとめてグループ化する](how-to-group-related-constant-values-together.md)|関連する定数の値をグループ化する方法について説明します。|  
  
## <a name="reference"></a>関連項目  
  
|定義|用語|  
|---|---|  
|[定数と列挙体](../../../language-reference/constants-and-enumerations.md)|Visual Basic の事前定義定数の一覧を紹介します。|  
|[Const ステートメント](../../../language-reference/statements/const-statement.md)|`Const` ステートメントとその使用法について説明します。|  
|[Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)|`Option Strict` ステートメントとその使用法について説明します。|  
  
## <a name="see-also"></a>関連項目

- [列挙型の概要](enumerations-overview.md)
- [方法: Visual Basic で配列変数を初期化する](../arrays/how-to-initialize-an-array-variable.md)
