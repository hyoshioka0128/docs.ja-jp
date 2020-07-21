---
title: データとデータ オブジェクト
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data transfer [WPF], drag-and-drop
- DataFormats class [WPF]
- DataObject class [WPF]
ms.assetid: 5967d557-1867-420f-a524-ae3af78402da
ms.openlocfilehash: 532c254f997da183b073ddc9e00b4364ecfcd739
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186346"
---
# <a name="data-and-data-objects"></a>データとデータ オブジェクト
ドラッグ アンド ドロップ操作の一部として転送されるデータは、データ オブジェクトに格納されます。  概念的には、データ オブジェクトには次のペアが 1 つ以上含まれます。  
  
- 実際のデータが含まれる <xref:System.Object>。  
  
- 対応するデータ形式識別子。  
  
 データ自体は、基の <xref:System.Object> として表すことができる任意のもので構成できます。  対応するデータ形式は、データの形式に関するヒントを提供する文字列または <xref:System.Type> です。  データ オブジェクトでは、複数のデータとデータ形式のペアをホストできます。これにより、1 つのデータ オブジェクトで、複数の形式のデータを提供できます。  
  
<a name="Data_and_Data_Objects"></a>
## <a name="data-objects"></a>データ オブジェクト  
 すべてのデータ オブジェクトでは、<xref:System.Windows.IDataObject> インターフェイスが実装されている必要があります。このインターフェイスでは、データ転送を可能にして容易にする、次の標準的なメソッドのセットが提供されています。  
  
|メソッド|まとめ|  
|------------|-------------|  
|<xref:System.Windows.IDataObject.GetData%2A>|指定したデータ形式でデータ オブジェクトを取得します。|  
|<xref:System.Windows.IDataObject.GetDataPresent%2A>|データを指定した形式で使用できるかどうか、または指定した形式に変換できるかどうかを確認します。|  
|<xref:System.Windows.IDataObject.GetFormats%2A>|このデータ オブジェクトのデータが格納されている形式の一覧、または変換できる形式の一覧を返します。|  
|<xref:System.Windows.IDataObject.SetData%2A>|指定したデータをこのデータ オブジェクトに格納します。|  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、<xref:System.Windows.DataObject> クラスの <xref:System.Windows.IDataObject> の基本的な実装が提供されます。 多くの一般的なデータ転送シナリオには、普通の <xref:System.Windows.DataObject> クラスで十分です。  
  
 ビットマップ、CSV、ファイル、HTML、RTF、文字列、テキスト、オーディオなど、定義済みの形式がいくつかあります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で提供されている定義済みのデータ形式の詳細については、<xref:System.Windows.DataFormats> クラスのリファレンス トピックを参照してください。  
  
 通常、データ オブジェクトには、データの抽出時にある形式で格納されたデータを別の形式に自動的に変換する機能が含まれています。この機能は、自動変換と呼ばれます。 データ オブジェクトで使用可能なデータ形式を問い合わせるときは、<xref:System.Windows.DataObject.GetFormats%28System.Boolean%29> メソッドまたは <xref:System.Windows.DataObject.GetDataPresent%28System.String%2CSystem.Boolean%29> メソッドを呼び出し、`autoConvert` パラメーターとして `false` を指定することにより、ネイティブ データ形式から自動変換可能なデータ形式をフィルターで除外できます。  <xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%2CSystem.Boolean%29> メソッドを使用してデータ オブジェクトにデータを追加する場合、`autoConvert` パラメーターを `false` に設定することにより、データの自動変換を禁止できます。  
  
<a name="Working_with_Data_Objects"></a>
## <a name="working-with-data-objects"></a>データ オブジェクトの操作  
 ここでは、データ オブジェクトを作成して操作するための一般的な手法について説明します。  
  
### <a name="creating-new-data-objects"></a>新しいデータ オブジェクトの作成  
 <xref:System.Windows.DataObject> クラスには複数のオーバーロードされたコンストラクターが用意されており、新しい <xref:System.Windows.DataObject> インスタンスにデータとデータ形式の 1 つのペアを簡単に設定できます。  
  
 次のコード例では、新しいデータ オブジェクトを作成し、オーバーロードされたコンストラクター <xref:System.Windows.DataObject.%23ctor%2A>(<xref:System.Windows.DataObject.%23ctor(System.String,System.Object)>) の 1 つを使用して、文字列と指定したデータ形式でデータ オブジェクトを初期化します。  この場合、データ形式は文字列で指定します。<xref:System.Windows.DataFormats> クラスによって、事前に定義された型の文字列のセットが提供されます。 既定では、格納されたデータの自動変換は許可されています。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_createdataobject_typestring)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_CreateDataObject_TypeString](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_createdataobject_typestring)]  
  
 データ オブジェクトを作成するコードの他の例については、「[データ オブジェクトを作成する](how-to-create-a-data-object.md)」を参照してください。  
  
