---
title: データ連結に関連するインターフェイス
ms.date: 03/30/2017
helpviewer_keywords:
- data [Windows Forms], data-binding interfaces
- INotifyPropertyChanged interface
- IBindingListView interface
- IList interface [Windows Forms], Windows Forms data binding
- IBindingList interface [Windows Forms], Windows Forms data binding
- interfaces [Windows Forms], Windows Forms data binding
- IEditableObject interface [Windows Forms], Windows Forms data binding
- data binding [Windows Forms], interfaces
- IDataErrorInfo interface [Windows Forms], Windows Forms data binding
ms.assetid: 14e49a2e-3e46-47ca-b491-70d546333277
ms.openlocfilehash: 4e40f7ec1922cdf43e6a0b8f5734acaaeefbc514
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834588"
---
# <a name="interfaces-related-to-data-binding"></a>データ連結に関連するインターフェイス

ADO.NET を使用すると、アプリケーションのバインドニーズと使用するデータに合わせて、さまざまなデータ構造を作成できます。 Windows フォームでデータを提供または使用するための独自のクラスを作成することもできます。 これらのオブジェクトは、基本的なデータ バインディングから、デザイン時サポートの提供、エラー チェック、変更通知、データ自体に加えられた変更の構造化されたロールバックのサポートに至るまで、さまざまなレベルの機能を提供することができ、複雑さに対応できます。

## <a name="consumers-of-data-binding-interfaces"></a>データ バインディング インターフェイスのコンシューマー

以下のセクションでは、インターフェイスオブジェクトの2つのグループについて説明します。 1 つ目のグループでは、データ ソース作成者がデータ ソースに実装するインターフェイスを示します。 これらのインターフェイスは、データ ソース コンシューマーが使用するように設計されています。ほとんどの場合、データ ソース コンシューマーは、Windows フォーム コントロールまたはコンポーネントです。 2 つ目のグループでは、コンポーネント作成者向けに設計されたインターフェイスを示します。 コンポーネント作成者は、Windows フォーム データ バインディング エンジンが使用する、データ バインディングをサポートするコンポーネントを作成するときにこれらのインターフェイスを使用します。 フォームに関連付けられたクラス内でこれらのインターフェイスを実装することで、データ バインディングを実現できます。各ケースは、データの操作を可能にするインターフェイスを実装するクラスを示しています。 Visual Studio の迅速なアプリケーション開発 (RAD) データデザインエクスペリエンスツールは、既にこの機能を利用しています。

### <a name="interfaces-for-implementation-by-data-source-authors"></a>データ ソース作成者が実装するインターフェイス

以下のインターフェイスは、Windows フォーム コントロールで使用するように設計されています。

- <xref:System.Collections.IList> インターフェイス

  インターフェイスを実装<xref:System.Collections.ArrayList> <xref:System.Collections.CollectionBase>するクラスは、、、またはです。 <xref:System.Array> <xref:System.Collections.IList> これらは、型<xref:System.Object>の項目のインデックス付きリストです。 インデックスの最初の項目によって型が決定されるため、これらのリストには同種の型が含まれている必要があります。 <xref:System.Collections.IList>は、実行時にのみバインドに使用できます。

  > [!NOTE]
  > Windows フォームにバインドするビジネスオブジェクトの一覧を作成する場合は、 <xref:System.ComponentModel.BindingList%601>を使用することを検討してください。 は<xref:System.ComponentModel.BindingList%601> 、双方向の Windows フォームデータバインディングに必要なプライマリインターフェイスを実装する拡張可能なクラスです。

- <xref:System.ComponentModel.IBindingList> インターフェイス

  インターフェイスを<xref:System.ComponentModel.IBindingList>実装するクラスは、はるかに高いレベルのデータバインディング機能を提供します。 この実装では、基本的な並べ替え機能と変更通知を提供します。変更通知では、リスト項目が変更されたとき (たとえば、顧客リストの 3 番目の項目の Address フィールドが変更されたとき) と、リスト自体が変更されたとき (たとえば、リスト内の項目の数が増減したとき) のどちらの場合も変更が通知されます。 複数のコントロールを同じデータにバインドする予定であり、いずれかのコントロールで行われたデータ変更をバインドされた他のコントロールに反映させる必要がある場合に、変更通知が重要になります。

  > [!NOTE]
  > プロパティを<xref:System.ComponentModel.IBindingList> `true` <xref:System.ComponentModel.IBindingList.ListChanged>使用してインターフェイスの変更通知を有効にします。このプロパティは、リストが変更されたこと、またはリスト内の項目が変更されたことを示すイベントを発生させます。 <xref:System.ComponentModel.IBindingList.SupportsChangeNotification%2A>

  変更の種類は、 <xref:System.ComponentModel.ListChangedType> <xref:System.ComponentModel.ListChangedEventArgs>パラメーターのプロパティによって記述されます。 したがって、データ モデルが更新されるたびに、依存するビュー (同じデータ ソースにバインドされた他のコントロールなど) も更新されます。 ただし、一覧に含まれるオブジェクトは、リストが<xref:System.ComponentModel.IBindingList.ListChanged>イベントを発生させることができるように、変更時にリストに通知する必要があります。

  > [!NOTE]
  > は<xref:System.ComponentModel.BindingList%601> 、 <xref:System.ComponentModel.IBindingList>インターフェイスの一般的な実装を提供します。

