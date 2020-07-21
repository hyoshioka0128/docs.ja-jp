---
title: '方法: 文字列を解析する'
ms.date: 07/20/2015
ms.assetid: 896e1b4b-f9bd-4975-8bc1-55b6badce1ac
ms.openlocfilehash: 0a9076fc516bb8e6bc74732ca252fabfeda43d53
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84398013"
---
# <a name="how-to-parse-a-string-visual-basic"></a>方法: 文字列を解析する (Visual Basic)
このトピックでは、C# で XML ツリーを作成する方法について説明します。  
  
## <a name="example"></a>例  
 Visual Basic では、`XElement.Parse` メソッドを使用して文字列を解析できます。 ただし、次のコードに示すように XML リテラルを使用する方が効率的です。これは、XML リテラルでは、文字列から XML を解析する場合のようなパフォーマンスの低下がないためです。  
  
 XML リテラルを使用すると、XML を Visual Basic プログラムに単にコピーして貼り付けることができます。  
  
> [!NOTE]
> テキストの解析やテキスト ファイルからの XML ドキュメントの読み込みは、関数型構築より非効率です。 XML ツリーをコードから初期化すると、関数型構築で必要となるプロセッサ時間は、テキストの解析に比べて短くなります。  
  
```vb  
Dim contacts as XElement = _  
    <Contacts>  
        <Contact>  
            <Name>Patrick Hines</Name>  
            <Phone Type="home">206-555-0144</Phone>  
            <Phone Type="work">425-555-0145</Phone>  
            <Address>  
            <Street1>123 Main St</Street1>  
            <City>Mercer Island</City>  
            <State>WA</State>  
            <Postal>68042</Postal>  
            </Address>  
            <NetWorth>10</NetWorth>  
        </Contact>  
        <Contact>  
            <Name>Gretchen Rivas</Name>  
            <Phone Type="mobile">206-555-0163</Phone>  
            <Address>  
            <Street1>123 Main St</Street1>  
            <City>Mercer Island</City>  
            <State>WA</State>  
            <Postal>68042</Postal>  
            </Address>  
            <NetWorth>11</NetWorth>  
        </Contact>  
    </Contacts>  
```  
  
## <a name="see-also"></a>関連項目

- [XML の解析 (Visual Basic)](parsing-xml.md)
