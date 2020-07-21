---
title: 弱いイベント パターン
ms.date: 03/30/2017
helpviewer_keywords:
- weak event pattern implementation [WPF]
- event handlers [WPF], weak event pattern
- IWeakEventListener interface [WPF]
ms.assetid: e7c62920-4812-4811-94d8-050a65c856f6
ms.openlocfilehash: 9f61a5a60b2ba1305158d1ab570079fe6aac19ac
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76870741"
---
# <a name="weak-event-patterns"></a>弱いイベント パターン
アプリケーションでは、イベント ソースにアタッチされているハンドラーが、ハンドラーをソースにアタッチしたリスナー オブジェクトと連携して破棄されない可能性があります。 このような状況では、メモリ リークが発生する可能性があります。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、この問題の解決に使用できる設計パターンを導入しており、特定のイベントには専用のマネージャー クラスを用意し、そのイベントのリスナーにインターフェイスを実装しています。 この設計パターンは、"*弱いイベント パターン*" 呼ばれます。  
  
## <a name="why-implement-the-weak-event-pattern"></a>弱いイベント パターンを実装するのはなぜですか  
 イベントをリッスンすると、メモリ リークが発生する可能性があります。 イベントをリッスンする一般的な手法は、ソース上のイベントにハンドラーをアタッチする言語固有の構文を使用することです。 たとえば、C# の場合、その構文は `source.SomeEvent += new SomeEventHandler(MyEventHandler)` です。  
  
 この手法では、イベント ソースからイベント リスナーへの強い参照が作成されます。 通常、リスナーのイベント ハンドラーをアタッチすると、リスナーのオブジェクトの有効期間はソースのオブジェクトの有効期間の影響を受けます (イベント ハンドラーが明示的に削除されていない場合)。 ただし、状況によっては、ソースの有効期間ではなく、他の要因でリスナーのオブジェクトの有効期間が制御される場合があります。たとえば、アプリケーションのビジュアル ツリーに現在属しているかどうかなどです。 ソース オブジェクトの有効期間がリスナーのオブジェクトの有効期間を超えている場合は常に、通常のイベント パターンでメモリ リークが発生します。つまり、リスナーは意図したよりも長く存続します。  
  
 弱いイベント パターンは、このメモリ リークの問題を解決するように設計されています。 リスナーをイベントに登録する必要がある場合は常に弱いイベント パターンを使用できますが、リスナー側では登録を解除する正確なタイミングを認識できません。 ソースのオブジェクトの有効期間がリスナーの有効なオブジェクトの有効期間を超える場合にも、弱いイベント パターンを使用できます (この場合、"*役に立つ*" かどうかは使う側の判断次第です)。弱いイベント パターンを使用すると、リスナーでは、リスナーのオブジェクトの有効期間特性に影響を与えることなく、イベントの登録と受信を行うことができます。 実際には、ソースからの暗黙の参照によって、リスナーがガベージ コレクションの対象かどうかが判断されることはありません。 この参照は弱い参照であるため、弱いイベント パターンと関連する API の名前が付けられます。 ガベージ コレクションまたはその他の方法でリスナーを破棄することができます。また、破棄されたオブジェクトに対する収集不可能なハンドラー参照を保持することなく、ソースを継続できます。  
  
## <a name="who-should-implement-the-weak-event-pattern"></a>弱いイベント パターンを実装する必要があるのはだれですか  
 弱いイベント パターンの実装に関心を持つのは、主にコントロールの作成者です。 コントロールの作成者は、コントロールの動作とコンテインメイトと、それが挿入されているアプリケーションに与える影響について主に責任を担っています。 これには、コントロール オブジェクトの有効期間動作、特にここで説明しているメモリ リークの問題の処理が含まれます。  
  
 弱いイベント パターンの適用に本質的に適しているシナリオがあります。 このようなシナリオの 1 つにデータ バインディングがあります。 データ バインディングでは、ソース オブジェクトが、バインディングのターゲットであるリスナー オブジェクトから完全に独立しているのが一般的です。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] データ バインディングの多くの側面には、イベントの実装方法に弱いイベント パターンが既に適用されています。  
  
## <a name="how-to-implement-the-weak-event-pattern"></a>弱いイベント パターンを実装する方法  
 弱いイベント パターンを実装するには、3 つの方法があります。 その 3 つの方法と、それぞれを使用すべき場合についてのガイダンスを次の表に示します。  
  