### <a name="storing-data-in-multiple-formats"></a>複数の形式でのデータの格納  
 1 つのデータ オブジェクトに、複数の形式でデータを格納できます。   1 つのデータ オブジェクトへの複数のデータ形式の格納を戦略的に使用すると、データ オブジェクトが、1 つのデータ形式しか表現できない場合より、広範なドロップ ターゲットでデータ オブジェクトを使用できるようになる可能性があります。  一般に、ドラッグ元は、可能性のあるドロップ ターゲットで使用可能なデータ形式が何であっても対応できなければならないことに注意してください。  
  
 次の例では、<xref:System.Windows.DataObject.SetData%28System.String%2CSystem.Object%29> メソッドを使用して、複数の形式でデータ オブジェクトにデータを追加する方法を示します。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_storemultipleformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_StoreMultipleFormats](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_storemultipleformats)]  
  
### <a name="querying-a-data-object-for-available-formats"></a>データ オブジェクトでの使用可能な形式のクエリ  
 1 つのデータ オブジェクトに任意の数のデータ形式を含めることができるため、データ オブジェクトには使用可能なデータ形式の一覧を取得するための機能が含まれています。  
  
 次のコード例では、<xref:System.Windows.DataObject.GetFormats%2A> のオーバーロードを使用して、データ オブジェクトで使用できるすべてのデータ形式 (ネイティブと自動変換の両方) を示す文字列の配列を取得します。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getalldataformats)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetAllDataFormats](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getalldataformats)]  
  
 データ オブジェクトで使用可能なデータ形式を照会する他のコード例については、「[データ オブジェクト内のデータ形式の一覧を表示する](how-to-list-the-data-formats-in-a-data-object.md)」を参照してください。  データ オブジェクトで特定のデータ形式の存在を照会する例については、「[データ形式がデータ オブジェクトに存在するかどうかを判別する](how-to-determine-if-a-data-format-is-present-in-a-data-object.md)」を参照してください。  
  
### <a name="retrieving-data-from-a-data-object"></a>データ オブジェクトからのデータの取得  
 特定の形式でデータ オブジェクトからデータを取得するには、<xref:System.Windows.DataObject.GetData%2A> メソッドのいずれかを呼び出し、目的のデータ形式を指定するだけです。  <xref:System.Windows.DataObject.GetDataPresent%2A> メソッドの 1 つを使用して、特定のデータ形式が存在するかどうかを確認できます。  <xref:System.Windows.DataObject.GetData%2A> からは、<xref:System.Object> でデータが返されます。データ形式によっては、このオブジェクトを型固有のコンテナーにキャストできます。  
  
 次のコード例では、<xref:System.Windows.DataObject.GetDataPresent%28System.String%29> のオーバーロードを使用して、指定したデータ形式 (ネイティブまたは自動変換) が使用可能かどうかを確認しています。 指定した形式が使用可能な場合は、<xref:System.Windows.DataObject.GetData%28System.String%29> メソッドを使用してデータを取得します。  
  
 [!code-csharp[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/CSharp/Window1.xaml.cs#_dragdrop_getspecificdataformat)]
 [!code-vb[DragDrop_DragDropMiscCode#_DragDrop_GetSpecificDataFormat](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDrop_DragDropMiscCode/visualbasic/window1.xaml.vb#_dragdrop_getspecificdataformat)]  
  
 データ オブジェクトからデータを取得するコードの他の例については、「[特定のデータ形式でデータを取得する](how-to-retrieve-data-in-a-particular-data-format.md)」を参照してください。  
  
### <a name="removing-data-from-a-data-object"></a>データ オブジェクトからのデータの削除  
 データ オブジェクトからデータを直接削除することはできません。  データ オブジェクトからデータを効果的に削除するには、次の手順のようにします。  
  
1. 保持するデータだけが含まれる新しいデータ オブジェクトを作成します。  
  
2. 古いデータ オブジェクトから新しいデータ オブジェクトに必要なデータを "コピー" します。  データをコピーするには、<xref:System.Windows.DataObject.GetData%2A> メソッドのいずれかを使用して、生データが含まれる <xref:System.Object> を取得した後、<xref:System.Windows.DataObject.SetData%2A> メソッドのいずれかを使用して、新しいデータ オブジェクトにデータを追加します。  
  
3. 古いデータ オブジェクトを新しいデータ オブジェクトに置き換えます。  
  
> [!NOTE]
> <xref:System.Windows.DataObject.SetData%2A> メソッドでは、データ オブジェクトへのデータの追加だけが行われます。データとデータ形式が前回の呼び出しとまったく同じであっても、データは置き換えられません。 同じデータとデータ形式に対して <xref:System.Windows.DataObject.SetData%2A> を 2 回呼び出すと、データ オブジェクトにそのデータとデータ形式が 2 つ存在することになります。
