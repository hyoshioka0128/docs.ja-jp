---
title: '方法: プリンターを複製する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- print queues [WPF]
- cloning printers [WPF]
- printers [WPF], cloning
- print queues [WPF], cloning
- cloning print queues [WPF]
ms.assetid: dd6997c9-fe04-40f8-88a6-92e3ac0889eb
ms.openlocfilehash: e6af8d6410c4e383990bdaa27f97cc698be71719
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64649199"
---
# <a name="how-to-clone-a-printer"></a>方法: プリンターを複製する
ほとんどの企業は、ある時点で同じモデルのプリンターを複数購入します。 通常、これらはすべて、ほぼ同一の構成設定でインストールされます。 各プリンターのインストールには時間がかかり、エラーが発生しやすくなります。 <xref:System.Printing.IndexedProperties?displayProperty=nameWithType> 名前空間と、Microsoft .NET Framework で公開されている <xref:System.Printing.PrintServer.InstallPrintQueue%2A> クラスを使用すると、既存の印刷キューから複製された任意の数の追加の印刷キューをすぐにインストールすることができます。  
  
## <a name="example"></a>例  
 次の例では、2 番目の印刷キューが既存の印刷キューから複製されています。 2 番目と最初の違いは、名前、場所、ポート、および共有状態のみです。 これを行うための主な手順は次のとおりです。  
  
1. 複製する既存のプリンターの <xref:System.Printing.PrintQueue> オブジェクトを作成します。  
  
2. <xref:System.Printing.PrintQueue> の <xref:System.Printing.PrintSystemObject.PropertiesCollection%2A> から <xref:System.Printing.IndexedProperties.PrintPropertyDictionary> を作成します。 この辞書内の各エントリの <xref:System.Collections.DictionaryEntry.Value%2A> プロパティは、<xref:System.Printing.IndexedProperties.PrintProperty> から派生したいずれかの型のオブジェクトです。 この辞書内のエントリの値を設定するには、2 つの方法があります。  
  
    - 辞書の **Remove** と <xref:System.Printing.IndexedProperties.PrintPropertyDictionary.Add%2A> メソッドを使用してエントリを削除し、目的の値で再度追加します。  
  
    - 辞書の <xref:System.Printing.IndexedProperties.PrintPropertyDictionary.SetProperty%2A> メソッドを使用します。  
  
     次の例では、両方の方法を示しています。  
  
3. <xref:System.Printing.IndexedProperties.PrintBooleanProperty> オブジェクトを作成し、その <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> を "IsShared" に、またその <xref:System.Printing.IndexedProperties.PrintBooleanProperty.Value%2A> を `true` に設定します。  
  
4. <xref:System.Printing.IndexedProperties.PrintBooleanProperty> オブジェクトを使用して、<xref:System.Printing.IndexedProperties.PrintPropertyDictionary> の "IsShared" エントリの値にします。  
  
5. <xref:System.Printing.IndexedProperties.PrintStringProperty> オブジェクトを作成し、その <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> を "ShareName" に、またその <xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A> を適切な <xref:System.String> に設定します。  
  
6. <xref:System.Printing.IndexedProperties.PrintStringProperty> オブジェクトを使用して、<xref:System.Printing.IndexedProperties.PrintPropertyDictionary> の "ShareName" エントリの値にします。  
  
7. 別の <xref:System.Printing.IndexedProperties.PrintStringProperty> オブジェクトを作成し、その <xref:System.Printing.IndexedProperties.PrintProperty.Name%2A> を "Location" に、またその <xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A> を適切な <xref:System.String> に設定します。  
  
8. 2 番目の <xref:System.Printing.IndexedProperties.PrintStringProperty> オブジェクトを使用して、<xref:System.Printing.IndexedProperties.PrintPropertyDictionary> の "Location" エントリの値にします。  
  
9. <xref:System.String> の配列を作成します。 各項目は、サーバー上のポートの名前です。  
  
10. <xref:System.Printing.PrintServer.InstallPrintQueue%2A> を使用して、新しいプリンターを新しい値を使用してインストールします。  
  
 次に例を示します。  
  
 [!code-csharp[ClonePrinter#ClonePrinter](~/samples/snippets/csharp/VS_Snippets_Wpf/ClonePrinter/CSharp/Program.cs#cloneprinter)]
 [!code-vb[ClonePrinter#ClonePrinter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ClonePrinter/visualbasic/program.vb#cloneprinter)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Printing.IndexedProperties>
- <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>
- <xref:System.Printing.LocalPrintServer>
- <xref:System.Printing.PrintQueue>
- <xref:System.Collections.DictionaryEntry>
- [WPF のドキュメント](documents-in-wpf.md)
- [印刷の概要](printing-overview.md)
