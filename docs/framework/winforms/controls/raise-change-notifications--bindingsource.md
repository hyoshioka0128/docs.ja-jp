---
title: '方法: BindingSource と INotifyPropertyChanged の各インターフェイスを使用して変更通知を発生させる'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- change notifications [Windows Forms], raising
- BindingSource component [Windows Forms], and IPropertyChange
- data sources [Windows Forms], detecting changes
- examples [Windows Forms], BindingSource component
- change notifications
- INotifyPropertyChanged interface [Windows Forms], using with BindingSource
- BindingSource component [Windows Forms], examples
ms.assetid: 7fa2cf51-c09f-4375-adf0-e36c5617f099
ms.openlocfilehash: 2fe4458aa43144a9c29ed67fd7bee99a37fe1434
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81739686"
---
# <a name="how-to-raise-change-notifications-using-a-bindingsource-and-the-inotifypropertychanged-interface"></a>方法: BindingSource と INotifyPropertyChanged の各インターフェイスを使用して変更通知を発生させる
コンポーネント<xref:System.Windows.Forms.BindingSource>は、データ ソースに含まれる型が実装<xref:System.ComponentModel.INotifyPropertyChanged>し、プロパティ値が変更されたときに<xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged>イベントを発生させると、データ ソースの変更を自動的に検出します。 この変更検出は、データ ソース値の<xref:System.Windows.Forms.BindingSource>変更に応じて自動的に更新されるようにバインドされたコントロールが役立ちます。  
  
> [!NOTE]
> データ ソースが <xref:System.ComponentModel.INotifyPropertyChanged> を実装し、非同期操作を実行している場合は、バック グラウンド スレッド上のデータ ソースを変更しないようにします。 代わりに、バック グラウンド スレッド上のデータを読み取り、UI スレッドでリストにデータをマージする必要があります。  
  
## <a name="example"></a>例  
 次のコード例は、<xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスの簡単な実装を示します。 <xref:System.Windows.Forms.BindingSource> が <xref:System.ComponentModel.INotifyPropertyChanged> 型の一覧にバインドされるときに、<xref:System.Windows.Forms.BindingSource> がバインドされたコントロールにデータ ソースの変更を自動的に渡す方法も示します。  
  
 `CallerMemberName` 属性を使用する場合、`NotifyPropertyChanged` メソッドの呼び出しが、文字列引数としてプロパティ名を指定する必要はありません。 詳細については、「[呼び出し元情報 (C#)」または「呼び出し](../../../csharp/language-reference/attributes/caller-information.md)[元情報 (Visual Basic)」を参照](../../../visual-basic/programming-guide/concepts/caller-information.md)してください。  
  
 [!code-csharp[System.ComponentModel.IPropertyChangeExample#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.IPropertyChangeExample#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- システム、システム.データ、システム図面、およびシステム.Windows.Forms アセンブリへの参照。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ComponentModel.INotifyPropertyChanged>
- [BindingSource コンポーネント](bindingsource-component.md)
- [方法: BindingSource ResetItem メソッドを使用して変更通知を発生させる](how-to-raise-change-notifications-using-the-bindingsource-resetitem-method.md)
