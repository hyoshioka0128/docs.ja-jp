---
title: Windows ストア アプリおよび Windows ランタイムのための .NET Framework サポート
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- Windows Store apps, .NET Framework support for
- Windows Runtime, .NET Framework support for
- .NET for Windows Store apps
- .NET Framework, and Windows Store apps
- .NET Framework, and Windows Runtime
ms.assetid: 6fa7d044-ae12-4c54-b8ee-50915607a565
ms.openlocfilehash: 7ca5a1259f970f2db5400837eb7d20998dd824cb
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288863"
---
# <a name="net-framework-support-for-windows-store-apps-and-windows-runtime"></a>Windows ストア アプリおよび Windows ランタイムのための .NET Framework サポート

.NET Framework 4.5 では、Windows ランタイムを使用した多数のソフトウェア開発シナリオがサポートされています。 これらのシナリオは次の 3 つのカテゴリに分類されます。

- 「 [C# または Visual Basic を使用した Windows ストアアプリのためのロードマップ](https://docs.microsoft.com/previous-versions/windows/apps/br229583(v=win.10))」で説明されているように、xaml コントロールを使用した Windows 8.x ストアアプリの開発の[概要](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140)) [」を参照](https://docs.microsoft.com/previous-versions/windows/apps/br229566(v=win.10))してください。

- .NET Framework で作成する Windows 8.x ストアアプリで使用するクラスライブラリの開発。

- でパッケージ化された Windows ランタイムコンポーネントの開発。WinMD ファイルは、Windows ランタイムをサポートする任意のプログラミング言語で使用できます。 例については、「 [C# および Visual Basic での Windows ランタイムコンポーネントの作成](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)」を参照してください。

このトピックでは、3つのカテゴリすべてについて .NET Framework が提供するサポートの概要を示し、Windows ランタイムコンポーネントのシナリオについて説明します。 最初のセクションには、.NET Framework と Windows ランタイム間の関係に関する基本情報が含まれています。また、ヘルプシステムと IDE で発生する可能性のあるいくつかの特異についても説明しています。 [2 番目のセクション](#WindowsRuntimeComponents)では、Windows ランタイムコンポーネントを開発するシナリオについて説明します。

## <a name="the-basics"></a>基本操作

.NET Framework は、前に示した3つの開発シナリオをサポートしています。これは、Windows 8.x ストアアプリ用 .NET を提供し、Windows ランタイム自体をサポートすることによって行います。

- [.NET Framework および Windows ランタイム名前空間](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140)#net-framework-and-windows-runtime-namespaces)は、.NET Framework クラスライブラリの簡素化されたビューを提供し、Windows 8.x ストアアプリと Windows ランタイムコンポーネントの作成に使用できる型とメンバーのみを含みます。

  - Visual Studio (Visual Studio 2012 以降) を使用して Windows 8.x ストアアプリまたは Windows ランタイムコンポーネントを開発する場合、一連の参照アセンブリによって、関連する型とメンバーのみが表示されます。

  - この簡素化された API セットは、.NET Framework 内で重複する機能を削除するか、Windows ランタイム機能を複製することで、さらに簡略化されています。 たとえば、コレクション型のジェネリックバージョンのみが含まれており、XML ドキュメントオブジェクトモデルは、Windows ランタイム XML API セットを優先して削除されます。

  - Windows ランタイムはマネージコードから簡単に呼び出すことができるため、単にオペレーティングシステム API をラップする機能も削除されます。

  Windows 8.x ストアアプリ用 .NET の詳細については、「 [Windows ストアアプリ用 .net の概要](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))」を参照してください。 API の選択プロセスの詳細については、.NET ブログの「 [Metro スタイルアプリ用 .net](https://devblogs.microsoft.com/dotnet/net-for-metro-style-apps/) 」エントリを参照してください。

- [Windows ランタイム](/uwp/api/)は、Windows 8.x ストアアプリを構築するためのユーザーインターフェイス要素を提供し、オペレーティングシステムの機能へのアクセスを提供します。 .NET Framework と同様に、Windows ランタイムには、C# および Visual Basic コンパイラが .NET Framework クラスライブラリの使用方法 Windows ランタイムを使用できるようにするメタデータがあります。 .NET Framework を使用すると、いくつかの相違点を非表示にすることで、Windows ランタイムを簡単に使用できるようになります。

  - .NET Framework と Windows ランタイム間のプログラミングパターンの違い (イベントハンドラーの追加や削除のパターンなど) は表示されません。 ユーザーは .NET Framework のパターンを使用するとよいだけです。

  - よく使用される型 (たとえばプリミティブ型やコレクション) の違いの一部が非表示になります。 この記事の「 [IDE に表示される相違点](#DifferencesVisibleInIDE)」で説明したように、.NET Framework の型を使用するだけです。

ほとんどの場合、Windows ランタイムの .NET Framework サポートは透過的です。 次のセクションでは、マネージコードと Windows ランタイムの違いについて説明します。

<a name="AboutReferenceDocumentation"></a>

### <a name="the-net-framework-and-the-windows-runtime-reference-documentation"></a>.NET Framework と Windows ランタイムリファレンスドキュメント

Windows ランタイムと .NET Framework のドキュメントセットは別々になっています。 型またはメンバーに関するヘルプを表示するために F1 キーを押すと、該当するセットのリファレンス ドキュメントが表示されます。 ただし、 [Windows ランタイムリファレンス](/uwp/api/)を参照すると、不可解のような例が発生する可能性があります。

- インターフェイスなどのトピック <xref:Windows.Foundation.Collections.IIterable%601> には、Visual Basic または C# の宣言構文がありません。 代わりに、構文セクションの上にメモが表示されます (この例では、".NET: このインターフェイスは、system.string として表示されます \<T> )。 これは、.NET Framework と Windows ランタイムは、インターフェイスが異なる同様の機能を提供するためです。 さらに、`IIterable` では列挙子を返すのに `First` メソッドではなく <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> メソッドを使用するという、動作の違いもあります。 一般的なタスクを実行する別の方法を学習するのではなく、.NET Framework は、使い慣れた型を使用するようにマネージコードを表示することによって、Windows ランタイムをサポートしています。 IDE にはインターフェイスが表示されません `IIterable` 。そのため、Windows ランタイムリファレンスドキュメントでこのインターフェイスを使用する唯一の方法は、そのドキュメントを直接参照することです。

- このドキュメントでは、そのパラメーターの型が言語によって異なる場合があるという、 <xref:Windows.Web.Syndication.SyndicationFeed.%23ctor(System.String,System.String,Windows.Foundation.Uri)> 密接に関連する問題について説明します。 C# と Visual Basic の場合、パラメーターの型は <xref:System.String?displayProperty=nameWithType> と <xref:System.Uri?displayProperty=nameWithType> です。 これもやはり、.NET Framework で独自の `String` 型と `Uri` 型が使われるためであり、このようなよく使用される型について、.NET Framework ユーザーが処理を実行する別の方法を学習しても意味はありません。 IDE では、.NET Framework は対応する Windows ランタイムの種類を非表示にします。

- 構造体などのいくつかのケースでは、 <xref:Windows.UI.Xaml.GridLength> .NET Framework は同じ名前で、より多くの機能を持つ型を提供します。 たとえば、一連のコンストラクターとプロパティのトピックは `GridLength` に関連付けられますが、メンバーがマネージド コードでのみ使用可能であるために、Visual Basic と C# に関してのみ構文ブロックの機能を備えています。 Windows ランタイムでは、構造体にはフィールドしかありません。 Windows ランタイム構造体には、同等の <xref:Windows.UI.Xaml.GridLengthHelper> 機能を提供するためのヘルパークラスが必要です。 このヘルパー クラスは、マネージド コードを記述している間は IDE に表示されません。

- IDE では、Windows ランタイム型はから派生しているように見え <xref:System.Object?displayProperty=nameWithType> ます。 この型のメンバーは、<xref:System.Object> などの <xref:System.Object.ToString%2A?displayProperty=nameWithType> から継承されるように表示されます。 これらのメンバーは、型が実際にから継承された場合と同様に動作し、 <xref:System.Object> Windows ランタイム型をにキャストでき <xref:System.Object> ます。 この機能は、.NET Framework が Windows ランタイムに提供するサポートの一部です。 ただし、Windows ランタイムリファレンスドキュメントで型を表示した場合、そのようなメンバーは表示されません。 これらの見かけ上の継承されたメンバーに関するドキュメントは、<xref:System.Object?displayProperty=nameWithType> のリファレンス ドキュメントに含まれています。

<a name="DifferencesVisibleInIDE"></a>

### <a name="differences-that-are-visible-in-the-ide"></a>IDE で表示される相違点

C# で記述された Windows ランタイムコンポーネントを使用して、JavaScript を使用して Windows 用に開発された Windows 8.x ストアアプリのアプリケーションロジックを提供するなど、より高度なプログラミングシナリオでは、このような違いは IDE とドキュメントで明確になります。 コンポーネントが JavaScript にを返し、javascript `IDictionary<int, string>` デバッガーでそれを確認すると、javascript では `IMap<int, string>` Windows ランタイム型が使用されるため、のメソッドが表示されます。 よく使用されるコレクション型のうち、この 2 言語で表示が異なる型の一部を次の表に示します。

|Windows ランタイム型|対応する .NET Framework の型|
|--------------------------------------------------------------|---------------------------------------|
|`IIterable<T>`|`IEnumerable<T>`|
|`IIterator<T>`|`IEnumerator<T>`|
|`IVector<T>`|`IList<T>`|
|`IVectorView<T>`|`IReadOnlyList<T>`|
|`IMap<K, V>`|`IDictionary<TKey, TValue>`|
|`IMapView<K, V>`|`IReadOnlyDictionary<TKey, TValue>`|
|`IBindableIterable`|`IEnumerable`|
|`IBindableVector`|`IList`|
|`Windows.UI.Xaml.Data.INotifyPropertyChanged`|`System.ComponentModel.INotifyPropertyChanged`|
|`Windows.UI.Xaml.Data.PropertyChangedEventHandler`|`System.ComponentModel.PropertyChangedEventHandler`|
|`Windows.UI.Xaml.Data.PropertyChangedEventArgs`|`System.ComponentModel.PropertyChangedEventArgs`|

Windows ランタイムでは、 `IMap<K, V>` と `IMapView<K, V>` はを使用して反復処理され `IKeyValuePair` ます。 これらをマネージド コードに渡すと、`IDictionary<TKey, TValue>` および `IReadOnlyDictionary<TKey, TValue>` として表示されるため、これを列挙するには必然的に `System.Collections.Generic.KeyValuePair<TKey, TValue>` を使用します。

インターフェイスがマネージド コード内に表示される方法によって、これらのインターフェイスを実装する型の表示方法が決まります。 たとえば、`PropertySet` クラスは `IMap<K, V>` を実装しますが、これはマネージド コードでは `IDictionary<TKey, TValue>` として表示されます。 `PropertySet` では、`IMap<K, V>` ではなく `IDictionary<TKey, TValue>` が実装されたように見えるため、マネージド コードでは .NET Framework ディクショナリの `Add` メソッドのように動作する `Add` メソッドがあるように表示されます。 `Insert` メソッドがないように見えます。

.NET Framework を使用して Windows ランタイムコンポーネントを作成する方法、および JavaScript でそのようなコンポーネントを使用する方法を示すチュートリアルについては、「 [C# および Visual Basic での Windows ランタイムコンポーネントの作成](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)」を参照してください。

### <a name="primitive-types"></a>プリミティブ型

マネージコードで Windows ランタイムの自然な使用を有効にするために、コードでプリミティブ型 Windows ランタイムの代わりに .NET Framework プリミティブ型が表示されます。 .NET Framework では、`Int32` 構造体などのプリミティブ型には、`Int32.TryParse` メソッドなどの便利なプロパティとメソッドが多くあります。 これに対し、Windows ランタイムのプリミティブ型と構造体にはフィールドしかありません。 マネージド コードでプリミティブを使用すると、.NET Framework の型のように表示され、通常どおりに .NET Framework 型のプロパティとメソッドを使用できます。 要約すると、次のようになります。

- Windows ランタイムプリミティブ、、 `Int32` 、 `Int64` `Single` `Double` 、 `Boolean` 、 `String` (Unicode 文字の変更できないコレクション)、、、、およびでは、 `Enum` `UInt32` `UInt64` `Guid` 名前空間で同じ名前の型を使用し `System` ます。

- `UInt8` では `System.Byte` を使用します。

- `Char16` では `System.Char` を使用します。

- `IInspectable` インターフェイスでは、`System.Object` を使用します。

- `HRESULT` では、`System.Int32` のメンバーを 1 つ含む構造体を使用します。

インターフェイス型の場合と同様に、この表現の証拠が表示されるのは、.NET Framework プロジェクトが、JavaScript を使用してビルドされた Windows 8.x ストアアプリで使用される Windows ランタイムコンポーネントである場合のみです。

マネージコード内に同等の .NET Framework として表示されるその他の基本的な Windows ランタイム型には、構造体とし `Windows.Foundation.DateTime` てマネージコードに表示される構造体と、構造体として表示される構造体が含まれ <xref:System.DateTimeOffset?displayProperty=nameWithType> `Windows.Foundation.TimeSpan` <xref:System.TimeSpan?displayProperty=nameWithType> ます。

### <a name="other-differences"></a>その他の相違点

場合によっては、.NET Framework 型が Windows ランタイム型ではなくコードに表示されるという事実は、ユーザー側での操作が必要になります。 たとえば、クラスは <xref:Windows.Foundation.Uri?displayProperty=nameWithType> .NET Framework コードとして表示され <xref:System.Uri?displayProperty=nameWithType> ます。 <xref:System.Uri?displayProperty=nameWithType>相対 URI を使用できますが、 <xref:Windows.Foundation.Uri?displayProperty=nameWithType> 絶対 uri が必要です。 したがって、Windows ランタイムメソッドに URI を渡す場合は、絶対 URI であることを確認する必要があります。 「[Windows ランタイムへの URI の引き渡し](passing-a-uri-to-the-windows-runtime.md)」をご覧ください。

<a name="WindowsRuntimeComponents"></a>

## <a name="scenarios-for-developing-windows-runtime-components"></a>Windows ランタイム コンポーネントの開発シナリオ

マネージ Windows ランタイムコンポーネントでサポートされるシナリオは、次の一般的な原則によって異なります。

- .NET Framework を使用して構築された Windows ランタイムコンポーネントには、他の Windows Runtimelibraries と明らかな違いはありません。 たとえば、マネージコードを使用してネイティブ Windows ランタイムコンポーネントを再実装した場合、2つのコンポーネントはと区別できません。 コンポーネントがマネージド コードで記述されているという事実は、そのコード自体がマネージド コードであったとしても、そのコンポーネントを使用するコードには表示されません。 ただし内部的には、そのコンポーネントは真のマネージド コードであり、共通言語ランタイム (CLR) 上で実行されます。

- コンポーネントには、アプリケーションロジック、Windows 8.x ストア UI コントロール、またはその両方を実装する型を含めることができます。

  > [!NOTE]
  > アプリケーション ロジックから UI 要素を分離することをお勧めします。 また、windows 用に開発された windows 8.x ストアアプリでは、JavaScript と HTML を使用して windows 8.x ストアの UI コントロールを使用することはできません。

- コンポーネントには、Windows 8.x ストアアプリ用の Visual Studio ソリューション内のプロジェクト、または複数のソリューションに追加できる再利用可能なコンポーネントを使用できます。

  > [!NOTE]
  > コンポーネントが C# または Visual Basic でのみ使用される場合、Windows ランタイムコンポーネントにする必要はありません。 代わりに、通常の .NET Framework クラスライブラリにする場合は、パブリック API サーフェイスを Windows ランタイム型に制限する必要はありません。

- Windows ランタイム属性を使用して、 <xref:Windows.Foundation.Metadata.VersionAttribute> 異なるバージョンで追加された型 (および型のメンバー) を識別することにより、再利用可能なコンポーネントのバージョンをリリースできます。

- コンポーネント内の型は Windows ランタイム型から派生できます。 コントロールは、名前空間のプリミティブコントロール型、 <xref:Windows.UI.Xaml.Controls.Primitives> またはなどの完成したコントロールから派生でき <xref:Windows.UI.Xaml.Controls.Button> ます。

  > [!IMPORTANT]
  > Windows 8 および .NET Framework 4.5 以降では、マネージ Windows ランタイムコンポーネントのすべてのパブリック型がシールされている必要があります。 別の Windows ランタイムコンポーネントの型は、その型から派生することはできません。 コンポーネントでポリモーフィックな動作を提供するには、インターフェイスを作成し、そのインターフェイスをポリモーフィックな型に実装します。

- コンポーネント内のパブリック型のすべてのパラメーターと戻り値の型は Windows ランタイム型 (コンポーネントで定義されている Windows ランタイム型を含む) である必要があります。

次のセクションでは、一般的なシナリオの例を示します。

### <a name="application-logic-for-a-windows-8x-store-app-with-javascript"></a>JavaScript を使用した Windows 8.x ストアアプリ用のアプリケーションロジック

JavaScript を使用して windows 用 Windows 8.x ストアアプリを開発する場合は、アプリケーションロジックの一部がマネージコードでより適切に動作するか、開発が容易であることがわかります。 JavaScript では .NET Framework クラス ライブラリを直接使用できませんが、クラス ライブラリを .WinMD ファイルにすることができます。 このシナリオでは、Windows ランタイムコンポーネントはアプリの不可欠な部分であるため、バージョン属性を指定することは意味がありません。

### <a name="reusable-windows-8x-store-ui-controls"></a>再利用可能な Windows 8.x ストアの UI コントロール

一連の関連する UI コントロールを再利用可能な Windows ランタイムコンポーネントにパッケージ化できます。 コンポーネントは、単独で商品化することも、作成するアプリの要素として使用することもできます。 このシナリオでは、Windows ランタイム属性を使用して互換性を向上させることが理にかなって <xref:Windows.Foundation.Metadata.VersionAttribute> います。

### <a name="reusable-application-logic-from-existing-net-framework-apps"></a>既存の .NET Framework アプリからの再利用可能なアプリケーション ロジック

既存のデスクトップアプリからマネージコードをスタンドアロンの Windows ランタイムコンポーネントとしてパッケージ化することができます。 これにより、C++ または JavaScript を使用して構築された Windows 8.x ストアアプリや、C# または Visual Basic を使用してビルドされた Windows 8.x ストアアプリで、コンポーネントを使用できます。 コードに再利用シナリオが複数ある場合、バージョン管理はオプションです。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[Windows ストア アプリ用 .NET の概要](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))|Windows 8.x ストアアプリと Windows RuntimeComponents の作成に使用できる .NET Framework の型とメンバーについて説明します。 (Windows デベロッパー センター内)。|
|[C# または Visual Basic を使った Windows ストア アプリのためのロードマップ](https://docs.microsoft.com/previous-versions/windows/apps/br229583(v=win.10))|C# または Visual Basic (多くのクイックスタートトピック、ガイドライン、ベストプラクティスを含む) を使用して、Windows 8.x ストアアプリの開発を開始する際に役立つ主要なリソースを提供します。 (Windows デベロッパー センター内)。|
|[How to (XAML)](https://docs.microsoft.com/previous-versions/windows/apps/br229566(v=win.10))|C# または Visual Basic (多くのクイックスタートトピック、ガイドライン、ベストプラクティスを含む) を使用して、Windows 8.x ストアアプリの開発を開始する際に役立つ主要なリソースを提供します。 (Windows デベロッパー センター内)。|
|[C# および Visual Basic での Windows ランタイム コンポーネントの作成](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)|.NET Framework を使用して Windows ランタイムコンポーネントを作成する方法について説明します。また、JavaScript を使用して Windows 用にビルドされた Windows 8.x ストアアプリの一部として使用する方法、および Visual Studio との組み合わせをデバッグする方法について説明します。 (Windows デベロッパー センター内)。|
|[Windows ランタイム リファレンス](/uwp/api/)|Windows ランタイムのリファレンスドキュメントです。 (Windows デベロッパー センター内)。|
|[Windows ランタイムへの URI の引き渡し](passing-a-uri-to-the-windows-runtime.md)|マネージコードから Windows ランタイムに URI を渡すときに発生する可能性がある問題と、その回避方法について説明します。|
