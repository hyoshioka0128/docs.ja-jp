---
title: '方法: データ形式がデータ オブジェクトに存在するかどうかを判別する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataFormats class [WPF]
- drag-and-drop [WPF], data formats present
- data formats [WPF], determining if present
ms.assetid: e487a454-c9fc-4e53-aeaa-c458d059ad4c
ms.openlocfilehash: 4cec733490e2a9dc5d54b3b253ac38a5090ac885
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776247"
---
# <a name="how-to-determine-if-a-data-format-is-present-in-a-data-object"></a>方法: データ形式がデータ オブジェクトに存在するかどうかを判別する
次の例は、さまざまな <xref:System.Windows.DataObject.GetDataPresent%2A> メソッドのオーバーロードを使用して、特定のデータ形式がデータ オブジェクトに存在するかどうかのクエリを実行する方法を示しています。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、<xref:System.Windows.DataObject.GetDataPresent%28System.String%29> オーバーロードを使用して、記述子文字列によって特定のデータ形式が存在するかどうかのクエリを実行します。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_String](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_querydataformats_string)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_String](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_querydataformats_string)]  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、<xref:System.Windows.DataObject.GetDataPresent%28System.Type%29> オーバーロードを使用して、型によって特定のデータ形式が存在するかどうかのクエリを実行します。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_Type](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_querydataformats_type)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_Type](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_querydataformats_type)]  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、<xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29> オーバーロードを使用して、記述子文字列によってデータのクエリを実行し、自動変換可能なデータ形式を扱う方法を指定します。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_Autoconvert](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_querydataformats_autoconvert)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_QueryDataFormats_Autoconvert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_querydataformats_autoconvert)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.IDataObject>
