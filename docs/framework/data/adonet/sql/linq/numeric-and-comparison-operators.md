---
title: 数値演算子および比較演算子
ms.date: 03/30/2017
ms.assetid: 25b4a26a-06f2-4f80-87a9-76705ed46197
ms.openlocfilehash: 7e7af725864aa191f092055fa32b403093321aa5
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781286"
---
# <a name="numeric-and-comparison-operators"></a>数値演算子および比較演算子

算術演算子と比較演算子は、次の点を除いて、共通言語ランタイム (CLR) では期待どおりに動作します。

- SQL では、浮動小数点数に対して剰余演算子がサポートされません。

- SQL ではチェックされない算術はサポートされません。

- インクリメント演算子とデクリメント演算子は、SQL に複製できない式で使用すると副作用があるため、SQL ではサポートされません。

## <a name="supported-operators"></a>サポートされる演算子

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、次の演算子をサポートしています。

- 基本算術演算子

  - `+`

  - `-` (減算)

  - `*`

  - `/`

  - Visual Basic 整数除算 (`\`)

  - `%` (Visual Basic `Mod`)

  - `<<`

  - `>>`

  - `-` (単項マイナス符号)

- 基本比較演算子

  - Visual Basic `=` および C# `==`

  - Visual Basic `<>` および C# `!=`

  - Visual Basic `Is/IsNot`

  - `<`

  - `<=`

  - `>`

  - `>=`

## <a name="see-also"></a>関連項目

- [データ型と関数](data-types-and-functions.md)
- [C# 演算子](../../../../../csharp/language-reference/operators/index.md)
- [演算子](../../../../../visual-basic/language-reference/operators/index.md)
