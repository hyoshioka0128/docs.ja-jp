---
title: '方法: XDocument、XElement、または LINQ for XML クエリの結果にバインドする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], binding to XDocument
- data binding [WPF], binding to XElement
ms.assetid: 6a629a49-fe1c-465d-b76a-3dcbf4307b64
ms.openlocfilehash: 070f67f30613d4522a48e08fd1c208fbe5887525
ms.sourcegitcommit: 82f94a44ad5c64a399df2a03fa842db308185a76
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72920125"
---
# <a name="how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results"></a>方法: XDocument、XElement、または LINQ for XML クエリの結果にバインドする

この例では、<xref:System.Xml.Linq.XDocument> を使用して XML データを <xref:System.Windows.Controls.ItemsControl> にバインドする方法を示します。

## <a name="example"></a>例

次の XAML コードでは、<xref:System.Windows.Controls.ItemsControl> を定義し、`Planet` 型のデータ用のデータ テンプレートを `http://planetsNS` XML 名前空間に含めます。 名前空間を占有する XML データ型では、名前空間をかっこで囲んで含める必要があります。また、その XML データ型が、XAML マークアップ拡張機能が出現する可能性がある場所に出現する場合は、名前空間の前に、かっこのエスケープ シーケンスを使用して指定する必要があります。 このコードでは、<xref:System.Xml.Linq.XElement> クラスの <xref:System.Xml.Linq.XContainer.Element%2A> および <xref:System.Xml.Linq.XElement.Attribute%2A> メソッドに対応する動的プロパティにバインドします。 動的プロパティによって、XAML がこれらのメソッドの名前を共有する動的プロパティにバインドできます。 詳しくは、「[LINQ to XML の動的プロパティ](linq-to-xml-dynamic-properties.md)」をご覧ください。 XML 用の既定の名前空間宣言が属性名には適用されないことに注意してください。

[!code-xaml[XLinqExample#StackPanelResources](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#stackpanelresources)]
[!code-xaml[XLinqExample#ItemsControl](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml#itemscontrol)]

次の C# コードでは、<xref:System.Xml.Linq.XDocument.Load%2A> を呼び出して、スタック パネルのデータ コンテキストを、`http://planetsNS` XML 名前空間内の `SolarSystemPlanets` という名前の要素のすべてのサブ要素に設定します。

[!code-csharp[XLinqExample#LoadDCFromFile](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromfile)]
[!code-vb[XLinqExample#LoadDCFromFile](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromfile)]

XML データは、<xref:System.Windows.Data.ObjectDataProvider> を使用して XAML リソースとして格納できます。 コード例全体については、「[L2DBForm.xaml ソース コード](l2dbform-xaml-source-code.md)」を参照してください。 次の例は、コードでデータ コンテキストをオブジェクト リソースに設定する方法を示しています。

[!code-csharp[XLinqExample#LoadDCFromXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#loaddcfromxaml)]
[!code-vb[XLinqExample#LoadDCFromXAML](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#loaddcfromxaml)]

<xref:System.Xml.Linq.XContainer.Element%2A> および <xref:System.Xml.Linq.XElement.Attribute%2A> に動的プロパティをマップすることによって、XAML 内での柔軟性が増します。 コードを LINQ for XML クエリの結果にバインドすることもできます。 この例は、要素の値によって並べられたクエリ結果にバインドします。

[!code-csharp[XLinqExample#BindToResults](~/samples/snippets/csharp/VS_Snippets_Wpf/XLinqExample/CSharp/Window1.xaml.cs#bindtoresults)]
[!code-vb[XLinqExample#BindToResults](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XLinqExample/visualbasic/window1.xaml.vb#bindtoresults)]

## <a name="see-also"></a>関連項目

- [バインディング ソースの概要](binding-sources-overview.md)
- [LINQ to XML による WPF のデータ バインディングの概要](wpf-data-binding-with-linq-to-xml-overview.md)
- [LINQ to XML を使用した WPF のデータ バインディングの例](linq-to-xml-data-binding-sample.md)
- [LINQ to XML の動的プロパティ](linq-to-xml-dynamic-properties.md)