- <xref:System.ComponentModel.IBindingListView> インターフェイス

  <xref:System.ComponentModel.IBindingListView>インターフェイスを実装するクラスは、の<xref:System.ComponentModel.IBindingList>実装のすべての機能に加えて、フィルター処理や高度な並べ替え機能を提供します。 この実装では、文字列ベースのフィルター処理と、プロパティ記述子と方向のペアによる複数列の並べ替え機能を提供します。

- <xref:System.ComponentModel.IEditableObject> インターフェイス

  <xref:System.ComponentModel.IEditableObject>インターフェイスを実装するクラスを使用すると、オブジェクトに対する変更が永続的になるタイミングをオブジェクトで制御できます。 この実装<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>では、 <xref:System.ComponentModel.IEditableObject.EndEdit%2A>、、および<xref:System.ComponentModel.IEditableObject.CancelEdit%2A>の各メソッドを使用して、オブジェクトに対して行われた変更をロールバックすることができます。 次に<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>、、、および<xref:System.ComponentModel.IEditableObject.CancelEdit%2A>の各メソッドの機能<xref:System.ComponentModel.IEditableObject.EndEdit%2A>について簡単に説明し、データに加えられた変更をロールバックできるように、それらのメソッドを相互に連携させる方法を示します。

  - メソッド<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>は、オブジェクトに対する編集の開始を通知します。 このインターフェイスを実装するオブジェクトは、メソッドが呼び出され<xref:System.ComponentModel.IEditableObject.BeginEdit%2A> <xref:System.ComponentModel.IEditableObject.CancelEdit%2A>た場合に更新を破棄できるように、メソッド呼び出しの後に更新を保存する必要があります。 データバインディング Windows フォームでは、1つ<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>の編集トランザクションのスコープ内でを複数回呼び出すことができ<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>ます<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>( <xref:System.ComponentModel.IEditableObject.EndEdit%2A>たとえば、、、)。 の<xref:System.ComponentModel.IEditableObject>実装では、が既<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>に呼び出されているかどうかを<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>追跡し、後続のへの呼び出しを無視する必要があります。 このメソッドは複数回呼び出すことができるので、それ以降の呼び出しは破壊的であることが重要です。つまり、それ以降<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>の呼び出しでは、作成された更新を破棄したり、最初<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>の呼び出しで保存されたデータを変更したりすることはできません。

  - オブジェクト<xref:System.ComponentModel.IEditableObject.EndEdit%2A>が現在編集モードで<xref:System.ComponentModel.IEditableObject.BeginEdit%2A>ある場合、メソッドは、が呼び出されてから基になるオブジェクトに変更をプッシュします。

  - メソッド<xref:System.ComponentModel.IEditableObject.CancelEdit%2A>は、オブジェクトに対して行われたすべての変更を破棄します。

  、 <xref:System.ComponentModel.IEditableObject.BeginEdit%2A> 、<xref:System.ComponentModel.IEditableObject.EndEdit%2A>およびの各メソッドの動作の詳細については、「[データベースにデータを保存する](/visualstudio/data-tools/save-data-back-to-the-database)」を参照<xref:System.ComponentModel.IEditableObject.CancelEdit%2A>してください。

  このトランザクションのデータ機能の概念は、 <xref:System.Windows.Forms.DataGridView>コントロールによって使用されます。

- <xref:System.ComponentModel.ICancelAddNew> インターフェイス

  インターフェイスを<xref:System.ComponentModel.ICancelAddNew>実装するクラスは、通常、 <xref:System.ComponentModel.IBindingList>インターフェイスを実装し、 <xref:System.ComponentModel.IBindingList.AddNew%2A>メソッドを使用してデータソースに加えられた追加をロールバックすることができます。 データソースが<xref:System.ComponentModel.IBindingList>インターフェイスを実装している場合は、 <xref:System.ComponentModel.ICancelAddNew>インターフェイスも実装する必要があります。

