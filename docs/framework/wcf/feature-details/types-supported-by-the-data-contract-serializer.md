---
title: データ コントラクト シリアライザーでサポートされる型
description: WCF データコントラクトシリアライザーがシリアル化と逆シリアル化のためにサポートする型の完全な一覧を参照してください。
ms.date: 03/30/2017
helpviewer_keywords:
- serialization [WCF], supported types
ms.assetid: 7381b200-437a-4506-9556-d77bf1bc3f34
ms.openlocfilehash: ef9d2e61ab7121c97bd474bb151fee32907b1dac
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246533"
---
# <a name="types-supported-by-the-data-contract-serializer"></a>データ コントラクト シリアライザーでサポートされる型

Windows Communication Foundation (WCF) は、を <xref:System.Runtime.Serialization.DataContractSerializer> 既定のシリアル化エンジンとして使用して、データを xml に変換し、xml をデータに変換します。 <xref:System.Runtime.Serialization.DataContractSerializer> は、 *データ コントラクト* 型をシリアル化するように設計されています。 ただし、暗黙のデータ コントラクトを持つと考えられるその他の型も多数サポートされています。 以下は、シリアル化可能なすべての型です。

- パラメーターを持たないコンストラクターを持つ公開されている型すべて

- データ コントラクト型。 <xref:System.Runtime.Serialization.DataContractAttribute> 属性が適用される型です。 ビジネス オブジェクトを表す新しいカスタム型は、通常、データ コントラクト型として作成されます。 詳細については、「[データコントラクト](using-data-contracts.md)と[シリアル化](serializable-types.md)可能な型の使用」を参照してください。

- コレクション型。 データのリストを表す型です。 型の通常の配列、または <xref:System.Collections.ArrayList> や <xref:System.Collections.Generic.Dictionary%602>などのコレクション型です。 <xref:System.Runtime.Serialization.CollectionDataContractAttribute> 属性を使用してこれらの型のシリアル化をカスタマイズすることもできますが、必須ではありません。 詳細については、「[データコントラクトのコレクション型](collection-types-in-data-contracts.md)」を参照してください。

- 列挙型。 フラグ列挙体などの列挙体はシリアル化できます。 列挙型は、必要に応じて、 <xref:System.Runtime.Serialization.DataContractAttribute> 属性でマークできます。その場合は、シリアル化に参加するすべてのメンバーを <xref:System.Runtime.Serialization.EnumMemberAttribute> 属性でマークする必要があります。 マークされていないメンバーはシリアル化されません。 詳細については、「[データコントラクトの列挙型](enumeration-types-in-data-contracts.md)」を参照してください。

- .NET Framework プリミティブ型。 .NET Framework に組み込まれている型 ( <xref:System.Byte>、 <xref:System.SByte>、 <xref:System.Int16>、 <xref:System.Int32>、 <xref:System.Int64>、 <xref:System.UInt16>、 <xref:System.UInt32>、 <xref:System.UInt64>、 <xref:System.Single>、 <xref:System.Double>、 <xref:System.Boolean>、 <xref:System.Char>、 <xref:System.Decimal>、 <xref:System.Object>、および <xref:System.String>) は、すべてシリアル化可能であり、プリミティブ型であると考えられます。

- その他のプリミティブ型。 これらの型は .NET Framework のプリミティブではないが、シリアル化された XML 形式ではプリミティブとして扱われます。 この型には、 <xref:System.DateTime>、 <xref:System.DateTimeOffset>、 <xref:System.TimeSpan>、 <xref:System.Guid>、 <xref:System.Uri>、 <xref:System.Xml.XmlQualifiedName>、および <xref:System.Byte>の配列が含まれます。

  > [!NOTE]
  > 他のプリミティブ型とは異なり、 <xref:System.DateTimeOffset> は既定では既知の型ではありません。 詳細については、「[データコントラクトの既知の型](data-contract-known-types.md)」を参照してください。

- <xref:System.SerializableAttribute> 属性でマークされた型。 .NET Framework 基本クラスライブラリに含まれる多くの型は、このカテゴリに分類されます。 <xref:System.Runtime.Serialization.DataContractSerializer> は、.NET Framework リモート処理、 <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>、および <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>で使用されていたこのシリアル化プログラミング モデルを完全にサポートします。これは、 <xref:System.Runtime.Serialization.ISerializable> インターフェイスのサポートを含みます。