|方法|実装する場合|  
|--------------|-----------------------|  
|既存の弱いイベント マネージャー クラスを使用する|サブスクライブするイベントに対応する <xref:System.Windows.WeakEventManager> がある場合は、既存の弱いイベント マネージャーを使用します。 WPF に含まれている弱いイベント マネージャーの一覧については、<xref:System.Windows.WeakEventManager> クラスの継承階層を参照してください。 含まれている弱いイベント マネージャーは限られているため、おそらく他の方法のいずれかを選択する必要があります。|  
|ジェネリックの弱いイベント マネージャー クラスを使用する|既存の <xref:System.Windows.WeakEventManager> を使用できず、簡単な実装方法が必要で、効率については気にしない場合は、ジェネリック <xref:System.Windows.WeakEventManager%602> を使用します。 ジェネリック <xref:System.Windows.WeakEventManager%602> は、既存またはカスタムの弱いイベント マネージャーよりも非効率的です。 たとえば、ジェネリック クラスでは、イベントの名前を指定してイベントを検出するために、より多くのリフレクションを行います。 また、ジェネリック <xref:System.Windows.WeakEventManager%602> を使用してイベントを登録するコードは、既存またはカスタムの <xref:System.Windows.WeakEventManager> を使用するよりも詳細です。|  
|カスタムの弱いイベント マネージャー クラスを作成する|既存の <xref:System.Windows.WeakEventManager> を使用できず、最高の効率が必要な場合は、カスタムの <xref:System.Windows.WeakEventManager> を作成します。 カスタムの <xref:System.Windows.WeakEventManager> を使用してイベントをサブスクライブする方が効率的ですが、最初からコードを作成するコストが発生します。|  
|サードパーティの弱いイベント マネージャーを使用する|NuGet には[複数の弱いイベント マネージャー](https://www.nuget.org/packages?q=weak+event+manager&prerel=false)があり、多くの WPF フレームワークもそのパターンをサポートしています (たとえば、[疎結合イベント サブスクリプションに関する Prism のドキュメント](https://github.com/PrismLibrary/Prism-Documentation/blob/master/docs/wpf/legacy/Communication.md#subscribing-to-events)を参照してください)。|

 以下のセクションでは、弱いイベント パターンを実装する方法について説明します。  この説明のために、サブスクライブするイベントには次の特性があります。  
  
- イベント名は `SomeEvent` です。  
  
- イベントは `EventSource` クラスによって発生します。  
  
- イベント ハンドラーの型は `SomeEventEventHandler` (または `EventHandler<SomeEventEventArgs>`) です。  
  
- イベントからイベント ハンドラーに型 `SomeEventEventArgs` のパラメーターが渡されます。  
  
### <a name="using-an-existing-weak-event-manager-class"></a>既存の弱いイベント マネージャー クラスの使用  
  
1. 既存の弱いイベント マネージャーを見つけます。  
  
     WPF に含まれている弱いイベント マネージャーの一覧については、<xref:System.Windows.WeakEventManager> クラスの継承階層を参照してください。  
  
2. 通常のイベント フックアップではなく、新しい弱いイベント マネージャーを使用します。  
  
     たとえば、コードで次のパターンを使用してイベントをサブスクライブするとします。  
  
    ```csharp  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     次のパターンに変更します。  
  
    ```csharp  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     同様に、コードで次のパターンを使用してイベントのサブスクライブを解除するとします。  
  
    ```csharp  
    source.SomeEvent -= new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     次のパターンに変更します。  
  
    ```csharp  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
### <a name="using-the-generic-weak-event-manager-class"></a>ジェネリックの弱いイベント マネージャー クラスの使用  
  
1. 通常のイベント フックアップではなく、ジェネリック <xref:System.Windows.WeakEventManager%602> クラスを使用します。  
  
     <xref:System.Windows.WeakEventManager%602> を使用してイベント リスナーを登録する場合、次のコードに示すように、イベント ソースと <xref:System.EventArgs> 型を型パラメーターとしてクラスに指定し、<xref:System.Windows.WeakEventManager%602.AddHandler%2A> を呼び出します。  
  
    ```csharp  
    WeakEventManager<EventSource, SomeEventEventArgs>.AddHandler(source, "SomeEvent", source_SomeEvent);  
    ```  
  
### <a name="creating-a-custom-weak-event-manager-class"></a>カスタムの弱いイベント マネージャー クラスの作成  
  
1. 次のクラス テンプレートをプロジェクトにコピーします。  
  
     このクラスは、<xref:System.Windows.WeakEventManager> クラスから継承されます。  
  
     [!code-csharp[WeakEvents#WeakEventManagerTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/WeakEvents/CSharp/WeakEventManagerTemplate.cs#weakeventmanagertemplate)]  
  
2. `SomeEventWeakEventManager` の名前を実際の名前に置き換えます。  
  
3. 前述の 3 つの名前を、実際のイベントの対応する名前に置き換えます (`SomeEvent`、`EventSource`、および `SomeEventEventArgs`)。  
  
4. 弱いイベント マネージャー クラスの可視性 (public、internal、private) を、管理対象のイベントと同じ可視性に設定します。  
  
5. 通常のイベント フックアップではなく、新しい弱いイベント マネージャーを使用します。  
  
     たとえば、コードで次のパターンを使用してイベントをサブスクライブするとします。  
  
    ```csharp  
    source.SomeEvent += new SomeEventEventHandler(OnSomeEvent);  
    ```  
  
     次のパターンに変更します。  
  
    ```csharp  
    SomeEventWeakEventManager.AddHandler(source, OnSomeEvent);  
    ```  
  
     同様に、コードで次のパターンを使用してイベントのサブスクライブを解除するとします。  
  
    ```csharp  
    source.SomeEvent -= new SomeEventEventHandler(OnSome);  
    ```  
  
     次のパターンに変更します。  
  
    ```csharp  
    SomeEventWeakEventManager.RemoveHandler(source, OnSomeEvent);  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.WeakEventManager>
- <xref:System.Windows.IWeakEventListener>
- [ルーティング イベントの概要](routed-events-overview.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
