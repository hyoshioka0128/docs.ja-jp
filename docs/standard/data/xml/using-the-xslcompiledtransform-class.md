---
title: XslCompiledTransform クラスの使用
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: f9b074f6-d6f4-49dd-a093-df510bf0cf7b
ms.openlocfilehash: 8705b4c6324ce20a1f37d3ee864ab494adcdd6a5
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84281772"
---
# <a name="using-the-xslcompiledtransform-class"></a>XslCompiledTransform クラスの使用
<xref:System.Xml.Xsl.XslCompiledTransform> クラスは Microsoft .NET Framework XSLT プロセッサです。 このクラスは、スタイル シートをコンパイルし、XSLT 変換を実行するために使用されます。  
  
> [!NOTE]
> 全体的なパフォーマンスは <xref:System.Xml.Xsl.XslCompiledTransform> クラスの方が <xref:System.Xml.Xsl.XslTransform> クラスより優れていますが、<xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> クラスの <xref:System.Xml.Xsl.XslCompiledTransform> メソッドが変換で初めて呼び出されたときは、<xref:System.Xml.Xsl.XslTransform.Load%2A> クラスの <xref:System.Xml.Xsl.XslTransform> メソッドよりパフォーマンスが劣る場合があります。 これは、XSLT ファイルを読み込む前にコンパイルする必要があるためです。 詳細については、ブログ記事「[XslCompiledTransform Slower than XslTransform?](https://docs.microsoft.com/archive/blogs/antosha/xslcompiledtransform-slower-than-xsltransform)」(XslCompiledTransform は XslTransform よりも遅いか?) を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [XslCompiledTransform クラスへの入力](inputs-to-the-xslcompiledtransform-class.md)  
 使用可能な XSLT 入力オプションについて説明します。  
  
 [XslCompiledTransform クラスの出力オプション](output-options-on-the-xslcompiledtransform-class.md)  
 使用可能な XSLT 出力オプションについて説明します。  
  
 [XSLT 処理中の外部リソースの解決](resolving-external-resources-during-xslt-processing.md)  
 外部リソースを解決するための <xref:System.Xml.XmlResolver> クラスの使用について説明します。  
  
 [XSLT スタイル シートの拡張](extending-xslt-style-sheets.md)  
 XSLT の拡張機能のサポートについて説明します。  
  
|||  
|-|-|  
|[XSLT エラーの解決](recoverable-xslt-errors.md)|W3C (World Wide Web Consortium) 勧告『XSLT 1.0』で許可されている随意動作を示し、<xref:System.Xml.Xsl.XslCompiledTransform> クラスによるこれらの動作の処理方法を説明します。|  
|[方法: ノード フラグメントを変換する](how-to-transform-a-node-fragment.md)|ノード フラグメントの変換方法を説明します。|  
  
## <a name="related-sections"></a>関連項目  
 [XslTransform クラスからの移行](migrating-from-the-xsltransform-class.md)  
 <xref:System.Xml.Xsl.XslTransform> クラスからコードを移行する方法について説明します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Xsl.XsltSettings>
- <xref:System.Xml.Xsl.XsltMessageEncounteredEventArgs>