- 生の XML を表す型、または ADO.NET リレーショナルデータを表す型。 <xref:System.Xml.XmlElement> 型および <xref:System.Xml.XmlNode> 型の配列は、XML を直接表す方法としてサポートされています。 また、 <xref:System.Xml.Serialization.IXmlSerializable> インターフェイスを実装する型 (関連する <xref:System.Xml.Serialization.XmlSchemaProviderAttribute> 属性、および <xref:System.Xml.Linq.XDocument> 型と <xref:System.Xml.Linq.XElement> 型を含む) もサポートされています。 ADO.NET <xref:System.Data.DataTable> 型と <xref:System.Data.DataSet> 型 (およびその型指定された派生クラス) はすべて <xref:System.Xml.Serialization.IXmlSerializable> インターフェイスを実装するため、このカテゴリに分類されます。 詳細については、「[データコントラクトの XML 型と ADO.NET 型](xml-and-ado-net-types-in-data-contracts.md)」を参照してください。

## <a name="limitations-of-using-certain-types-in-partial-trust-mode"></a>部分信頼モードにおける特定の型の使用制限

部分信頼モードのシナリオで型を使用する場合、型によっては次の制限があります。

- 部分信頼コードで <xref:System.Runtime.Serialization.ISerializable> を使用して <xref:System.Runtime.Serialization.DataContractSerializer> を実装する型のシリアル化または逆シリアル化を行うには、 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter%2A> アクセス許可および <xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A> アクセス許可が必要です。

- [部分信頼](partial-trust.md)モードで WCF コードを実行する場合、フィールド (との両方) のシリアル化と逆シリアル化 `readonly` はサポートされ `public` `private` ていません。 これは、生成された IL が検証不能であるため、より高いアクセス許可が必要になるためです。

- 部分信頼環境では、 <xref:System.Runtime.Serialization.DataContractSerializer> と <xref:System.Xml.Serialization.XmlSerializer> の両方がサポートされています。 ただし、 <xref:System.Runtime.Serialization.DataContractSerializer> の使用は、次の条件に従う必要があります。

  - シリアル化可能なすべての `[DataContract]` 型はパブリックである必要があります。

  - `[DataMember]` 型にあるシリアル化可能なすべての `[DataContract]` フィールドまたはプロパティは、パブリックで読み書き可能である必要があります。 `readonly`部分的に信頼されたアプリケーションで WCF を実行する場合、フィールドのシリアル化と逆シリアル化はサポートされません。

  - 部分信頼環境では、 `[Serializable]`/`ISerializable]` プログラミング モデルはサポートされていません。

  - 既知の型はコード内、またはマシン レベルの構成 (`Machine.config`) で指定する必要があります。 既知の型はセキュリティ上の理由からアプリケーション レベルの構成では指定できません。

- <xref:System.Runtime.Serialization.IObjectReference> メソッドにはセキュリティ アクセス許可 <xref:System.Runtime.Serialization.IObjectReference.GetRealObject%2A> が必要であるため、 `[SecurityPermission(SecurityAction.LinkDemand, Flags=SecurityPermissionFlag.SerializationFormatter)]`を実装した型は、部分信頼環境で例外をスローします。

## <a name="additional-notes-on-serialization"></a>シリアル化に関するその他のメモ

次の規則はデータ コントラクト シリアライザーによってサポートされる型にも適用されます。

- ジェネリック型は、データ コントラクト シリアライザーで完全にサポートされます。

- Null 許容値型は、データコントラクトシリアライザーによって完全にサポートされます。

- インターフェイス型は <xref:System.Object> (コレクション インターフェイスの場合はコレクション型) として扱われます。

- 構造体とクラスの両方がサポートされています。

- は、 <xref:System.Runtime.Serialization.DataContractSerializer> <xref:System.Xml.Serialization.XmlSerializer> および ASP.NET Web サービスで使用されるプログラミングモデルをサポートしていません。 特に、 <xref:System.Xml.Serialization.XmlElementAttribute> や <xref:System.Xml.Serialization.XmlAttributeAttribute>のような属性をサポートしていません。 このプログラミングモデルのサポートを有効にするには、WCF を、の代わりにを使用するように切り替える必要があり <xref:System.Xml.Serialization.XmlSerializer> <xref:System.Runtime.Serialization.DataContractSerializer> ます。

- <xref:System.DBNull> 型は、特殊な方法で処理されます。 これは、シングルトン型です。デシリアライザーは、逆シリアル化後にシングルトン制約に従い、シングルトン インスタンスへのすべての `DBNull` 参照を指します。 `DBNull` はシリアル化可能な型であるため、 <xref:System.Security.Permissions.SecurityPermissionAttribute.SerializationFormatter%2A> アクセス許可が必要です。

## <a name="see-also"></a>関連項目

- [データ コントラクトの XML および ADO.NET の種類](xml-and-ado-net-types-in-data-contracts.md)
- [データ コントラクトの使用](using-data-contracts.md)
- [シリアル化可能な型](serializable-types.md)
- [データ コントラクトのコレクション型](collection-types-in-data-contracts.md)
- [データ コントラクトの列挙型](enumeration-types-in-data-contracts.md)
