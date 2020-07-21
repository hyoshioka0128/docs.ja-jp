---
title: '方法: データ オブジェクト内のデータ形式の一覧を表示する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- drag-and-drop [WPF], listing data formats
- DataFormats class [WPF]
- data formats [WPF], listing
ms.assetid: 18e7ba4b-ccef-4815-ae2d-3a32891010c0
ms.openlocfilehash: f8230eac33a18a0d99cc757d54c2b901c1afe977
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001495"
---
# <a name="how-to-list-the-data-formats-in-a-data-object"></a>方法: データ オブジェクト内のデータ形式の一覧を表示する
次の例では、<xref:System.Windows.DataObject.GetFormats%2A> メソッドのオーバーロードを使用して、データ オブジェクトで使用できる各データ形式を示す文字列の配列を取得する方法を示します。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、<xref:System.Windows.DataObject.GetFormats%2A> のオーバーロードを使用して、データ オブジェクトで使用できるすべてのデータ形式 (ネイティブと自動変換の両方) を示す文字列の配列を取得します。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats)]  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、<xref:System.Windows.DataObject.GetFormats%2A> のオーバーロードを使用して、データ オブジェクトで使用できるデータ形式のみ (自動変換可能なデータ形式はフィルター処理済み) を示す文字列の配列を取得します。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats_NativeOnly](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats_nativeonly)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats_NativeOnly](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats_nativeonly)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.IDataObject>
- [ドラッグ アンド ドロップの概要](drag-and-drop-overview.md)
