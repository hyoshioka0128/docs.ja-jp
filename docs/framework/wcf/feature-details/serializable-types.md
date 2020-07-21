---
title: シリアル化可能な型
ms.date: 03/30/2017
ms.assetid: f1c8539a-6a79-4413-b294-896f0957b2cd
ms.openlocfilehash: e65fcb93c5c36bb289b825cef58b3adc6f5155f5
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84586105"
---
# <a name="serializable-types"></a>シリアル化可能な型
既定では、<xref:System.Runtime.Serialization.DataContractSerializer> は公開されている型をすべてシリアル化します。 その型の読み書き可能なパブリック プロパティおよびパブリック フィールドは、すべてシリアル化されます。  
  
 既定の動作を変更するには、<xref:System.Runtime.Serialization.DataContractAttribute> 属性と <xref:System.Runtime.Serialization.DataMemberAttribute> 属性を型とメンバーに適用します。この機能は、使用するコントロールに型がない場合や属性を追加するように変更できない場合に役立ちます。 <xref:System.Runtime.Serialization.DataContractSerializer> は "マークされていない" 型を認識します。  
  
## <a name="serialization-defaults"></a>シリアル化の既定  
 <xref:System.Runtime.Serialization.DataContractAttribute> 属性と <xref:System.Runtime.Serialization.DataMemberAttribute> 属性を適用して、型とメンバーのシリアル化を明示的に制御またはカスタマイズできます。 さらに、これらの属性をプライベート フィールドに適用することもできます。 ただし、これらの属性でマークされていない型もシリアル化および逆シリアル化されます。 次のルールと例外が適用されます。  
  
- <xref:System.Runtime.Serialization.DataContractSerializer> は、新しく作成した型の既定のプロパティを使用して、属性のない型からデータ コントラクトを推論します。  
  
- すべてのパブリック フィールドと、パブリック `get` メソッドおよび `set` メソッドを持つプロパティは、<xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> 属性をそのメンバーに適用しない限りシリアル化されます。  
  
- シリアル化のセマンティクスは <xref:System.Xml.Serialization.XmlSerializer> に似ています。  
  
- マークされていない型では、パラメーターのないコンストラクターを持つパブリック型のみがシリアル化されます。 このルールの例外として、<xref:System.Runtime.Serialization.ExtensionDataObject> インターフェイスとして使用される <xref:System.Runtime.Serialization.IExtensibleDataObject> があります。  
  
- 読み取り専用フィールド、`get` メソッドまたは `set` メソッドのないプロパティ、内部またはプライベート `set` メソッドまたは `get` メソッドのあるプロパティはシリアル化されません。 そのようなプロパティは無視され、例外はスローされません。ただし、取得専用のコレクションの場合は除きます。  
  
- <xref:System.Xml.Serialization.XmlSerializer> 属性 (`XmlElement`、`XmlAttribute`、`XmlIgnore`、`XmlInclude` など) は無視されます。  
  
- <xref:System.Runtime.Serialization.DataContractAttribute> 属性を指定の型に適用しない場合は、シリアライザーは <xref:System.Runtime.Serialization.DataMemberAttribute> 属性が適用されるその型のすべてのメンバーを無視します。  
  
- <xref:System.Runtime.Serialization.DataContractSerializer.KnownTypes%2A> プロパティは <xref:System.Runtime.Serialization.DataContractAttribute> 属性でマークされていない型でサポートされます。 これには、マークされていない型での <xref:System.Runtime.Serialization.KnownTypeAttribute> 属性のサポートも含まれます。  
  
- パブリック メンバー、プロパティ、またはフィールドのシリアル化のプロセスを "取り消す" には、<xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> 属性をそのメンバーに適用します。  
  
## <a name="inheritance"></a>継承  
 マークされていない型 (<xref:System.Runtime.Serialization.DataContractAttribute> 属性のない型) は、この属性を持つ型から継承できます。ただし、その反対はできません。つまり、マークされていない型から属性を持つ型を継承することはできません。 このルールは、以前のバージョンの .NET Framework で記述されたコードとの下位互換性を確保するために主に適用されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- <xref:System.Xml.Serialization.XmlSerializer>
- [データ コントラクト シリアライザーでサポートされる型](types-supported-by-the-data-contract-serializer.md)
