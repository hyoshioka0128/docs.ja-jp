---
title: 範囲変数 <variable> により、それを囲むブロック内の変数、以前に定義された範囲変数、またはクエリ式内で暗黙的に宣言された変数が非表示になります
ms.date: 07/20/2015
f1_keywords:
- bc36633
- vbc36633
helpviewer_keywords:
- BC36633
ms.assetid: 5d5470e4-3de5-49c2-8831-1087625f4a77
ms.openlocfilehash: 290ca81dea500558ed73956c91bdf7bfec312014
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400397"
---
# <a name="range-variable-variable-hides-a-variable-in-an-enclosing-block-a-previously-defined-range-variable-or-an-implicitly-declared-variable-in-a-query-expression"></a>範囲変数 \<variable> により、それを囲むブロック内の変数、以前に定義された範囲変数、またはクエリ式内で暗黙的に宣言された変数が非表示になります
`Select`、`From`、`Aggregate`、または `Let` 句で指定された範囲変数名が、クエリで既に指定されている範囲変数の名前、またはクエリによって暗黙的に宣言された変数の名前 (フィールド名や集計関数の名前など) と重複しています。  
  
 **エラー ID:** BC36633  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- 特定のクエリ スコープ内のすべての範囲変数の名前が一意であることを確認します。 入れ子になったクエリのスコープが一意になるように、クエリをかっこで囲むことができます。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic における LINQ の概要](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [From 句](../queries/from-clause.md)
- [Let 句](../queries/let-clause.md)
- [Aggregate 句](../queries/aggregate-clause.md)
- [Select 句](../queries/select-clause.md)
