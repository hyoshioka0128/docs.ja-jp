---
title: XSLT 変換
ms.date: 03/30/2017
ms.technology: dotnet-standard
ms.assetid: 202f8820-224c-494f-b61e-cd127eac6e03
ms.openlocfilehash: 92d0af1519260d458d3954beaef38e698142367a
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288304"
---
# <a name="xslt-transformations"></a>XSLT 変換
XSLT (Extensible Stylesheet Language Transformation) を使用すれば、ソース XML ドキュメントの内容を、形式や構造が異なる別のドキュメントに変換できます。 たとえば、XSLT を使用して、XML を Web サイトで使われる HTML に変換したり、アプリケーションが必要とするフィールドだけが含まれたドキュメントに変換したりできます。 この変換処理の仕様は、[W3C 勧告『XSL Transformations (XSLT) Version 1.0』](https://www.w3.org/TR/xslt-10/)で規定されています。  
  
 <xref:System.Xml.Xsl.XslCompiledTransform> クラスは .NET の XSLT プロセッサです。 <xref:System.Xml.Xsl.XslCompiledTransform> クラスは、[W3C 勧告『XSLT 1.0』](https://www.w3.org/TR/xslt-10/)をサポートしています。  
  
> [!NOTE]
> .NET Framework Version 2.0 では <xref:System.Xml.Xsl.XslTransform> クラスが廃止されています。 <xref:System.Xml.Xsl.XslCompiledTransform> クラスが XSLT エンジンの新しい実装です。 このクラスは、パフォーマンスが向上しており、新しいセキュリティ機能を備えています。 XSLT アプリケーションの作成には <xref:System.Xml.Xsl.XslCompiledTransform> クラスを使用することが推奨されています。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [XslCompiledTransform クラスの使用](using-the-xslcompiledtransform-class.md)  
 <xref:System.Xml.Xsl.XslCompiledTransform> クラスの使用方法について説明します。  
  
 [XslTransform クラスからの移行](migrating-from-the-xsltransform-class.md)  
 <xref:System.Xml.Xsl.XslTransform> クラスからコードを移行する方法について説明します。  
  
 [XSLT コンパイラ (xsltc.exe)](xslt-compiler-xsltc-exe.md)  
 XSLT コンパイラの使用方法について説明します。  
  
 [XslTransform クラスを使用した XSLT 変換](xslt-transformations-with-the-xsltransform-class.md)  
 <xref:System.Xml.Xsl.XslTransform> クラスの使用方法について説明します。  
  
## <a name="reference"></a>関連項目  
 <xref:System.Xml.Xsl.XslCompiledTransform>  
 <xref:System.Xml.Xsl.XsltArgumentList>  
 <xref:System.Xml.Xsl.XsltSettings>  
  
## <a name="related-sections"></a>関連項目  
 [XML ドキュメントと XML データ](index.md)
