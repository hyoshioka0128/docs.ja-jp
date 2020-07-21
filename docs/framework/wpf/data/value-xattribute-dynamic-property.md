---
title: Value (XAttribute 動的プロパティ)
ms.date: 10/22/2019
ms.topic: reference
apiname:
- XAttribute.Value
apitype: Assembly
ms.openlocfilehash: 32c15a89a976b5f9af12f040c43e724a25357ead
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72920976"
---
# <a name="value-xattribute-dynamic-property"></a>Value (XAttribute 動的プロパティ)

XML 属性の値を取得または設定します。

## <a name="syntax"></a>構文

```xaml
attrib.Value
```

## <a name="property-valuereturn-value"></a>プロパティ値/戻り値

この属性の値を表す <xref:System.String> です。

## <a name="exceptions"></a>例外

|例外の種類|条件|
| - |---------------|
|<xref:System.ArgumentNullException>|設定時に `value` が `null` である場合に発生します。|

## <a name="remarks"></a>Remarks

このプロパティは、<xref:System.Xml.Linq.XAttribute.Value%2A> クラスの <xref:System.Xml.Linq.XAttribute?displayProperty=fullName> プロパティに相当します。ただし、この動的プロパティは変更通知もサポートします。

## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XAttribute.Value%2A?displayProperty=fullName>
- [XAttribute クラスの動的プロパティ](value-xattribute-dynamic-property.md)
- [属性](attribute-xelement-dynamic-property.md)
