---
title: '方法: XslTransform コードを移行する'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 910beb2f-cfb3-4e8e-9936-f7e0c5f4064a
ms.openlocfilehash: 42ca884c269611ebf7dae3b4e7aa8a39ba96b521
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287741"
---
# <a name="how-to-migrate-your-xsltransform-code"></a>方法: XslTransform コードを移行する
新しい XSLT クラスは、従来のクラスに非常に近いものとなるように設計されています。 <xref:System.Xml.Xsl.XslCompiledTransform> クラスは <xref:System.Xml.Xsl.XslTransform> クラスを置き換えます。 スタイル シートは <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> メソッドを使用してコンパイルされます。 変換は <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> メソッドを使用して行われます。 次の手順では、一般的な XSLT タスクを挙げ、<xref:System.Xml.Xsl.XslTransform> クラスと <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用したコードを比較します。  
  
### <a name="to-transform-a-file-and-output-to-a-uri"></a>ファイルを変換して URI に出力するには  
  
- <xref:System.Xml.Xsl.XslTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#9](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#9)]
     [!code-vb[XML_Migration#9](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#9)]  
  
- <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#10](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#10)]
     [!code-vb[XML_Migration#10](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#10)]  
  
### <a name="to-compile-a-style-sheet-and-use-a-resolver-with-default-credentials"></a>スタイル シートをコンパイルして、既定の資格情報でリゾルバーを使用するには  
  
- <xref:System.Xml.Xsl.XslTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#11](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#11)]
     [!code-vb[XML_Migration#11](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#11)]  
  
- <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#12](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#12)]
     [!code-vb[XML_Migration#12](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#12)]  
  
### <a name="to-use-an-xslt-parameter"></a>XSLT パラメーターを使用するために必要な処理  
  
- <xref:System.Xml.Xsl.XslTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#13](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#13)]
     [!code-vb[XML_Migration#13](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#13)]  
  
- <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#14](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#14)]
     [!code-vb[XML_Migration#14](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#14)]  
  
### <a name="to-enable-xslt-scripting"></a>XSLT スクリプトを有効にするには  
  
- <xref:System.Xml.Xsl.XslTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#15](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#15)]
     [!code-vb[XML_Migration#15](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#15)]  
  
- <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#16](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#16)]
     [!code-vb[XML_Migration#16](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#16)]  
  
### <a name="to-load-the-results-into-a-dom-object"></a>結果を DOM オブジェクトに読み込むには  
  
- <xref:System.Xml.Xsl.XslTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#19](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#19)]
     [!code-vb[XML_Migration#19](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#19)]  
  
- <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用したコード。  
  
    > [!NOTE]
    > <xref:System.Xml.Xsl.XslCompiledTransform> クラスには、XSLT 変換結果を <xref:System.Xml.XmlReader> オブジェクトとして返すメソッドはありません。 しかし、XML ファイルに出力して、その XML ファイルを別のオブジェクトに読み込むことができます。  
  
     [!code-csharp[XML_Migration#20](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#20)]
     [!code-vb[XML_Migration#20](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#20)]  
  
### <a name="to-stream-the-results-into-another-data-store"></a>結果を別のデータ ストアにストリーム出力するには  
  
- <xref:System.Xml.Xsl.XslTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#17](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#17)]
     [!code-vb[XML_Migration#17](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#17)]  
  
- <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用したコード。  
  
     [!code-csharp[XML_Migration#18](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#18)]
     [!code-vb[XML_Migration#18](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#18)]  
  
## <a name="see-also"></a>関連項目

- [XslTransform クラスからの移行](migrating-from-the-xsltransform-class.md)
- [XslCompiledTransform クラスの使用](using-the-xslcompiledtransform-class.md)
