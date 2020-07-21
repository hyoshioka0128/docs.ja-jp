---
title: '方法: プロパティの変更通知を実装する'
description: Windows Presentation Foundation (WPF) で、プロパティ値が変更されたときにプロパティがバインディング ソースに自動的に通知できるようにします。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- notifications of change [WPF]
- data binding [WPF], property change notifications
- change notifications [WPF]
- properties [WPF], change notifications
ms.assetid: 30b59d9e-8c3a-4349-aa82-4be837e841cf
ms.openlocfilehash: 6c298930b7b1f812e94ea6add8f53c67d3453530
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620782"
---
# <a name="how-to-implement-property-change-notification"></a>方法: プロパティの変更通知を実装する
バインディング ターゲットのプロパティにバインディング ソースの動的変更が自動的に反映される (たとえば、ユーザーがフォームを編集するとプレビュー ペインが自動的に更新される) ようにするために、<xref:System.Windows.Data.BindingMode.OneWay> または <xref:System.Windows.Data.BindingMode.TwoWay> バインディングをサポートするには、クラスが適切なプロパティ変更通知を提供する必要があります。 この例では、<xref:System.ComponentModel.INotifyPropertyChanged> を実装するクラスを作成する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.ComponentModel.INotifyPropertyChanged> を実装するには、<xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> イベントを宣言し、`OnPropertyChanged` メソッドを作成する必要があります。 次に、変更を通知する必要のある各プロパティについて、そのプロパティが更新されるたびに `OnPropertyChanged` を呼び出します。  
  
 [!code-csharp[SimpleBinding#PersonClass](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Person.cs#personclass)]
 [!code-vb[SimpleBinding#PersonClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Person.vb#personclass)]  
  
 `Person` クラスを使用して <xref:System.Windows.Data.BindingMode.TwoWay> バインディングをサポートする例については、「[TextBox テキストでソースを更新するタイミングを制御する](how-to-control-when-the-textbox-text-updates-the-source.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [バインディング ソースの概要](binding-sources-overview.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [方法トピック](data-binding-how-to-topics.md)
