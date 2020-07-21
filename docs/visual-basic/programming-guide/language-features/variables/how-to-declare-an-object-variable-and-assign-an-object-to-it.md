---
title: '方法: Visual Basic でオブジェクト変数を宣言し、オブジェクト変数にオブジェクトを代入する'
ms.date: 07/20/2015
helpviewer_keywords:
- object variables [Visual Basic], declaring
- declaring object variables [Visual Basic]
ms.assetid: 2fa77dde-1fb2-439a-80d4-3e9787649fad
ms.openlocfilehash: d9a8c1fb30bfa5988d48202e41202e7ede0f5f27
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410504"
---
# <a name="how-to-declare-an-object-variable-and-assign-an-object-to-it-in-visual-basic"></a>方法: Visual Basic でオブジェクト変数を宣言してオブジェクトを代入する

[Object データ型](../../../language-reference/data-types/object-data-type.md)の変数は、[Dim ステートメント](../../../language-reference/statements/dim-statement.md)で `As Object` を指定して宣言します。 このような変数にオブジェクトを代入するには、代入ステートメントまたは初期化句で等号 (`=`) の後にオブジェクトを配置します。

## <a name="example"></a>例

次の例では、`Object` 変数を宣言して、現在のインスタンスをこれに代入します。

```vb
Dim thisObject As Object
thisObject = "This is an Object"
```

宣言に変数の初期化を含めると、宣言と代入を同時に行うことができます。 次の例は、前の例と同じです。

```vb
Dim thisObject As Object= "This is an Object"
```

## <a name="compile-the-code"></a>コードのコンパイル

この例で必要な要素は次のとおりです。

- <xref:System> 名前空間への参照

- `Dim` ステートメントを入れるクラス、構造体、またはモジュール。

- 代入ステートメントを入れるプロシージャ。

## <a name="see-also"></a>関連項目

- [変数宣言](variable-declaration.md)
- [オブジェクト変数](object-variables.md)
- [オブジェクト変数の宣言](object-variable-declaration.md)
- [Object 型](../../../language-reference/data-types/object-data-type.md)
- [Dim ステートメント](../../../language-reference/statements/dim-statement.md)
- [ローカル型の推論](local-type-inference.md)
- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
