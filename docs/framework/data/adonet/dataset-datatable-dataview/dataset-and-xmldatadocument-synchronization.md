---
title: DataSet と XmlDataDocument の同期
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0ce3793d-54b2-47e4-8cf7-b0591cc4dd21
ms.openlocfilehash: e76e81153cb7d074fe975744c6b6041ee04be90f
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785430"
---
# <a name="dataset-and-xmldatadocument-synchronization"></a>DataSet と XmlDataDocument の同期
ADO.NET の <xref:System.Data.DataSet> には、データのリレーショナル表現があります。 階層データにアクセスするには、.NET Framework で使用できる XML クラスを使用できます。 従来、この 2 つのデータ表現は個別に使用されていました。 .NET Framework では、データのリレーショナル表現と階層表現の両方へリアルタイムに同期的な方法でアクセスできます。リレーショナル表現にアクセスするには **DataSet** オブジェクトを使用します。階層表現にアクセスするには <xref:System.Xml.XmlDataDocument> オブジェクトを使用します。  
  
 **DataSet** が **XmlDataDocument** と同期されているときは、両方のオブジェクトが 1 つのデータ セットで動作しています。 つまり **DataSet** が変更されると、その変更内容が **XmlDataDocument** に反映されます。この逆の反映も行われます。 **DataSet** と **XmlDataDocument** の間のリレーションシップにより、1 つのアプリケーションから 1 つのデータ セットを使用して、**DataSet** の周囲に構築されたサービス スイート全体 (Web Forms、Windows フォーム コントロール、Visual Studio、.NET デザイナーなど) にアクセスしたり、XML サービス スイート (XSL (Extensible Stylesheet Language)、XSLT (XSL Transformations)、XPath (XML Path Language) など) にアクセスしたりできる優れた柔軟性が実現されます。 アプリケーションでアクセス対象とするサービス セットを選択する必要はありません。どちらのサービス セットにもアクセスできます。  
  
 **DataSet** を **XmlDataDocument** と同期する方法は数種類あります。 次の操作を行うことができます。  
  
- **DataSet** にスキーマ (リレーショナル構造) とデータを読み込み、この DataSet を新しい **XmlDataDocument** と同期します。 この方法では、既存のリレーショナル データの階層ビューが作成されます。 次に例を示します。  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema and data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema and data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    ```  
  
- **DataSet** にスキーマだけを読み込み (厳密に型指定された **DataSet** など)、それを **XmlDataDocument** と同期します。次に、XML ドキュメントから **XmlDataDocument** を読み込みます。 この方法では、既存の階層データのリレーショナル ビューが作成されます。 **DataSet** スキーマのテーブル名と列名が、同期をとる XML 要素の名前と一致している必要があります。 この名前の一致では、大文字と小文字が区別されます。  
  
     **DataSet** のスキーマが一致する必要があるのは、リレーショナル ビューで公開する XML 要素だけです。 つまり、このドキュメント上に非常に大きい XML ドキュメントと非常に小さなリレーショナル ウィンドウを作成できます。 **DataSet** で XML ドキュメントの一部だけが公開される場合でも、**XmlDataDocument** では XML ドキュメント全体が保持されます。 (これの詳しい例については、「[Dataset と XmlDataDocument の同期](synchronizing-a-dataset-with-an-xmldatadocument.md)」をご覧ください)。  
  
     次のコード例では、**DataSet** を作成してそのスキーマを読み込み、**XmlDataDocument** と同期する手順を示します。 **DataSet** スキーマが一致する必要があるのは、**XmlDataDocument** の中で **DataSet** を使用して公開する要素だけであることに注意してください。  
  
    ```vb  
    Dim dataSet As DataSet = New DataSet  
  
    ' Add code here to populate the DataSet with schema, but not data.  
  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument(dataSet)  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    DataSet dataSet = new DataSet();  
  
    // Add code here to populate the DataSet with schema, but not data.  
  
    XmlDataDocument xmlDoc = new XmlDataDocument(dataSet);  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
     データが含まれる **DataSet** と同期されている **XmlDataDocument** を読み込むことはできません。 読み込もうとすると例外がスローされます。  
  
