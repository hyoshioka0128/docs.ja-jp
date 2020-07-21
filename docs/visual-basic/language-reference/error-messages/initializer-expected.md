---
title: 初期化子が必要です
ms.date: 07/20/2015
f1_keywords:
- vbc30996
- bc30996
helpviewer_keywords:
- BC30996
ms.assetid: 6e183fe0-8888-43ed-a062-01571079455f
ms.openlocfilehash: 13fa8917f228661fc44f5e0920d91c596e250c38
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84402838"
---
# <a name="initializer-expected"></a>初期化子が必要です
次の例に示すように、初期化リストが空のオブジェクト初期化子を使用して、クラスのインスタンスを宣言しようとしました。  
  
 `' Not valid.`  
  
 `' Dim aStudent As New Student With {}`  
  
 次の例に示すように、初期化子リストの少なくとも 1 つのフィールドまたはプロパティを初期化する必要があります。  
  
 `Dim aStudent As New Student With {.year = "Senior"}`  
  
 **エラー ID:** BC30996  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. 初期化子の少なくとも 1 つのフィールドまたはプロパティを初期化するか、オブジェクト初期化子を使用しないようにしてください。  
  
## <a name="see-also"></a>関連項目

- [オブジェクト初期化子: 名前付きの型と匿名型](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [方法: オブジェクト初期化子を使用してオブジェクトを宣言する](../../programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
