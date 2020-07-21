---
title: '方法: データ オブジェクトを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataObject class [WPF], creating
- data objects [WPF], creating
- drag-and-drop [WPF], creating data objects
ms.assetid: 022fa142-717d-4fea-a53c-3b52e9d91aff
ms.openlocfilehash: deae8751518d9322e8d924a1b1fcbc20e25b35ed
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776494"
---
# <a name="how-to-create-a-data-object"></a>方法: データ オブジェクトを作成する
次の例は、<xref:System.Windows.DataObject> クラスによって提供されるコンストラクターを使用して、データ オブジェクトを作成するさまざまな方法を示しています。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、新しいデータ オブジェクトが作成され、オーバーロードされたコンストラクター (<xref:System.Windows.DataObject.%23ctor%28System.Object%29>) の 1 つを使用して、文字列でデータ オブジェクトが初期化されます。  この場合、格納されているデータの型に応じて適切なデータ形式が自動的に決定されます。格納されているデータの自動変換が既定で許可されています。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Simple](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_simple)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Simple](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_simple)]  
  
### <a name="description"></a>説明  
 次のコード例は、上記のコードの短縮版です。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Simple_Condensed](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_simple_condensed)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Simple_Condensed](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_simple_condensed)]  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、新しいデータ オブジェクトが作成され、オーバーロードされたコンストラクター (<xref:System.Windows.DataObject.%23ctor%28System.String%2CSystem.Object%29>) の 1 つを使用して、文字列と指定されたデータ形式でデータ オブジェクトが初期化されます。  この場合、データ形式は文字列で指定されます。<xref:System.Windows.DataFormats> クラスによって、事前に定義済みの型の文字列のセットが提供されます。 既定で、格納されているデータの自動変換が許可されています。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_typestring)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_typestring)]  
  
### <a name="description"></a>説明  
 次のコード例は、上記のコードの短縮版です。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString_Condensed](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_typestring_condensed)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString_Condensed](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_typestring_condensed)]  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、新しいデータ オブジェクトが作成され、オーバーロードされたコンストラクター (<xref:System.Windows.DataObject.%23ctor%2A>) の 1 つを使用して、文字列と指定されたデータ形式でデータ オブジェクトが初期化されます。  この場合、データ形式は <xref:System.Type> パラメーターによって指定されます。  既定で、格納されているデータの自動変換が許可されています。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Type](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_type)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Type](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_type)]  
  
### <a name="description"></a>説明  
 次のコード例は、上記のコードの短縮版です。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Type_Condensed](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_type_condensed)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_Type_Condensed](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_type_condensed)]  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次のコード例では、新しいデータ オブジェクトが作成され、オーバーロードされたコンストラクター (<xref:System.Windows.DataObject.%23ctor%28System.String%2CSystem.Object%2CSystem.Boolean%29>) の 1 つを使用して、文字列と指定されたデータ形式でデータ オブジェクトが初期化されます。  この場合、データ形式は文字列で指定されます。<xref:System.Windows.DataFormats> クラスによって、事前に定義済みの型の文字列のセットが提供されます。 この特定のコンストラクターのオーバーロードによって、呼び出し元で自動変換が許可されるかどうかを指定できるようになります。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_AutoConvert](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_autoconvert)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_AutoConvert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_autoconvert)]  
  
### <a name="description"></a>説明  
 次のコード例は、上記のコードの短縮版です。  
  
### <a name="code"></a>コード  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_AutoConvert_Condensed](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_autoconvert_condensed)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_AutoConvert_Condensed](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_autoconvert_condensed)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.IDataObject>
