---
title: 既定プロパティ '<propertyname1>' は、'<propertyname2>' の既定プロパティ '<classname>' と競合しているため、'Shadows' と宣言できません。
ms.date: 07/20/2015
f1_keywords:
- vbc40007
- bc40007
helpviewer_keywords:
- BC40007
ms.assetid: 692ccf76-5715-4f11-a972-84cf9de30bc1
ms.openlocfilehash: 37f98ce8120d5861552819690f9d5f22c9959a0e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409726"
---
# <a name="default-property-propertyname1-conflicts-with-default-property-propertyname2-in-classname-and-so-should-be-declared-shadows"></a>既定プロパティ '\<propertyname1>' は、'\<propertyname2>' の既定プロパティ '\<classname>' と競合しているため、'Shadows' と宣言できません。
プロパティが、基底クラスで定義されたプロパティと同じ名前で宣言されています。 この場合、このクラスのプロパティは、基底クラス プロパティをシャドウする必要があります。  
  
 このメッセージは警告です。 `Shadows` は、既定で指定されていると見なされます。 警告を非表示にする方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」をご覧ください。  
  
 **エラー ID:** BC40007  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- `Shadows` キーワードを宣言に追加するか、宣言されるプロパティの名前を変更します。  
  
## <a name="see-also"></a>関連項目

- [Shadows](../modifiers/shadows.md)
- [Visual Basic におけるシャドウ](../../programming-guide/language-features/declared-elements/shadowing.md)
