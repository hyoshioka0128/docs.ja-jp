---
title: XslTransform からの出力
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 8e149d32-4b2f-493f-9e4b-d0d93475acde
ms.openlocfilehash: 5fa8c8228382f7f326a8d2243ed0450fca31f6fb
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288694"
---
# <a name="outputs-from-an-xsltransform"></a>XslTransform からの出力
スタイル シートは、`<xsl:output>` ステートメントと `method` 属性を使って出力形式を決定できます。次の表では、<xref:System.Xml.Xsl.XslTransform.Transform%2A> メソッドを使用して出力を書き出し、出力形式を <xref:System.IO.Stream> または <xref:System.IO.TextWriter> として宣言した場合に出力形式がどうなるかを説明します。  
  
> [!NOTE]
> .NET Framework 2.0 では <xref:System.Xml.Xsl.XslTransform> クラスが廃止されています。 <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用して XSLT (Extensible Stylesheet Language for Transformations) 変換を実行できます。 詳しくは、「[XslCompiledTransform クラスの使用](using-the-xslcompiledtransform-class.md)」および「[XslTransform クラスからの移行](migrating-from-the-xsltransform-class.md)」をご覧ください。  
  
 スタイル シートは、`<xsl:output>` ステートメントと `method` 属性を使って出力形式を決定できます。次の表では、<xref:System.Xml.Xsl.XslTransform.Transform%2A> メソッドを使用して出力を書き出し、出力形式を <xref:System.IO.Stream> または <xref:System.IO.TextWriter> として宣言した場合に出力形式がどうなるかを説明します。 <xref:System.Xml.Xsl.XslTransform.Transform%2A> メソッドを `<xsl:output>` ステートメントと共に使用して出力の種類を宣言した場合に得られる結果を次の表に示します。  
  
|\<xsl:output method = > 属性|結果の形式|  
|-----------------------------------------|-------------------|  
|method="xml"|XML|  
|method="html"|HTML|  
|method="text"|テキスト|  
  
> [!NOTE]
> メモ:<xref:System.Xml.Xsl.XslTransform.Transform%2A> メソッドの出力が <xref:System.Xml.XmlReader> または <xref:System.Xml.XmlWriter> である場合、`<xsl:output>` ステートメントは無視されます。  
  
 <xref:System.Xml.Xsl.XslTransform.Transform%2A> メソッドの出力が <xref:System.IO.Stream> または <xref:System.IO.TextWriter> である場合は、次の属性がサポートされます。  
  
- encoding*  
  
- omit-xml-declaration  
  
- スタンドアロン  
  
- doctype-public  
  
- doctype-system  
  
- cdata-section-elements  
  
- indent  
  
    > [!NOTE]
    > \*<xref:System.Xml.Xsl.XslTransform.Transform%2A> メソッドがその出力を <xref:System.IO.TextWriter> に送信する場合、encoding 属性は無視されます。 その場合は、encoding 属性の代わりに <xref:System.IO.TextWriter> の encoding プロパティが使用されます。
  
 <xref:System.Xml.Xsl.XslTransform.Transform%2A> メソッドの出力が <xref:System.IO.Stream> の場合、次の属性は無視されます。  
  
- version : バージョンは常に 1.0 です。  
  
- media-type : メディア タイプです。  
  
## <a name="escaping-special-characters"></a>特殊文字のエスケープ  
 `<xsl:text disable-output-escaping>` 記号の代わりに `<&lt>` を使用するなど、特殊文字を XML 形式にエスケープする必要があるかどうかを示すには、`"<"` タグを使用します。 `disable-output-escaping` オブジェクトまたは <xref:System.Xml.XmlReader> オブジェクトへの変換では <xref:System.Xml.XmlWriter> 属性が無視されるため、特殊文字はこのタグの影響を受けません。  
  
## <a name="see-also"></a>関連項目

- [XslTransform クラスによる XSLT プロセッサの実装](xsltransform-class-implements-the-xslt-processor.md)
