---
title: Element (XElement 動的プロパティ)
ms.date: 10/22/2019
ms.topic: reference
apiname:
- XElement.Element
apitype: Assembly
ms.openlocfilehash: fc0277d0dc38574696f01e6915e5382744345771
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72921186"
---
# <a name="element-xelement-dynamic-property"></a>Element (XElement 動的プロパティ)

指定された展開名に対応する子要素のインスタンスを取得するためのインデクサーを取得します。

## <a name="syntax"></a>構文

```xaml
elem.Element[{namespaceName}localName]
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値

`XElement Item(String expandedName)` 型のインデクサー。 このインデクサーは、展開名のパラメーターを取得し、対応する <xref:System.Xml.Linq.XElement> を返します。指定された名前を持つ要素がない場合は、`null` を返します。

## <a name="remarks"></a>Remarks

このプロパティは、<xref:System.Xml.Linq.XContainer.Element%2A> クラスの <xref:System.Xml.Linq.XContainer?displayProperty=fullName> メソッドに相当します。

## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XContainer.Element%2A?displayProperty=fullName>
- [XElement クラスの動的プロパティ](attribute-xelement-dynamic-property.md)
- [要素](elements-xelement-dynamic-property.md)
