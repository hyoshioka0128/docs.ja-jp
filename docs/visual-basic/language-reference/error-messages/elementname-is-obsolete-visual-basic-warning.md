---
title: "'<elementname>' は古い形式です (Visual Basic 警告)"
ms.date: 07/20/2015
f1_keywords:
- vbc40008
- bc40008
helpviewer_keywords:
- BC40008
ms.assetid: 729e3eb5-76ac-4c55-9fdd-78350e0de55e
ms.openlocfilehash: 7914bc859966e17f3da41c9a13a01573b31baf91
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409674"
---
# <a name="elementname-is-obsolete-visual-basic-warning"></a>'\<elementname>' は古い形式です (Visual Basic 警告)
<xref:System.ObsoleteAttribute> 属性でマークされているプログラミング要素にステートメントがアクセスを試行しています。この試行をディレクティブは警告として処理します。  
  
 <xref:System.ObsoleteAttribute> を適用することで、任意のプログラミング要素を使用しない要素としてマークできます。 これを行う場合、この属性の <xref:System.ObsoleteAttribute.IsError%2A> プロパティを `True` または `False`のどちらかに設定できます。 `True`に設定した場合、この要素を使用しようとすると、コンパイラはエラーとして処理します。 `False`に設定した場合、または既定値の `False`を使用した場合、コンパイラはこの要素の使用が試行されると、警告を発行します。  
  
 既定では、 <xref:System.ObsoleteAttribute.IsError%2A> の <xref:System.ObsoleteAttribute> プロパティが `False`であるため、このメッセージは警告になります。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」をご覧ください。  
  
 **エラー ID:** BC40008  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- ソース コード参照の要素名のスペルが正しいことを確認します。  
  
## <a name="see-also"></a>関連項目

- [属性の概要](../../programming-guide/concepts/attributes/index.md)