- <xref:System.ComponentModel.IDataErrorInfo> インターフェイス

  インターフェイスを実装するクラス<xref:System.ComponentModel.IDataErrorInfo>を使用すると、オブジェクトは、バインドされたコントロールにカスタムエラー情報を提供できます。

  - @No__t-0 プロパティは、一般的なエラーメッセージテキスト ("エラーが発生しました" など) を返します。

  - @No__t-0 プロパティは、列からの特定のエラーメッセージを含む文字列を返します (例: "`State` の列の値が無効です")。

- <xref:System.Collections.IEnumerable> インターフェイス

  インターフェイスを<xref:System.Collections.IEnumerable>実装するクラスは、通常、ASP.NET によって使用されます。 このインターフェイスの Windows フォームサポートは、コンポーネントを<xref:System.Windows.Forms.BindingSource>通じてのみ使用できます。

  > [!NOTE]
  > コンポーネント<xref:System.Windows.Forms.BindingSource>は、バインド<xref:System.Collections.IEnumerable>のためにすべての項目を別のリストにコピーします。

- <xref:System.ComponentModel.ITypedList> インターフェイス

  <xref:System.ComponentModel.ITypedList>インターフェイスを実装するコレクションクラスは、バインドされたコントロールに公開されるプロパティの順序とセットを制御する機能を提供します。

  > [!NOTE]
  > <xref:System.ComponentModel.ITypedList.GetItemProperties%2A> メソッド<xref:System.ComponentModel.PropertyDescriptor>を実装し、配列が null でない場合、配列の最後のエントリは、項目の別のリストであるリストプロパティを記述するプロパティ記述子になります。

- <xref:System.ComponentModel.ICustomTypeDescriptor> インターフェイス

  インターフェイスを<xref:System.ComponentModel.ICustomTypeDescriptor>実装するクラスは、それ自体に関する動的な情報を提供します。 このインターフェイスはに<xref:System.ComponentModel.ITypedList>似ていますが、リストではなくオブジェクトに使用されます。 このインターフェイスは、基<xref:System.Data.DataRowView>になる行のスキーマを射影するために、によって使用されます。 の<xref:System.ComponentModel.ICustomTypeDescriptor>単純な実装は、 <xref:System.ComponentModel.CustomTypeDescriptor>クラスによって提供されます。

  > [!NOTE]
  > を実装<xref:System.ComponentModel.ICustomTypeDescriptor>する型へのデザイン時バインディングをサポートするには、型<xref:System.ComponentModel.IComponent>もを実装し、フォームのインスタンスとして存在する必要があります。

- <xref:System.ComponentModel.IListSource> インターフェイス

  インターフェイスを<xref:System.ComponentModel.IListSource>実装するクラスは、リスト以外のオブジェクトのリストベースのバインドを有効にします。 の<xref:System.ComponentModel.IListSource.GetList%2A> <xref:System.Collections.IList>メソッドは、を継承しないオブジェクトからバインド可能なリストを返すために使用されます。 <xref:System.ComponentModel.IListSource> <xref:System.ComponentModel.IListSource>は、 <xref:System.Data.DataSet>クラスによって使用されます。

- <xref:System.ComponentModel.IRaiseItemChangedEvents> インターフェイス

  <xref:System.ComponentModel.IRaiseItemChangedEvents>インターフェイスを実装するクラスは、 <xref:System.ComponentModel.IBindingList>インターフェイスも実装するバインド可能なリストです。 このインターフェイスは、型が<xref:System.ComponentModel.IBindingList.ListChanged> <xref:System.ComponentModel.IRaiseItemChangedEvents.RaisesItemChangedEvents%2A>プロパティを通じて型<xref:System.ComponentModel.ListChangedType.ItemChanged>のイベントを発生させるかどうかを示すために使用されます。

  > [!NOTE]
  > 前に説明し<xref:System.ComponentModel.IRaiseItemChangedEvents>たイベント変換を一覧表示し、 <xref:System.Windows.Forms.BindingSource>コンポーネントと対話するプロパティがデータソースに用意されている場合は、を実装する必要があります。 それ以外の<xref:System.Windows.Forms.BindingSource>場合、では、イベント変換の一覧を表示するプロパティも実行され、パフォーマンスが低下します。

