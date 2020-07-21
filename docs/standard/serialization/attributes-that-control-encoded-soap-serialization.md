---
title: エンコード済み SOAP シリアル化を制御する属性
description: この記事では、SOAP 仕様に準拠するために必要な System.Xml.Serialization 名前空間で指定されている特殊な属性のセットの一覧を示します。
ms.date: 03/30/2017
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- XML serialization, attributes
- attributes [.NET Framework], XML serialization
- serialization, attributes
ms.assetid: 93ee258c-9c0f-4a08-897c-c10db7a00f91
ms.openlocfilehash: d9a4631189d348c02ab36054257a54c9c4673018
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84289669"
---
# <a name="attributes-that-control-encoded-soap-serialization"></a>エンコード済み SOAP シリアル化を制御する属性

World Wide Web コンソーシアム (W3C) のドキュメント『[Simple Object Access Protocol (SOAP) 1.1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/)』には、SOAP パラメーターのエンコード方法について説明したオプションのセクション (セクション 5) が含まれています。 このセクション 5 の仕様に準拠するには、<xref:System.Xml.Serialization> 名前空間で指定されている特殊な属性セットを使用する必要があります。 これらの属性をクラスやクラスのメンバーに適宜適用し、<xref:System.Xml.Serialization.XmlSerializer> を使用して、クラスのインスタンスをシリアル化します。

これらの属性、およびその適用対象と機能を次の表に示します。 これらの属性を使用して XML シリアル化を制御する方法の詳細については、「[方法: オブジェクトを SOAP エンコード済み XML ストリームとしてシリアル化する](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)」と「[方法: SOAP エンコード済み XML シリアル化をオーバーライドする](how-to-override-encoded-soap-xml-serialization.md)」を参照してください。

属性の詳細については、「[属性](../attributes/index.md)」を参照してください。

|属性|対象|指定内容|
|---------------|----------------|---------------|
|<xref:System.Xml.Serialization.SoapAttributeAttribute>|パブリック フィールド、パブリック プロパティ、パブリック パラメーター、または戻り値|クラス メンバーを XML 属性としてシリアル化します。|
|<xref:System.Xml.Serialization.SoapElementAttribute>|パブリック フィールド、パブリック プロパティ、パブリック パラメーター、または戻り値|クラスを XML 要素としてシリアル化します。|
|<xref:System.Xml.Serialization.SoapEnumAttribute>|列挙体識別子であるパブリック フィールド|列挙体のメンバーの要素名を指定します。|
|<xref:System.Xml.Serialization.SoapIgnoreAttribute>|パブリック プロパティとパブリック フィールド|クラスのシリアル化時に、そのクラスに含まれているプロパティまたはフィールドを無視します。|
|<xref:System.Xml.Serialization.SoapIncludeAttribute>|パブリック派生クラス宣言、およびパブリック メソッド (Web サービス記述言語 (WSDL: Web Service Description Language) ドキュメント用)|シリアル化時に認識されるように、スキーマの生成時にその型を対象に含めます。|
|<xref:System.Xml.Serialization.SoapTypeAttribute>|パブリック クラス宣言|クラスを XML 型としてシリアル化します。|

## <a name="see-also"></a>関連項目

- [XML シリアル化および SOAP シリアル化](xml-and-soap-serialization.md)
- [方法: オブジェクトを SOAP エンコード済み XML ストリームとしてシリアル化する](how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)
- [方法: SOAP エンコード済み XML シリアル化をオーバーライドする](how-to-override-encoded-soap-xml-serialization.md)
- [属性](../attributes/index.md)
- <xref:System.Xml.Serialization.XmlSerializer>
- [方法: オブジェクトをシリアル化する](how-to-serialize-an-object.md)
- [方法: オブジェクトを逆シリアル化する](how-to-deserialize-an-object.md)
