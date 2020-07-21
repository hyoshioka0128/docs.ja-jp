---
title: '方法: 特定のデータ形式でデータを取得する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- drag-and-drop [WPF], retrieving data
- DataFormats class [WPF], retrieving data
- DataObject class [WPF], retrieving data
ms.assetid: a625acf3-1144-44cd-add7-456aefc3859f
ms.openlocfilehash: b3ec1b8fa873fd449956912e9e77e98b0362cb0e
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61768421"
---
# <a name="how-to-retrieve-data-in-a-particular-data-format"></a>方法: 特定のデータ形式でデータを取得する
次の例では、指定の形式でデータ オブジェクトからデータを取得する方法を示します。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、<xref:System.Windows.DataObject.GetDataPresent%28System.String%29> オーバーロードを使用し、指定のデータ形式が利用できるかどうかをまず確認します (ネイティブで利用できるか、自動変換で利用できるか)。指定の形式が利用できる場合、この例では、<xref:System.Windows.DataObject.GetData%28System.String%29> メソッドを使用することでデータが取得されます。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat)]  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、<xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29> オーバーロードを使用し、指定のデータ形式が利用できるかどうかをまず確認します (自動変換できるデータ形式がフィルター処理される)。指定の形式が利用できる場合、この例では、<xref:System.Windows.DataObject.GetData%28System.String%29> メソッドを使用することでデータが取得されます。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat_Native](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat_native)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat_Native](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat_native)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.IDataObject>
- [ドラッグ アンド ドロップの概要](drag-and-drop-overview.md)
