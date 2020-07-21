---
title: 異なるストアでの XSLT 変換
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 369850e9-004a-45d2-b5c3-5060d9135adb
ms.openlocfilehash: 0eb98aad00227688df3e097ad674b44a29e5cb1a
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281714"
---
# <a name="xslt-transformations-over-different-stores"></a>異なるストアでの XSLT 変換
> [!NOTE]
> .NET Framework 2.0 では <xref:System.Xml.Xsl.XslTransform> クラスが廃止されています。 <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用して XSLT (Extensible Stylesheet Language for Transformations) 変換を実行できます。 詳しくは、「[XslCompiledTransform クラスの使用](using-the-xslcompiledtransform-class.md)」および「[XslTransform クラスからの移行](migrating-from-the-xsltransform-class.md)」をご覧ください。  
  
 ADO.NET と .NET Framework の XML クラスは、データ アクセス用の統合プログラミング モデルとして機能します。 そのデータは、XML データ (タグで区切られたテキスト) とリレーショナル データ (行と列で構成されたテーブル) のどちらとしても表されます。 .NET Framework の XML は、XML データを任意のデータ ストリームから XML ドキュメント オブジェクト モデル (DOM) ノード ツリーに読み込みます。読み込まれたデータにはプログラムからアクセスできます。一方、ADO.NET は、<xref:System.Data.DataSet> オブジェクト内のリレーショナル データにアクセスし、それを操作する手段を提供します。  
  
 XML DOM により、XML ドキュメント内のデータや追加のクラスにアクセスして、XML ドキュメント内で読み取り、書き込み、および移動を行うことができます。 これらのクラスは、<xref:System.Xml> 名前空間でサポートされます。この名前空間は、XML DOM と ADO.NET が提供するデータ アクセス サービスを統合する役割も果たします。 <xref:System.Xml.XmlDataDocument> は、データへのリレーショナル アクセスを可能にします。 <xref:System.Xml.XmlDataDocument> は、XML を ADO.NET <xref:System.Data.DataSet> 内のリレーショナル データに対応付けます。 .NET Framework ベースのアプリケーションであれば、<xref:System.Xml> 名前空間内のクラスを使用して、XML ドキュメントと <xref:System.Xml.XmlDataDocument> 内のリレーショナル データの両方にアクセスし、それらを操作できます。 この実装は、データを収集したり、分散させたりするための n 層アーキテクチャをサポートします。 詳細については、「[XML とリレーショナル データおよび ADO.NET との統合](xml-integration-with-relational-data-and-adonet.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [XslTransform クラスによる XSLT プロセッサの実装](xsltransform-class-implements-the-xslt-processor.md)
