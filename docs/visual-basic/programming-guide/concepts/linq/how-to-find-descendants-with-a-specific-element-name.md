---
title: '方法: 特定の要素名を持つ子孫を検索する'
ms.date: 07/20/2015
ms.assetid: 78915518-0d25-4051-ab55-929779989510
ms.openlocfilehash: 19e0807f3bb7e83061b2076a177107eec126e717
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405210"
---
# <a name="how-to-find-descendants-with-a-specific-element-name-visual-basic"></a>方法: 特定の要素名を持つ子孫を検索する (Visual Basic)
特定の名前を持つ子孫をすべて検索しなければならない場合があります。 すべての子孫を反復処理するコードを記述することもできますが、<xref:System.Xml.Linq.XContainer.Descendants%2A> 軸を使用する方が簡単です。  
  
## <a name="example"></a>例  
 要素名に基づいて子孫を検索する方法の例を次に示します。  
  
```vb  
Dim root As XElement = _  
    <root>  
        <para>  
            <r>  
                <t>Some text </t>  
            </r>  
            <n>  
                <r>  
                    <t>that is broken up into </t>  
                </r>  
            </n>  
            <n>  
                <r>  
                    <t>multiple segments.</t>  
                </r>  
            </n>  
        </para>  
    </root>  
  
Dim textSegs As IEnumerable(Of String) = _  
    From seg In root...<t> _  
    Select seg.Value  
  
Dim str As String = textSegs.Aggregate( _  
    New StringBuilder, _  
    Function(sb, i) sb.Append(i), _  
    Function(sb) sb.ToString)  
  
Console.WriteLine(str)  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```console  
Some text that is broken up into multiple segments.  
```  
  
## <a name="example"></a>例  
 次の例は名前空間に含まれている XML 用のクエリです。これらのクエリは上の例と同じ機能を表しています。 詳細については、「[名前空間の概要 (LINQ to XML) (Visual Basic)](namespaces-overview-linq-to-xml.md)」を参照してください。  
  
```vb  
Imports <xmlns='http://www.adatum.com'>  
  
Module Module1  
    Sub Main()  
        Dim root As XElement = _  
            <root>  
                <para>  
                    <r>  
                        <t>Some text </t>  
                    </r>  
                    <n>  
                        <r>  
                            <t>that is broken up into </t>  
                        </r>  
                    </n>  
                    <n>  
                        <r>  
                            <t>multiple segments.</t>  
                        </r>  
                    </n>  
                </para>  
            </root>  
  
        Dim textSegs As IEnumerable(Of String) = _  
            From seg In root...<t> _  
            Select seg.Value  
  
        Dim str As String = textSegs.Aggregate( _  
            New StringBuilder, _  
            Function(sb, i) sb.Append(i), _  
            Function(sb) sb.ToString)  
  
        Console.WriteLine(str)  
    End Sub  
End Module  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```console  
Some text that is broken up into multiple segments.  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XContainer.Descendants%2A>
- [基本的なクエリ (LINQ to XML) (Visual Basic)](basic-queries-linq-to-xml.md)
