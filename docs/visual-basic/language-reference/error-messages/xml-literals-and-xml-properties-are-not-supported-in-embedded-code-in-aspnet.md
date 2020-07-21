---
title: XML リテラルおよび XML プロパティは、ASP.NET 内の埋め込みコードではサポートされません
ms.date: 07/20/2015
f1_keywords:
- vbc31200
- bc31200
helpviewer_keywords:
- BC31200
ms.assetid: 053e8cba-8584-45cc-9fa0-43d122779772
ms.openlocfilehash: bda92b4244631f66142499a94be562854b35437e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406470"
---
# <a name="xml-literals-and-xml-properties-are-not-supported-in-embedded-code-within-aspnet"></a>XML リテラルおよび XML プロパティは、ASP.NET 内の埋め込みコードではサポートされません
XML リテラルおよび XML プロパティは、ASP.NET 内の埋め込みコードではサポートされません。 XML 機能を使用するには、コードをコードビハインドに移動します。  
  
 XML リテラルまたは XML 軸プロパティは、ASP.NET ファイルの埋め込みコード (`<%= =>`) 内で定義されます。  
  
 **エラー ID:** BC31200  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- XML リテラルまたは XML 軸プロパティが含まれているコードを、ASP.NET 分離コード ファイルに移動します。  
  
## <a name="see-also"></a>関連項目

- [XML リテラル](../xml-literals/index.md)
- [XML 軸プロパティ](../xml-axis/index.md)
- [XML](../../programming-guide/language-features/xml/index.md)
