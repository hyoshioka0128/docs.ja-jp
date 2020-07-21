---
title: '方法: INotifyPropertyChanged インターフェイスを実装する'
description: Windows フォームデータバインディングで使用されるビジネスオブジェクトに INotifyPropertyChanged インターフェイスを実装する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- INotifyPropertyChanged interface [Windows Forms], implementing
ms.assetid: eac428af-b43b-46ac-80d9-1a5f88658725
ms.openlocfilehash: 83d2ef32787d2dbcd877bc77dcede10111098f8a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619269"
---
# <a name="how-to-implement-the-inotifypropertychanged-interface"></a>方法: INotifyPropertyChanged インターフェイスを実装する
次のコード例は、インターフェイスを実装する方法を示して <xref:System.ComponentModel.INotifyPropertyChanged> います。 Windows フォームデータバインディングで使用されるビジネスオブジェクトにこのインターフェイスを実装します。 実装されている場合、インターフェイスは、ビジネスオブジェクトのプロパティの変更をバインドされたコントロールと通信します。  
  
## <a name="example"></a>例  
 [!code-csharp[System.ComponentModel.IPropertyChangeExample#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/CS/Form1.cs#1)]
 [!code-vb[System.ComponentModel.IPropertyChangeExample#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.IPropertyChangeExample/VB/Form1.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [方法: PropertyNameChanged パターンを適用する](how-to-apply-the-propertynamechanged-pattern.md)
- [Windows フォームでのデータ バインディング](windows-forms-data-binding.md)
- [方法: BindingSource と INotifyPropertyChanged の各インターフェイスを使用して変更通知を発生させる](./controls/raise-change-notifications--bindingsource.md)
- [Windows フォーム データ バインディングの変更通知](change-notification-in-windows-forms-data-binding.md)