- 新しい **XmlDataDocument** を作成して、XML ドキュメントからこの XmlDataDocument を読み込みます。次に、**XmlDataDocument** の **DataSet** プロパティを使用してデータのリレーショナル ビューにアクセスします。 **DataSet** を使用して **XmlDataDocument** のデータを表示するには、**DataSet** のスキーマを設定する必要があります。 この場合も、**DataSet** スキーマのテーブル名と列名が、同期をとる XML 要素の名前と一致している必要があります。 この名前の一致では、大文字と小文字が区別されます。  
  
     次のコード例では、**XmlDataDocument** のデータのリレーショナル ビューにアクセスする方法を示します。  
  
    ```vb  
    Dim xmlDoc As XmlDataDocument = New XmlDataDocument  
    Dim dataSet As DataSet = xmlDoc.DataSet  
  
    ' Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml")  
    ```  
  
    ```csharp  
    XmlDataDocument xmlDoc = new XmlDataDocument();  
    DataSet dataSet = xmlDoc.DataSet;  
  
    // Add code here to create the schema of the DataSet to view the data.  
  
    xmlDoc.Load("XMLDocument.xml");  
    ```  
  
 **XmlDataDocument** を **DataSet** と同期するもう 1 つの利点は、XML ドキュメントが完全に保持されることです。 **ReadXml** を使用して XML ドキュメントのデータを **DataSet** に格納すると、**WriteXml** を使用してデータが XML ドキュメントとして書き込まれるときに、この XML ドキュメントと元の XML ドキュメントが大幅に異なる場合があります。 これは、**DataSet** では XML ドキュメントから読み込んだ空白などの書式設定や、要素順序などの階層情報が維持されないためです。 **DataSet** には、XML ドキュメントで無視された要素も含まれていません。これは、これらの要素が **Dataset** のスキーマに一致しないためです。 **XmlDataDocument** を **DataSet** と同期することで、元の XML ドキュメントの書式設定要素や階層要素の構造が **XmlDataDocument** で維持され、**DataSet** には **DataSet** に適切なデータおよびスキーマ情報だけが含まれます。  
  
 **DataSet** を **XmlDataDocument** と同期する場合、<xref:System.Data.DataRelation> オブジェクトが入れ子かどうかによって同期結果が異なります。 詳しくは、「[DataRelation の入れ子化](nesting-datarelations.md)」をご覧ください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [DataSet と XmlDataDocument の同期](synchronizing-a-dataset-with-an-xmldatadocument.md)  
 最小限のスキーマが含まれており、厳密に型指定された **DataSet** を **XmlDataDocument** と同期させる方法を示します。  
  
 [DataSet に対する XPath クエリの実行](performing-an-xpath-query-on-a-dataset.md)  
 **DataSet** の内容に対して XPath クエリを実行する方法を示します。  
  
 [DataSet への XSLT 変換の適用](applying-an-xslt-transform-to-a-dataset.md)  
 **DataSet** の内容に XSLT 変換を適用する方法を示します。  
  
## <a name="related-sections"></a>関連項目  
 [DataSet での XML の使用](using-xml-in-a-dataset.md)  
 **DataSet** の内容を XML データとして読み込んで永続化する方法など、**DataSet** でデータ ソースとして XML と対話する方法を説明します。  
  
 [DataRelation の入れ子化](nesting-datarelations.md)  
 **DataSet** の内容を XML データとして表現する場合における、入れ子になった **DataRelation** オブジェクトの重要性について説明します。また、このようなリレーションを作成する方法について説明します。  
  
 [DataSet、DataTable、および DataView](index.md)  
 **DataSet** について説明し、DataSet を使用したアプリケーション データの管理方法と、DataSet を使用したデータ ソース (リレーショナル データベースや XML など) との対話方法について説明します。  
  
 <xref:System.Xml.XmlDataDocument>  
 **XmlDataDocument** クラスに関するリファレンス情報が含まれます。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET の概要](../ado-net-overview.md)
