---
title: "'<typename>' はデリゲート型です。"
ms.date: 07/20/2015
f1_keywords:
- bc32008
- vbc32008
helpviewer_keywords:
- BC32008
ms.assetid: dc6abba0-a9ad-450f-8899-87265bc84abc
ms.openlocfilehash: 7056bbf2b4de26feba3bfbe0e02b3239311271c9
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84382173"
---
# <a name="typename-is-a-delegate-type"></a>'\<typename>' はデリゲート型です。
'\<typename>' はデリゲート型です。 デリゲート コンストラクションでは、引数リストとして 1 つの AddressOf 式のみが許可されます。 多くの場合、デリゲート コンストラクションの代わりに AddressOf 式を使用できます。  
  
 デリゲート クラスのインスタンスを作成する `New` 句は、デリゲート コンストラクターに無効な引数リストを指定します。  
  
 新しいデリゲート インスタンスを作成するときは、1 つの `AddressOf` 式のみを指定できます。  
  
 このエラーは、デリゲート コンストラクターに引数を渡さない場合、複数の引数を渡した場合、または有効な `AddressOf` 式ではない 1 つの引数を渡した場合に発生する可能性があります。  
  
 **エラー ID:** BC32008  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `New` 句で、デリゲート クラスの引数リストに含まれる 1 つの `AddressOf` 式を使用します。  
  
## <a name="see-also"></a>関連項目

- [New 演算子](../operators/new-operator.md)
- [AddressOf 演算子](../operators/addressof-operator.md)
- [デリゲート](../../programming-guide/language-features/delegates/index.md)
- [方法: デリゲート メソッドを呼び出す](../../programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)
