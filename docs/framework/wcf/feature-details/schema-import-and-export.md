---
title: スキーマのインポートとエクスポート
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, schema import and export
- XsdDataContractExporter class
- XsdDataContractImporter class
ms.assetid: 0da32b50-ccd9-463a-844c-7fe803d3bf44
ms.openlocfilehash: 942ade69d92d8a213f65a3a2e463b6924e2f986e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84590216"
---
# <a name="schema-import-and-export"></a>スキーマのインポートとエクスポート
Windows Communication Foundation (WCF) には、新しいシリアル化エンジン、が含まれてい <xref:System.Runtime.Serialization.DataContractSerializer> ます。 は、 `DataContractSerializer` .NET Framework のオブジェクトと XML を双方向に変換します。 シリアライザー自体に加えて、WCF には、関連付けられたスキーマインポートおよびスキーマエクスポートメカニズムが含まれています。 *スキーマ*は、シリアライザーによって生成されるか、またはデシリアライザーがアクセスできる XML の構造について、正式で正確で、コンピューターが読み取り可能な記述です。 WCF は、World Wide Web コンソーシアム (W3C) XML スキーマ定義言語 (XSD) をスキーマ表現として使用します。これは、多数のサードパーティプラットフォームと幅広く相互運用できます。  
  
 スキーマインポートコンポーネントは、 <xref:System.Runtime.Serialization.XsdDataContractImporter> XSD スキーマドキュメントを受け取り、シリアル化された形式が特定のスキーマに対応するように .NET Framework クラス (通常はデータコントラクトクラス) を生成します。  
  
 たとえば、次のスキーマ フラグメントがあるとします。  
  
 [!code-csharp[c_SchemaImportExport#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#8)]
 [!code-vb[c_SchemaImportExport#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#8)]  
  
 これは、読みやすいように、やや簡素化された次の型を生成します。  
  
 [!code-csharp[c_SchemaImportExport#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#1)]
 [!code-vb[c_SchemaImportExport#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#1)]  
  
 生成される型は、データコントラクトのベストプラクティス (「[ベストプラクティス: データコントラクトのバージョン管理](../best-practices-data-contract-versioning.md)」にあります) に従うことに注意してください。  
  
- この型は <xref:System.Runtime.Serialization.IExtensibleDataObject> インターフェイスを実装します。 詳細については、「[上位互換性のあるデータ コントラクト](forward-compatible-data-contracts.md)」を参照してください。  
  
- データ メンバーは、プライベート フィールドをラップするパブリック プロパティとして実装されます。  
  
- クラスは部分クラスであり、生成されたコードを変更せずに追加を行うことができます。  
  
 <xref:System.Runtime.Serialization.XsdDataContractExporter> では反転を実行できます。つまり、`DataContractSerializer` によってシリアル化できる型を受け取って XSD スキーマ ドキュメントを生成できます。  
  
## <a name="fidelity-is-not-guaranteed"></a>忠実性は保証されない  
 スキーマや型のラウンド トリップでの完全な忠実性は保証されません  (*ラウンドトリップ*とは、スキーマをインポートして一連のクラスを作成し、その結果をエクスポートしてもう一度スキーマを作成することを意味します)。同じスキーマを返すことはできません。 また、これとは逆のプロセスでも忠実性は保証されません  (スキーマを生成する型をエクスポートしてから、型をインポートし直す場合です。 この場合も、同じ型が返されない可能性があります)。  
  
## <a name="supported-types"></a>サポートされている型  
 データ コントラクト モデルは、WC3 スキーマの限られたサブセットしかサポートしません。 このサブセットに準拠しないスキーマを使用すると、インポート プロセスで例外が発生します。 たとえば、データ コントラクトのデータ メンバーを XML 属性としてシリアル化するように指定することはできません。 したがって、XML 属性を使用する必要があるスキーマはサポートされず、適切な XML 投影を持つデータ コントラクトを生成できないため、インポート時に例外が発生します。  
  
 たとえば、次のスキーマ フラグメントは、既定のインポート設定を使用してインポートすることはできません。  
  
 [!code-xml[c_SchemaImportExport#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/common/source.config#9)]  
  
 詳細については、「[データコントラクトスキーマの参照](data-contract-schema-reference.md)」を参照してください。 スキーマがデータ コントラクト ルールに準拠していない場合は、別のシリアル化エンジンを使用します。 たとえば、<xref:System.Xml.Serialization.XmlSerializer> は、独自のスキーマ インポート機構を使用します。 また、サポートされるスキーマの範囲を拡張する特別なインポート モードもあります。 詳細については、「 <xref:System.Xml.Serialization.IXmlSerializable> [クラスを生成するためのスキーマのインポート](importing-schema-to-generate-classes.md)」で型を生成する方法に関するセクションを参照してください。  
  
 は `XsdDataContractExporter` 、でシリアル化できるすべての .NET Framework 型をサポートして `DataContractSerializer` います。 詳細については、「[データコントラクトシリアライザーでサポートされる型](types-supported-by-the-data-contract-serializer.md)」を参照してください。 通常、`XsdDataContractExporter` を使用して作成されたスキーマは、`XsdDataContractImporter` を使用してカスタマイズしない限り、<xref:System.Xml.Serialization.XmlSchemaProviderAttribute> で使用できる有効なデータです。  
  
 の使用方法の詳細については <xref:System.Runtime.Serialization.XsdDataContractImporter> 、「[スキーマをインポートしてクラスを生成する](importing-schema-to-generate-classes.md)」を参照してください。  
  
 の使用方法の詳細については <xref:System.Runtime.Serialization.XsdDataContractExporter> 、「[クラスからのスキーマのエクスポート](exporting-schemas-from-classes.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Serialization.DataContractSerializer>
- <xref:System.Runtime.Serialization.XsdDataContractImporter>
- <xref:System.Runtime.Serialization.XsdDataContractExporter>
- [クラスを作成するためのスキーマのインポート](importing-schema-to-generate-classes.md)
- [クラスからのスキーマのエクスポート](exporting-schemas-from-classes.md)
