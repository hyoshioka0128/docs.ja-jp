---
title: '方法: デジタル署名で XML ドキュメントに署名する'
description: デジタル署名を使用して XML ドキュメントに署名する方法について説明します。 .NET では、System.xml 名前空間のクラスを使用します。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- signatures, XML signing
- System.Security.Cryptography.SignedXml class
- digital signatures, XML signing
- System.Security.Cryptography.RSACryptoServiceProvider class
- XML digital signatures
- XML signing
- signing XML
ms.assetid: 99692ac1-d8c9-42d7-b1bf-2737b01037e4
ms.openlocfilehash: 97bd23182ed54b899b76dbf43e179fe0c94b011d
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598568"
---
# <a name="how-to-sign-xml-documents-with-digital-signatures"></a>方法: デジタル署名で XML ドキュメントに署名する
<xref:System.Security.Cryptography.Xml> 名前空間のクラスを使用すると、XML ドキュメントまたは XML ドキュメントの一部にデジタル署名で署名することができます。  XML デジタル署名 (XMLDSIG) を使用すると、データが署名後に変更されなかったことを確認できます。  XMLDSIG 標準の詳細については、「World Wide Web コンソーシアム (W3C) 勧告」 [XML 署名の構文と処理](https://www.w3.org/TR/xmldsig-core/)に関する説明を参照してください。  
  
 この手順のコード例では、XML ドキュメント全体にデジタル署名し、<> 要素のドキュメントに署名を添付する方法を示し `Signature` ます。  この例では、RSA 署名キーを作成し、キーをセキュリティで保護されたキー コンテナーに追加してから、キーを使用して XML ドキュメントにデジタル署名しています。  キーは、XML デジタル署名を確認するために取得したり、別の XML ドキュメントの署名に使用したりすることができます。  
  
 この手順を使用して作成された XML デジタル署名を確認する方法については、「[方法: Xml ドキュメントのデジタル署名を検証](how-to-verify-the-digital-signatures-of-xml-documents.md)する」を参照してください。  
  
### <a name="to-digitally-sign-an-xml-document"></a>XML ドキュメントにデジタル署名するには  
  
1. <xref:System.Security.Cryptography.CspParameters> オブジェクトを作成し、キーのコンテナーの名前を指定します。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#2)]
     [!code-vb[HowToSignXMLDocumentRSA#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#2)]  
  
2. <xref:System.Security.Cryptography.RSACryptoServiceProvider> クラスを使用して非対称キーを生成します。  <xref:System.Security.Cryptography.CspParameters> オブジェクトを <xref:System.Security.Cryptography.RSACryptoServiceProvider> クラスのコンストラクターに渡すと、キーは自動的にキー コンテナーに保存されます。  このキーは、XML ドキュメントの署名に使用されます。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#3)]
     [!code-vb[HowToSignXMLDocumentRSA#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#3)]  
  
3. ディスクから XML ファイルを読み込んで <xref:System.Xml.XmlDocument> オブジェクトを作成します。  <xref:System.Xml.XmlDocument> オブジェクトには、暗号化する XML 要素が含まれています。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#4)]
     [!code-vb[HowToSignXMLDocumentRSA#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#4)]  
  
4. <xref:System.Security.Cryptography.Xml.SignedXml> オブジェクトを新規作成し、それに <xref:System.Xml.XmlDocument> オブジェクトを渡します。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#5)]
     [!code-vb[HowToSignXMLDocumentRSA#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#5)]  
  
5. 署名する RSA キーを <xref:System.Security.Cryptography.Xml.SignedXml> オブジェクトに追加します。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#6)]
     [!code-vb[HowToSignXMLDocumentRSA#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#6)]  
  
6. 署名内容について記述する <xref:System.Security.Cryptography.Xml.Reference> オブジェクトを作成します。  ドキュメント全体に署名するには、<xref:System.Security.Cryptography.Xml.Reference.Uri%2A> プロパティを `""` に設定します。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#7)]
     [!code-vb[HowToSignXMLDocumentRSA#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#7)]  
  
7. <xref:System.Security.Cryptography.Xml.XmlDsigEnvelopedSignatureTransform> オブジェクトを <xref:System.Security.Cryptography.Xml.Reference> オブジェクトに追加します。  変換を使用すると、検証側は、署名側が使用した方法と同一の方法で XML データを表すことができます。  XML データはさまざまな方法で表すことができるため、この手順は検証にとって重要です。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#8)]
     [!code-vb[HowToSignXMLDocumentRSA#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#8)]  
  
8. <xref:System.Security.Cryptography.Xml.Reference> オブジェクトを <xref:System.Security.Cryptography.Xml.SignedXml> オブジェクトに追加します。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#9](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#9)]
     [!code-vb[HowToSignXMLDocumentRSA#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#9)]  
  
9. <xref:System.Security.Cryptography.Xml.SignedXml.ComputeSignature%2A> メソッドを呼び出して署名を計算します。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#10](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#10)]
     [!code-vb[HowToSignXMLDocumentRSA#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#10)]  
  
10. 署名の XML 表現 (<`Signature`> 要素) を取得し、新しいオブジェクトに保存し <xref:System.Xml.XmlElement> ます。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#11](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#11)]
     [!code-vb[HowToSignXMLDocumentRSA#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#11)]  
  
11. <xref:System.Xml.XmlDocument> オブジェクトに要素を追加します。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#12](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#12)]
     [!code-vb[HowToSignXMLDocumentRSA#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#12)]  
  
12. ドキュメントを保存します。  
  
     [!code-csharp[HowToSignXMLDocumentRSA#13](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#13)]
     [!code-vb[HowToSignXMLDocumentRSA#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#13)]  
  
## <a name="example"></a>例  
 この例では、`test.xml` という名前のファイルがコンパイル済みのプログラムと同じディレクトリに存在することを前提としています。  次の XML を `test.xml` というファイルに配置し、この例で使用することができます。  
  
```xml  
<root>  
    <creditcard>  
        <number>19834209</number>  
        <expiry>02/02/2002</expiry>  
    </creditcard>  
</root>  
```  
  
 [!code-csharp[HowToSignXMLDocumentRSA#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToSignXMLDocumentRSA/cs/sample.cs#1)]
 [!code-vb[HowToSignXMLDocumentRSA#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToSignXMLDocumentRSA/vb/sample.vb#1)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
  
- この例をコンパイルするには、`System.Security.dll` への参照を含める必要があります。  
  
- 名前空間 <xref:System.Xml>、<xref:System.Security.Cryptography>、および <xref:System.Security.Cryptography.Xml> を含めます。  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 非対称キー ペアの秘密キーをプレーンテキストで保存または転送しないでください。  対称暗号化キーと非対称暗号化キーの詳細については、「[暗号化と復号化のためのキーの生成](generating-keys-for-encryption-and-decryption.md)」を参照してください。  
  
 秘密キーをソース コードに直接埋め込まないでください。  埋め込みキーは、 [ildasm.exe (IL 逆アセンブラー)](../../framework/tools/ildasm-exe-il-disassembler.md)を使用するか、メモ帳などのテキストエディターでアセンブリを開くことで、簡単にアセンブリから読み取ることができます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Security.Cryptography.Xml>
- [方法: XML ドキュメントのデジタル署名を検証する](how-to-verify-the-digital-signatures-of-xml-documents.md)
