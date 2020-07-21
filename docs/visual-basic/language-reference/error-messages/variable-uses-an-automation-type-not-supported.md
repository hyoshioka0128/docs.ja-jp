---
title: サポートされていない Automation の型が変数で使用されています
ms.date: 07/20/2015
f1_keywords:
- vbrID458
ms.assetid: bde4f4da-493b-452c-b6e4-1d370edba4cd
ms.openlocfilehash: 7d52189e31823b63547c757434847c0e1717aada
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406548"
---
# <a name="variable-uses-an-automation-type-not-supported-in-visual-basic"></a>Visual Basic でサポートされていないオートメーションが変数で使用されています。

Visual Basic でサポートされていないデータ型を持つタイプ ライブラリまたはオブジェクト ライブラリに定義された変数を使用しようとしました。

## <a name="to-correct-this-error"></a>このエラーを解決するには

- Visual Basic によって認識される型の変数を使用します。

     \- または -

- `FileGet` または `FileGetObject` の使用中にこのエラーが発生した場合は、使用しようとしているファイルが `FilePut` または `FilePutObject` と共に書き込まれていることを確認してください。

## <a name="see-also"></a>関連項目

- [データの種類](../data-types/index.md)
