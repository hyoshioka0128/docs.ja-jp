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
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 2f46d21123ecfda4bd336edbbd79fabf01e002a4
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835326"
---
# <a name="net-framework-support-for-windows-store-apps-and-windows-runtime"></a>Windows ストア アプリおよび Windows ランタイムのための .NET Framework サポート

.NET Framework 4.5 では、Windows ランタイムを使用した多数のソフトウェア開発シナリオがサポートされています。 これらのシナリオは次の 3 つのカテゴリに分類されます。

- 「[または Visual Basic をC#使用した windows ストアアプリのためのロードマップ](https://docs.microsoft.com/previous-versions/windows/apps/br229583(v=win.10))」で説明されているように、xaml コントロールを使用して @no__t 0 のアプリを開発する」、「[方法 (XAML)](https://docs.microsoft.com/previous-versions/windows/apps/br229566(v=win.10))、および[windows ストアアプリ用 .net の概要」](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))を参照してください。

- .NET Framework で作成する [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] アプリで使用するクラス ライブラリを開発する。

- でパッケージ化された Windows ランタイムコンポーネントの開発。WinMD ファイルは、Windows ランタイムをサポートする任意のプログラミング言語で使用できます。 例については、「 [」 C#および「Visual Basic での Windows ランタイムコンポーネントの作成](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)」を参照してください。

このトピックでは、3つのカテゴリすべてについて .NET Framework が提供するサポートの概要を示し、Windows ランタイムコンポーネントのシナリオについて説明します。 最初のセクションには、.NET Framework と Windows ランタイム間の関係に関する基本情報が含まれています。また、ヘルプシステムと IDE で発生する可能性のあるいくつかの特異についても説明しています。 [2 番目のセクション](#WindowsRuntimeComponents)では、Windows ランタイムコンポーネントを開発するシナリオについて説明します。

## <a name="the-basics"></a>基本事項

.NET Framework は、前に示した3つの開発シナリオをサポートしています。このシナリオでは、@no__t 0 を指定し、Windows ランタイム自体をサポートしています。

- [.NET Framework および Windows ランタイム名前空間](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140)#net-framework-and-windows-runtime-namespaces)は、.NET Framework クラスライブラリの簡素化されたビューを提供し、@no__t 1 アプリおよび Windows ランタイムコンポーネントの作成に使用できる型とメンバーのみを含みます。

  - Visual Studio (Visual Studio 2012 以降) を使用して @no__t 0 アプリまたは Windows ランタイムコンポーネントを開発する場合、一連の参照アセンブリによって、関連する型とメンバーのみが表示されます。

  - この簡素化された API セットは、.NET Framework 内で重複する機能を削除するか、Windows ランタイム機能を複製することで、さらに簡略化されています。 たとえば、コレクション型のジェネリックバージョンのみが含まれており、XML ドキュメントオブジェクトモデルは、Windows ランタイム XML API セットを優先して削除されます。

  - Windows ランタイムはマネージコードから簡単に呼び出すことができるため、単にオペレーティングシステム API をラップする機能も削除されます。

  @No__t-0 の詳細については、「 [Windows ストアアプリ用 .net の概要](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))」を参照してください。 API の選択プロセスの詳細については、.NET ブログの「 [Metro スタイルアプリ用 .net](https://devblogs.microsoft.com/dotnet/net-for-metro-style-apps/) 」エントリを参照してください。

- [Windows ランタイム](/uwp/api/)は、@no__t 1 アプリを構築するためのユーザーインターフェイス要素を提供し、オペレーティングシステムの機能へのアクセスを提供します。 .NET Framework と同様に、Windows ランタイムには、 C#および Visual Basic コンパイラが .NET Framework クラスライブラリの使用方法 Windows ランタイムを使用できるようにするメタデータがあります。 .NET Framework を使用すると、いくつかの相違点を非表示にすることで、Windows ランタイムを簡単に使用できるようになります。

  - .NET Framework と Windows ランタイム間のプログラミングパターンの違い (イベントハンドラーの追加や削除のパターンなど) は表示されません。 ユーザーは .NET Framework のパターンを使用するとよいだけです。

  - よく使用される型 (たとえばプリミティブ型やコレクション) の違いの一部が非表示になります。 この記事の「 [IDE に表示される相違点](#DifferencesVisibleInIDE)」で説明したように、.NET Framework の型を使用するだけです。

ほとんどの場合、Windows ランタイムの .NET Framework サポートは透過的です。 次のセクションでは、マネージコードと Windows ランタイムの違いについて説明します。

<a name="AboutReferenceDocumentation"></a>

### <a name="the-net-framework-and-the-windows-runtime-reference-documentation"></a>.NET Framework と Windows ランタイムリファレンスドキュメント

Windows ランタイムと .NET Framework のドキュメントセットは別々になっています。 型またはメンバーに関するヘルプを表示するために F1 キーを押すと、該当するセットのリファレンス ドキュメントが表示されます。 ただし、 [Windows ランタイムリファレンス](/uwp/api/)を参照すると、不可解のような例が発生する可能性があります。

- @No__t-0 インターフェイスなどのトピックには Visual Basic またはC#の宣言構文がありません。 代わりに、構文のセクション (この場合は ".NET:このインターフェイスは >、no__t ") として表示されます。 これは、.NET Framework と Windows ランタイムは、インターフェイスが異なる同様の機能を提供するためです。 さらに、`IIterable` では列挙子を返すのに `First` メソッドではなく <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> メソッドを使用するという、動作の違いもあります。 一般的なタスクを実行する別の方法を学習するのではなく、.NET Framework は、使い慣れた型を使用するようにマネージコードを表示することによって、Windows ランタイムをサポートしています。 IDE に `IIterable` インターフェイスは表示されません。そのため、Windows ランタイムのリファレンスドキュメントでは、そのドキュメントを直接参照することによってのみ表示されます。

- @No__t 0 のドキュメントは、密接に関連する問題を示しています。このパラメーターの型は、言語によって異なる場合があります。 C# と Visual Basic の場合、パラメーターの型は <xref:System.String?displayProperty=nameWithType> と <xref:System.Uri?displayProperty=nameWithType> です。 これもやはり、.NET Framework で独自の `String` 型と `Uri` 型が使われるためであり、このようなよく使用される型について、.NET Framework ユーザーが処理を実行する別の方法を学習しても意味はありません。 IDE では、.NET Framework は対応する Windows ランタイムの種類を非表示にします。

- @No__t 0 構造体など、いくつかのケースでは、.NET Framework は同じ名前で、より多くの機能を持つ型を提供します。 たとえば、一連のコンストラクターとプロパティのトピックは `GridLength` に関連付けられますが、メンバーがマネージド コードでのみ使用可能であるために、Visual Basic と C# に関してのみ構文ブロックの機能を備えています。 Windows ランタイムでは、構造体にはフィールドしかありません。 Windows ランタイム構造体には、同等の機能を提供するために、@no__t 0 のヘルパークラスが必要です。 このヘルパー クラスは、マネージド コードを記述している間は IDE に表示されません。

- IDE では、Windows ランタイム型は <xref:System.Object?displayProperty=nameWithType> から派生するように見えます。 この型のメンバーは、<xref:System.Object> などの <xref:System.Object.ToString%2A?displayProperty=nameWithType> から継承されるように表示されます。 これらのメンバーは、型が実際に <xref:System.Object> から継承された場合と同様に動作し、Windows ランタイム型を <xref:System.Object> にキャストできます。 この機能は、.NET Framework が Windows ランタイムに提供するサポートの一部です。 ただし、Windows ランタイムリファレンスドキュメントで型を表示した場合、そのようなメンバーは表示されません。 これらの見かけ上の継承されたメンバーに関するドキュメントは、<xref:System.Object?displayProperty=nameWithType> のリファレンス ドキュメントに含まれています。

<a name="DifferencesVisibleInIDE"></a>

### <a name="differences-that-are-visible-in-the-ide"></a>IDE で表示される相違点

JavaScript を使用して Windows 用にビルドされた @no__t 1 C#アプリのアプリケーションロジックを提供するためにで記述された Windows ランタイムコンポーネントを使用するなど、より高度なプログラミングシナリオでは、このような違いは IDE とドキュメントで明らかになります。 コンポーネントから JavaScript に @no__t 0 が返され、javascript デバッガーでそれを確認すると、JavaScript では Windows ランタイム型が使用されるため、`IMap<int, string>` のメソッドが表示されます。 よく使用されるコレクション型のうち、この 2 言語で表示が異なる型の一部を次の表に示します。

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

Windows ランタイムでは、`IMap<K, V>` と `IMapView<K, V>` は、`IKeyValuePair` を使用して反復処理されます。 これらをマネージド コードに渡すと、`IDictionary<TKey, TValue>` および `IReadOnlyDictionary<TKey, TValue>` として表示されるため、これを列挙するには必然的に `System.Collections.Generic.KeyValuePair<TKey, TValue>` を使用します。

インターフェイスがマネージド コード内に表示される方法によって、これらのインターフェイスを実装する型の表示方法が決まります。 たとえば、`PropertySet` クラスは `IMap<K, V>` を実装しますが、これはマネージド コードでは `IDictionary<TKey, TValue>` として表示されます。 `PropertySet` では、`IMap<K, V>` ではなく `IDictionary<TKey, TValue>` が実装されたように見えるため、マネージド コードでは .NET Framework ディクショナリの `Add` メソッドのように動作する `Add` メソッドがあるように表示されます。 `Insert` メソッドがないように見えます。

.NET Framework を使用して Windows ランタイムコンポーネントを作成する方法、および JavaScript でそのようなコンポーネントを使用する方法を示すチュートリアルについては、「 [」および「Visual Basic でのC# Windows ランタイムコンポーネントの作成](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)」を参照してください。

### <a name="primitive-types"></a>プリミティブ型

マネージコードで Windows ランタイムの自然な使用を有効にするために、コードでプリミティブ型 Windows ランタイムの代わりに .NET Framework プリミティブ型が表示されます。 .NET Framework では、`Int32` 構造体などのプリミティブ型には、`Int32.TryParse` メソッドなどの便利なプロパティとメソッドが多くあります。 これに対し、Windows ランタイムのプリミティブ型と構造体にはフィールドしかありません。 マネージド コードでプリミティブを使用すると、.NET Framework の型のように表示され、通常どおりに .NET Framework 型のプロパティとメソッドを使用できます。 要約すると、次のようになります。

- Windows ランタイムプリミティブ `Int32`、`Int64`、`Single`、`Double`、`Boolean`、`String` (Unicode 文字の変更できないコレクション)、`Enum`、`UInt32`、@no__t、および @no__t は、@no__t 10 名前空間で同じ名前の型を使用します。

- `UInt8` では、`System.Byte` を使用します。

- `Char16` では、`System.Char` を使用します。

- `IInspectable` インターフェイスでは、`System.Object` を使用します。

- `HRESULT` では、`System.Int32` のメンバーを 1 つ含む構造体を使用します。

インターフェイス型の場合と同様に、この表現の証拠が表示されるのは、.NET Framework プロジェクトが、JavaScript を使用してビルドされた @no__t 0 アプリによって使用される Windows ランタイムコンポーネントである場合のみです。

マネージコード内に同等の .NET Framework として表示されるその他の基本的な Windows ランタイム型には、<xref:System.DateTimeOffset?displayProperty=nameWithType> の構造としてマネージコードに表示される @no__t 0 の構造体、および <xref:System.TimeSpan?displayProperty=nameWithType> として表示される @no__t 2 の構造体が含まれます。データ.

### <a name="other-differences"></a>その他の相違点

場合によっては、.NET Framework 型が Windows ランタイム型ではなくコードに表示されるという事実は、ユーザー側での操作が必要になります。 たとえば、<xref:Windows.Foundation.Uri?displayProperty=nameWithType> クラスは .NET Framework コードで <xref:System.Uri?displayProperty=nameWithType> として表示されます。 <xref:System.Uri?displayProperty=nameWithType> は相対 URI を許可しますが、<xref:Windows.Foundation.Uri?displayProperty=nameWithType> には絶対 URI が必要です。 したがって、Windows ランタイムメソッドに URI を渡す場合は、絶対 URI であることを確認する必要があります。 「 [Windows ランタイムへの URI の引き渡し」を](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)参照してください。

<a name="WindowsRuntimeComponents"></a>

## <a name="scenarios-for-developing-windows-runtime-components"></a>Windows ランタイム コンポーネントの開発シナリオ

マネージ Windows ランタイムコンポーネントでサポートされるシナリオは、次の一般的な原則によって異なります。

- .NET Framework を使用して構築された Windows ランタイムコンポーネントには、他の Windows Runtimelibraries と明らかな違いはありません。 たとえば、マネージコードを使用してネイティブ Windows ランタイムコンポーネントを再実装した場合、2つのコンポーネントはと区別できません。 コンポーネントがマネージド コードで記述されているという事実は、そのコード自体がマネージド コードであったとしても、そのコンポーネントを使用するコードには表示されません。 ただし内部的には、そのコンポーネントは真のマネージド コードであり、共通言語ランタイム (CLR) 上で実行されます。

- コンポーネントには、アプリケーション ロジック、[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI コントロール、またはその両方を実装する型を含めることができます。

  > [!NOTE]
  > アプリケーション ロジックから UI 要素を分離することをお勧めします。 また、JavaScript や HTML を使用して Windows 用にビルドされた [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] アプリでは、[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI コントロールを使用できません。

- コンポーネントは、[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] アプリ用 Visual Studio ソリューション内のプロジェクトの場合もあれば、複数のソリューションに追加できる再利用可能なコンポーネントの場合もあります。

  > [!NOTE]
  > コンポーネントがまたは Visual Basic のみでC#使用される場合、Windows ランタイムコンポーネントにする必要はありません。 代わりに、通常の .NET Framework クラスライブラリにする場合は、パブリック API サーフェイスを Windows ランタイム型に制限する必要はありません。

- Windows ランタイム <xref:Windows.Foundation.Metadata.VersionAttribute> 属性を使用して、異なるバージョンで追加された型 (および型のメンバー) を識別することにより、再利用可能なコンポーネントのバージョンをリリースできます。

- コンポーネント内の型は Windows ランタイム型から派生できます。 コントロールは、@no__t 0 の名前空間のプリミティブコントロール型、または <xref:Windows.UI.Xaml.Controls.Button> などの完成したコントロールから派生できます。

  > [!IMPORTANT]
  > @No__t-0 および .NET Framework 4.5 以降では、マネージ Windows ランタイムコンポーネントのすべてのパブリック型がシールされている必要があります。 別の Windows ランタイムコンポーネントの型は、その型から派生することはできません。 コンポーネントでポリモーフィックな動作を提供するには、インターフェイスを作成し、そのインターフェイスをポリモーフィックな型に実装します。

- コンポーネント内のパブリック型のすべてのパラメーターと戻り値の型は Windows ランタイム型 (コンポーネントで定義されている Windows ランタイム型を含む) である必要があります。

次のセクションでは、一般的なシナリオの例を示します。

### <a name="application-logic-for-a-includewin8_appname_longincludeswin8-appname-long-mdmd-app-with-javascript"></a>JavaScript による [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] アプリ用アプリケーション ロジック

JavaScript を使用して Windows の [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] アプリを開発する場合、アプリケーション ロジックの一部が、他の部分に比べてマネージド コードでより適切に機能したり、開発が容易であったりすることがあります。 JavaScript では .NET Framework クラス ライブラリを直接使用できませんが、クラス ライブラリを .WinMD ファイルにすることができます。 このシナリオでは、Windows ランタイムコンポーネントはアプリの不可欠な部分であるため、バージョン属性を指定することは意味がありません。

### <a name="reusable-includewin8_appname_longincludeswin8-appname-long-mdmd-ui-controls"></a>再利用可能な [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI コントロール

一連の関連する UI コントロールを再利用可能な Windows ランタイムコンポーネントにパッケージ化できます。 コンポーネントは、単独で商品化することも、作成するアプリの要素として使用することもできます。 このシナリオでは、Windows ランタイム <xref:Windows.Foundation.Metadata.VersionAttribute> 属性を使用して互換性を向上させることが理にかなっています。

### <a name="reusable-application-logic-from-existing-net-framework-apps"></a>既存の .NET Framework アプリからの再利用可能なアプリケーション ロジック

既存のデスクトップアプリからマネージコードをスタンドアロンの Windows ランタイムコンポーネントとしてパッケージ化することができます。 これによって、C# または Visual Basic を使用してビルドされる [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] アプリに加えて、C++ または JavaScript を使用してビルドされる [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] アプリでも、コンポーネントを使用できるようになります。 コードに再利用シナリオが複数ある場合、バージョン管理はオプションです。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[Windows ストア アプリ用 .NET の概要](https://docs.microsoft.com/previous-versions/windows/apps/br230302(v=vs.140))|@No__t-0 アプリと Windows RuntimeComponents の作成に使用できる .NET Framework の型とメンバーについて説明します。 (Windows デベロッパー センター内)。|
|[または Visual Basic を使用しC#た Windows ストアアプリのためのロードマップ](https://docs.microsoft.com/previous-versions/windows/apps/br229583(v=win.10))|C# または Visual Basic を使用して [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] アプリの開発を開始するときに役立つ主要リソース (各種のクイック スタート トピック、ガイドライン、ベスト プラクティスなど) が用意されています (Windows デベロッパー センター内)。|
|[How to (XAML)](https://docs.microsoft.com/previous-versions/windows/apps/br229566(v=win.10))|C# または Visual Basic を使用して [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] アプリの開発を開始するときに役立つ主要リソース (各種のクイック スタート トピック、ガイドライン、ベスト プラクティスなど) が用意されています (Windows デベロッパー センター内)。|
|[C# および Visual Basic での Windows ランタイム コンポーネントの作成](/windows/uwp/winrt-components/creating-windows-runtime-components-in-csharp-and-visual-basic)|.NET Framework を使用して Windows ランタイムコンポーネントを作成する方法、JavaScript を使用して Windows 用にビルドされた @no__t 0 アプリの一部として使用する方法、および Visual Studio との組み合わせをデバッグする方法について説明します。 (Windows デベロッパー センター内)。|
|[Windows ランタイムリファレンス](/uwp/api/)|Windows ランタイムのリファレンスドキュメントです。 (Windows デベロッパー センター内)。|
|[Windows ランタイムへの URI の引き渡し](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)|マネージコードから Windows ランタイムに URI を渡すときに発生する可能性がある問題と、その回避方法について説明します。|