- <xref:System.ComponentModel.ISupportInitialize> インターフェイス

  インターフェイスを<xref:System.ComponentModel.ISupportInitialize>実装するコンポーネントには、プロパティの設定や共同依存プロパティの初期化のためのバッチ最適化の利点があります。 に<xref:System.ComponentModel.ISupportInitialize>は、次の2つのメソッドがあります。

  - <xref:System.ComponentModel.ISupportInitialize.BeginInit%2A>オブジェクトの初期化が開始されていることを通知します。

  - <xref:System.ComponentModel.ISupportInitialize.EndInit%2A>オブジェクトの初期化が完了していることを通知します。

- <xref:System.ComponentModel.ISupportInitializeNotification> インターフェイス

  インターフェイスを<xref:System.ComponentModel.ISupportInitializeNotification>実装するコンポーネントも<xref:System.ComponentModel.ISupportInitialize>インターフェイスを実装します。 このインターフェイスを使用すると、 <xref:System.ComponentModel.ISupportInitialize>初期化が完了したことを他のコンポーネントに通知できます。 インターフェイス<xref:System.ComponentModel.ISupportInitializeNotification>には、次の2つのメンバーが含まれます。

  - <xref:System.ComponentModel.ISupportInitializeNotification.IsInitialized%2A>コンポーネントが初期化されているかどうかを示す値を返します。`boolean`

  - <xref:System.ComponentModel.ISupportInitializeNotification.Initialized>が呼び出さ<xref:System.ComponentModel.ISupportInitialize.EndInit%2A>れたときに発生します。

- <xref:System.ComponentModel.INotifyPropertyChanged> インターフェイス

  このインターフェイスを実装するクラスは、プロパティ値のいずれかが変更されたときにイベントを発生させる型です。 このインターフェイスは、コントロールのプロパティごとに変更イベントを持つパターンを置き換えるように設計されています。 <xref:System.ComponentModel.BindingList%601>で使用する場合、ビジネスオブジェクトは<xref:System.ComponentModel.INotifyPropertyChanged.PropertyChanged> <xref:System.ComponentModel.INotifyPropertyChanged>インターフェイスを実装する必要があり\`、BindingList 1 はイベント<xref:System.ComponentModel.BindingList%601.ListChanged>を型<xref:System.ComponentModel.ListChangedType.ItemChanged>のイベントに変換します。

  > [!NOTE]
  > バインドされたクライアントとデータソースの間のバインディングで変更通知が発生するには、バインドされたデータソースの型で <xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスを実装するか (推奨)、バインドする型に*propertyName*@no__t イベントを指定しますが、両方を行わないでください。

### <a name="interfaces-for-implementation-by-component-authors"></a>コンポーネント作成者が実装するインターフェイス

以下のインターフェイスは、Windows フォーム データ バインディング エンジンが使用するように設計されています。

- <xref:System.Windows.Forms.IBindableComponent> インターフェイス

  このインターフェイスを実装するクラスは、データ バインディングをサポートするコントロール以外のコンポーネントです。 このクラスは、このインターフェイスのプロパティ<xref:System.Windows.Forms.IBindableComponent.DataBindings%2A>と<xref:System.Windows.Forms.IBindableComponent.BindingContext%2A>プロパティを使用して、コンポーネントのデータバインディングとバインディングコンテキストを返します。

  > [!NOTE]
  > コンポーネントがから<xref:System.Windows.Forms.Control>継承している場合は、 <xref:System.Windows.Forms.IBindableComponent>インターフェイスを実装する必要はありません。

- <xref:System.Windows.Forms.ICurrencyManagerProvider> インターフェイス

  <xref:System.Windows.Forms.ICurrencyManagerProvider>インターフェイスを実装するクラスは、この特定のコンポーネントに関連<xref:System.Windows.Forms.CurrencyManager>付けられているバインディングを管理するための独自のを提供するコンポーネントです。 カスタム<xref:System.Windows.Forms.CurrencyManager>へのアクセスは、 <xref:System.Windows.Forms.ICurrencyManagerProvider.CurrencyManager%2A>プロパティによって提供されます。

  > [!NOTE]
  > を<xref:System.Windows.Forms.Control>継承するクラスは、 <xref:System.Windows.Forms.Control.BindingContext%2A>プロパティを通じてバインドを自動的に管理します。そのため、 <xref:System.Windows.Forms.ICurrencyManagerProvider>を実装する必要がある場合は、非常にまれです。

## <a name="see-also"></a>関連項目

- [データ連結と Windows フォーム](data-binding-and-windows-forms.md)
- [2 つのオブジェクトが等しいかどうかをテストする方法Windows フォームに単純バインド コントロールを作成する](how-to-create-a-simple-bound-control-on-a-windows-form.md)
- [Windows フォームでのデータ バインディング](windows-forms-data-binding.md)
