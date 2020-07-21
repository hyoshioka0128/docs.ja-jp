---
title: スタイルを含む WordprocessingML ドキュメント 2
ms.date: 07/20/2015
ms.assetid: a9136e4d-c368-4661-8049-7d45c679a236
ms.openlocfilehash: caf80014077bf57dc1ffb8eaeac6390cf4258015
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403551"
---
# <a name="wordprocessingml-document-with-styles"></a>スタイルを含む WordprocessingML ドキュメント
複雑な WordprocessingML ドキュメントには、スタイルを使用して書式設定された段落が含まれています。  
  
 WordprocessingML ドキュメントを構成する場合に役立つ情報をいくつか説明します。 WordprocessingML ドキュメントはパッケージに格納されます。 パッケージには複数のパーツがあります (パーツは、パッケージのコンテキストで使用する場合は明示的な意味を持っています。基本的には、パーツとはパッケージを構成するためにまとめて圧縮されたファイルです)。 スタイルを使用して書式設定された段落がドキュメントに含まれている場合、スタイルが適用されている段落を含むドキュメント パーツがあります。 ドキュメントによって参照されるスタイルを含むスタイル パーツもあります。  
  
 パッケージにアクセスする場合、任意のパスを使用してではなく、パーツ間のリレーションシップを通じてアクセスすることが重要です。 この問題は「WordprocessingML ドキュメント内のコンテンツの操作」のチュートリアルでは扱いませんが、このチュートリアルに用意されているプログラム例では正しい方法を示しています。  
  
## <a name="a-document-that-uses-styles"></a>スタイルを使用するドキュメント  
 「[WordprocessingML ドキュメントの構造 (Visual Basic)](shape-of-wordprocessingml-documents.md)」のトピックに示されている WordML の例は、とても簡単な例です。 次のドキュメントはもっと複雑になっています。段落がスタイルで書式設定されています。 Office Open XML ドキュメントを構成する XML を確認するには、「[Office Open XML ドキュメント パーツを出力する例 (Visual Basic)](example-that-outputs-office-open-xml-document-parts.md)」を実行するのが最も簡単です。  
  
 次のドキュメントでは、最初の段落にスタイル `Heading1` が設定されています。 既定のスタイルが設定されている段落が多数あります。 スタイル `Code` が設定されている段落も多数あります。 このドキュメントは比較的複雑であるため、LINQ to XML を使用した解析を行うのに適したドキュメントといえます。  
  
 既定以外のスタイルが設定されている段落では、段落要素に `w:pPr` という名前の子要素があり、この子要素には `w:pStyle` という子要素があります。 `w:val` 要素には、スタイル名を格納する  という属性があります。 段落に既定のスタイルが設定されている場合は、段落要素に `w:p.Pr` 子要素はありません。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<w:document  
    xmlns:ve="http://schemas.openxmlformats.org/markup-compatibility/2006"  
    xmlns:o="urn:schemas-microsoft-com:office:office"  
    xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships"  
    xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math"  
    xmlns:v="urn:schemas-microsoft-com:vml"  
    xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing"  
    xmlns:w10="urn:schemas-microsoft-com:office:word"  
    xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
    xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml">  
  <w:body>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Heading1" />  
      </w:pPr>  
      <w:r>  
        <w:t>Parsing WordprocessingML with LINQ to XML</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" />  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0">  
      <w:r>  
        <w:t>The following example prints to the console.</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" />  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r>  
        <w:t>using System;</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t>class Program {</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t xml:space="preserve">    public static void </w:t>  
      </w:r>  
      <w:smartTag w:uri="urn:schemas-microsoft-com:office:smarttags" w:element="place">  
        <w:r w:rsidRPr="00876F34">  
          <w:t>Main</w:t>  
        </w:r>  
      </w:smartTag>  
      <w:r w:rsidRPr="00876F34">  
        <w:t>(string[] args) {</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t xml:space="preserve">        Console.WriteLine("Hello World");</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t xml:space="preserve">    }</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRPr="00876F34" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r w:rsidRPr="00876F34">  
        <w:t>}</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" />  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0">  
      <w:r>  
        <w:t>This example produces the following output:</w:t>  
      </w:r>  
    </w:p>  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" />  
    <w:p w:rsidR="00A75AE0" w:rsidRDefault="00A75AE0" w:rsidP="006027C7">  
      <w:pPr>  
        <w:pStyle w:val="Code" />  
      </w:pPr>  
      <w:r>  
        <w:t>Hello World</w:t>  
      </w:r>  
    </w:p>  
    <w:sectPr w:rsidR="00A75AE0" w:rsidSect="00A75AE0">  
      <w:pgSz w:w="12240" w:h="15840" />  
      <w:pgMar w:top="1440" w:right="1800" w:bottom="1440" w:left="1800" w:header="720" w:footer="720" w:gutter="0" />  
      <w:cols w:space="720" />  
      <w:docGrid w:linePitch="360" />  
    </w:sectPr>  
  </w:body>  
</w:document>  
```  
  
## <a name="see-also"></a>関連項目

- [Office Open XML WordprocessingML ドキュメントの詳細 (Visual Basic)](details-of-office-open-xml-wordprocessingml-documents.md)
