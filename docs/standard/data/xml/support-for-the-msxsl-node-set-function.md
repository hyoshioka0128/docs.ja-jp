---
title: msxsl:node-set() 関数のサポート
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: d0cbf517-d9f6-4097-9851-4fa62903decd
ms.openlocfilehash: 747a0ff8c155f7635d5a6d2ebc76f287cf8646d4
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291449"
---
# <a name="support-for-the-msxslnode-set-function"></a>msxsl:node-set() 関数のサポート
`msxsl:node-set` 関数を使用すると、結果ツリー フラグメントをノード セットに変換できます。 結果として得られるノード セットには、常に単一のノードが含まれています。また、このノード セットは、常にそのツリーのルート ノードです。  
  
> [!NOTE]
> .NET Framework 2.0 では <xref:System.Xml.Xsl.XslTransform> クラスが廃止されています。 <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用して XSLT (Extensible Stylesheet Language for Transformations) 変換を実行できます。 詳しくは、「[XslCompiledTransform クラスの使用](using-the-xslcompiledtransform-class.md)」および「[XslTransform クラスからの移行](migrating-from-the-xsltransform-class.md)」をご覧ください。  
  
 `msxsl:node-set` 関数を使用すると、結果ツリー フラグメントをノード セットに変換できます。 結果として得られるノード セットには、常に単一のノードが含まれています。また、このノード セットは、常にそのツリーのルート ノードです。  
  
## <a name="example"></a>例  
 `$var` という変数がスタイル シート内のノード ツリーである例を次に示します。 for-each ステートメントを `node-set` 関数と組み合わせて使用すれば、このノード ツリーをノード セットとして反復処理できます。  
  
## <a name="nodesetxsl"></a>nodeset.xsl  
  
```xml  
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
                xmlns:msxsl="urn:schemas-microsoft-com:xslt"  
                xmlns:user="http://www.contoso.com"  
                version="1.0">  
    <xsl:variable name="books">  
        <book author="Michael Howard">Writing Secure Code</book>  
        <book author="Michael Kay">XSLT Reference</book>  
    </xsl:variable>  
  
    <xsl:template match="/">  
        <authors>  
            <xsl:for-each select="msxsl:node-set($books)/book">
                <author><xsl:value-of select="@author"/></author>  
            </xsl:for-each>  
        </authors>  
    </xsl:template>  
</xsl:stylesheet>  
```  
  
## <a name="output"></a>Output  
 変換による出力は次のとおりです。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<authors><author>Michael Howard</author><author>Michael Kay</author></authors>  
```  
  
## <a name="see-also"></a>関連項目

- [XslTransform クラスによる XSLT プロセッサの実装](xsltransform-class-implements-the-xslt-processor.md)
