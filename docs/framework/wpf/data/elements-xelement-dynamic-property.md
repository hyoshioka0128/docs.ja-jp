---
title: Elements (XElement 動的プロパティ)
ms.date: 10/22/2019
ms.topic: reference
apiname:
- XElement.Elements
apitype: Assembly
ms.openlocfilehash: 812adabd3bfb01fd9313ce3f35e6cb0a5e23344e
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72921150"
---
# <a name="elements-xelement-dynamic-property"></a>Elements (XElement 動的プロパティ)

現在の要素の子要素のうち指定された拡張名に一致する子要素の取得に使用するインデクサーを取得します。

## <a name="syntax"></a>構文

```xaml
elem.Elements[{namespaceName}localName]
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値

`IEnumerable<XElement> Item(String expandedName)` 型のインデクサー。 このインデクサーは、目的の子要素の拡張名を取得し、<xref:System.Collections.IEnumerable>`<`<xref:System.Xml.Linq.XElement>`>` コレクション内の一致する子要素を返します。

## <a name="remarks"></a>Remarks

このプロパティは、<xref:System.Xml.Linq.XContainer.Elements(System.Xml.Linq.XName)?displayProperty=fullName> クラスの <xref:System.Xml.Linq.XContainer> メソッドに相当します。

返されるコレクション内の要素は、XML ソース ドキュメント順になります。

このプロパティは、遅延実行を使用します。

## <a name="see-also"></a>関連項目

- [XElement クラスの動的プロパティ](attribute-xelement-dynamic-property.md)
- [要素](element-xelement-dynamic-property.md)
- [子孫](descendants-xelement-dynamic-property.md)
