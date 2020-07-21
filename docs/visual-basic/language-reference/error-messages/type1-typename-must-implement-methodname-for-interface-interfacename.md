---
title: <type1>'<typename>' は、インターフェイス '<interfacename>' に対して '<methodname>' を実装しなければなりません。
ms.date: 07/20/2015
f1_keywords:
- vbc30149
- bc30149
helpviewer_keywords:
- BC30149
ms.assetid: 29d1b7f4-dca7-478c-bbe7-c657f342c183
ms.openlocfilehash: 90d2b6d70390bfb732af4a5868c935de61d18f94
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408499"
---
# <a name="type1typename-must-implement-methodname-for-interface-interfacename"></a>\<type1>'\<typename>' は、インターフェイス '\<interfacename>' に対して '\<methodname>' を実装しなければなりません。
クラスまたは構造体では、インターフェイスを実装することが要求されますが、インターフェイスによって定義されるプロシージャは実装しません。 インターフェイスのすべてのメンバーを実装する必要があります。  
  
 **エラー ID:** BC30149  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. インターフェイスで定義されているものと同じ名前およびシグネチャを持つプロシージャを宣言します。 少なくとも `End Function` または `End Sub` ステートメントを含めてください。  
  
2. `Function` または `Sub` ステートメントの末尾に `Implements` 句を追加します。 次に例を示します。  
  
    ```vb  
    Public Sub DoSomething() Implements IBaseInterface.DoSomething  
    ```  
  
## <a name="see-also"></a>関連項目

- [Implements ステートメント](../statements/implements-statement.md)
- [インターフェイス](../../programming-guide/language-features/interfaces/index.md)
