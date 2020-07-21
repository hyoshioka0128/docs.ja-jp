---
title: 名前 <membername> は CLS に準拠していません。
ms.date: 07/20/2015
f1_keywords:
- bc40031
- vbc40031
helpviewer_keywords:
- BC40031
ms.assetid: e2b885dc-cbf9-49ff-bbbe-531657ea99f7
ms.openlocfilehash: 45c9332237dffc7311daeedaf36035d9e9958415
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397182"
---
# <a name="name-membername-is-not-cls-compliant"></a>名前 \<membername> は CLS に準拠していません。
アセンブリが `<CLSCompliant(True)>` としてマークされているのに、アンダースコア (`_`) で始まる名前のメンバーを公開しています。  
  
 プログラミング要素には 1 つ以上のアンダースコアを含めることができますが、[言語への非依存性、および言語非依存コンポーネント](../../../standard/language-independence-and-language-independent-components.md) (CLS) に準拠するためには、先頭をアンダースコアにしてはなりません。 「 [Declared Element Names](../../programming-guide/language-features/declared-elements/declared-element-names.md)」を参照してください。  
  
 プログラミング要素に <xref:System.CLSCompliantAttribute> を適用する場合は、属性の `isCompliant` パラメーターを `True` または `False` のどちらかに設定して、準拠または非準拠を示します。 このパラメーターには既定値がありません。値を指定する必要があります。  
  
 要素に <xref:System.CLSCompliantAttribute> を適用しないと、その要素は非準拠と見なされます。  
  
 既定では、このメッセージは警告です。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」をご覧ください。  
  
 **エラー ID:** BC40031  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- ソース コードを制御できる場合は、アンダースコアで始まらないようにメンバー名を変更します。  
  
- メンバーの名前が変更されないようにする必要がある場合は、その定義から <xref:System.CLSCompliantAttribute> を削除するか、`<CLSCompliant(False)>` としてマークします。 アセンブリを `<CLSCompliant(True)>` としてマークすることもできます。  
  
## <a name="see-also"></a>関連項目

- [宣言された要素の名前](../../programming-guide/language-features/declared-elements/declared-element-names.md)
- [Visual Basic の名前付け規則](../../programming-guide/program-structure/naming-conventions.md)
