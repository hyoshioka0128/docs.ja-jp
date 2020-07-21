---
title: Assembly
ms.date: 07/20/2015
f1_keywords:
- vb.Assembly
- vb.AssemblyAttribute
- Assembly
helpviewer_keywords:
- Assembly modifier
- Assembly keyword [Visual Basic]
- attribute blocks, Assembly keyword
ms.assetid: 925e7471-3bdf-4b51-bb93-cbcfc6efc52f
ms.openlocfilehash: 7d313dee1015362bd0215ed98ab7e898312cfbcd
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84373161"
---
# <a name="assembly-visual-basic"></a>Assembly (Visual Basic)
ソース ファイルの先頭の属性がアセンブリ全体に適用されることを指定します。  
  
## <a name="remarks"></a>Remarks  
 個々のプログラミング要素には、クラスやプロパティなどの多くの属性が関連しています。 そのような属性を適用するには、山かっこ (`< >`) 内の属性ブロックを宣言ステートメントに直接アタッチします。  
  
 属性が次の要素だけでなく、アセンブリ全体に関連する場合は、属性ブロックをソース ファイルの先頭に配置し、`Assembly` キーワードで属性を識別します。 それを現在のアセンブリ モジュールに適用する場合、[Module](module-keyword.md) キーワードを使用します。  
  
 また、AssemblyInfo.vb ファイル内のアセンブリに属性を適用することもできます。この場合、メイン ソースコード ファイルで属性ブロックを使用する必要はありません。  
  
## <a name="see-also"></a>関連項目

- [Module \<keyword>](module-keyword.md)
- [属性の概要](../../programming-guide/concepts/attributes/index.md)
