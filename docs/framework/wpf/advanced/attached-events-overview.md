---
title: 添付イベントの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- handling attached events [WPF]
- defining attached events as routed events [WPF]
- attached events [WPF], scenarios for
- attached events vs. routed events [WPF]
- backing attached events with routed events [WPF]
- attached events [WPF], definition
ms.assetid: 2c40eae3-80e4-4a45-ae09-df6c9ab4d91e
ms.openlocfilehash: e125c9a57090049f4319da96c7004f06606d0147
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141563"
---
# <a name="attached-events-overview"></a>添付イベントの概要

Extensible Application Markup Language (XAML) は言語コンポーネントと "*添付イベント*" と呼ばれている種類のイベントを定義します。 添付イベントという概念を利用すると、イベントを実際に定義または継承する要素にではなく、任意の要素に特定のイベントのハンドラーを追加できます。 この場合、イベントを発生させる可能性があるオブジェクトとターゲット処理インスタンスのいずれもイベントを定義せず、"所有" しません。  

<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックは、「[ルーティング イベントの概要](routed-events-overview.md)」と「[XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)」を既に読んでいることを前提としています。  
  
<a name="Syntax"></a>
## <a name="attached-event-syntax"></a>添付イベントの構文  
 添付イベントには XAML 構文とコーディング パターンが含まれています。コーディング パターンは、添付イベントの使用をサポートする目的でバッキング コードで使用する必要があります。  
  
 XAML 構文では、添付イベントはそのイベント名だけでなく、その所有タイプとイベント名により指定されます。所有タイプとイベント名はドット (.) で区切られます。 イベント名はその所有タイプにより修飾されるため、添付イベントの構文では、インスタンス化できるあらゆる要素に添付イベントを添付できます。  
  
 たとえば、カスタム `NeedsCleaning` 添付イベントのハンドラーを添付する XAML 構文は次のようになります。  
  
 [!code-xaml[WPFAquariumSln#AE](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquarium/Window1.xaml#ae)]  
  
 `aqua:` 接頭辞に注意してください。この場合は、マッピングされたカスタム xmlns から来ているカスタム イベントが添付イベントであるため、この接頭辞が必要になります。  
  
<a name="WPFImplements"></a>
## <a name="how-wpf-implements-attached-events"></a>WPF で添付イベントを実装する方法

WPF では、添付イベントは <xref:System.Windows.RoutedEvent> フィールドによりサポートされ、発生後、ツリー経由でルーティングされます。 通常、添付イベントの発生源 (イベントを発生させたオブジェクト) はシステムまたはサービス ソースです。そのため、イベントを発生させるコードを実行するオブジェクトは要素ツリーの直接的一部ではありません。  
  
<a name="Scenarios"></a>
## <a name="scenarios-for-attached-events"></a>添付イベントのシナリオ  
 WPF では、添付イベントは、サービス レベルの抽象化が存在する特定の機能領域に存在します。たとえば、静的な <xref:System.Windows.Input.Mouse> クラスまたは <xref:System.Windows.Controls.Validation> クラスにより有効化されたイベントに対するサービス レベルの抽象化です。 サービスと連動する、またはサービスを利用するクラスは、添付イベント構文のイベントを利用するか、クラスによるサービスの機能統合に含まれるルーティング イベントとして添付イベントを添付できます。  
  
 WPF は添付イベントの数を定義しますが、添付イベントを直接使用または処理するシナリオは非常に限られています。 一般的には、添付イベントはアーキテクチャ目的にサービスを提供しますが、その後、非添付の (CLR イベント "ラッパー" でサポートされる) ルーティング イベントに転送されます。  
  
 たとえば、基になる添付イベント <xref:System.Windows.Input.Mouse.MouseDown?displayProperty=nameWithType> を特定の <xref:System.Windows.UIElement> でより簡単に処理するには、添付イベント構文を XAML またはコードで使用するのではなく、その <xref:System.Windows.UIElement> で <xref:System.Windows.UIElement.MouseDown> を使用します。 添付イベントは、入力機器の将来の拡張を可能にするため、アーキテクチャにおける目的にサービスを提供します。 想定される機器では、マウスの入力をシミュレートするために、<xref:System.Windows.Input.Mouse.MouseDown?displayProperty=nameWithType> を発生させることのみが必要となります。その目的で <xref:System.Windows.Input.Mouse> から派生させる必要はありません。 ただし、このシナリオでは、イベントのコードが処理されます。添付イベントの XAML 処理はこのシナリオには関係しません。  
  
<a name="Handling"></a>
## <a name="handling-an-attached-event-in-wpf"></a>WPF で添付イベントを処理する  
 添付イベントと記述するハンドラー コードを処理するプロセスは基本的にルーティング イベントの場合と同じです。  
  
 一般的には、WPF 添付イベントは WPF ルーティング イベントとそれほど異なっているわけではありません。 違いは、イベントの発生源とメンバーとしてクラスにより公開される方法 (これは XAML ハンドラー構文にも影響を与えます) です。  
  
 ただし、前述のように、既存の WPF 添付イベントは WPF での取り扱いを特に意図しているわけではありません。 多くの場合、このイベントの目的は、合成中、合成された要素が親要素に状態を報告できるようにすることです。合成においては、イベントは通常、コードで発生します。また、関連する親クラスにおいて、クラスの処理に依存します。 たとえば、<xref:System.Windows.Controls.Primitives.Selector> 内の項目は添付 <xref:System.Windows.Controls.Primitives.Selector.Selected> イベントを発生させることが予想されます。このイベントは、<xref:System.Windows.Controls.Primitives.Selector> クラスにより処理されるクラスであり、可能性として <xref:System.Windows.Controls.Primitives.Selector> クラスにより別のルーティング イベント <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> に変換されます。 ルーティング イベントとクラス処理については、「[ルーティング イベントの処理済みとしてのマーキング、およびクラス処理](marking-routed-events-as-handled-and-class-handling.md)」を参照してください。  
  
<a name="Custom"></a>
## <a name="defining-your-own-attached-events-as-routed-events"></a>独自の添付イベントをルーティング イベントとして定義する  
 共通の WPF 基底クラスから派生させる場合、独自の添付イベントを実装できます。クラスに特定のパターン メソッドを追加し、基底クラスに既に存在するユーティリティ メソッドを使用します。  
  
 パターンは次のとおりです。  
  
- メソッド __Add*EventName*Handler__ と 2 つのパラメーター。 最初のパラメーターは、イベント ハンドラーが追加されるインスタンスです。 2 番目のパラメーターは追加するイベント ハンドラーです。 メソッドには `public` と `static` を指定する必要があります。戻り値はありません。  
  
- メソッド __Remove*EventName*Handler__ と 2 つのパラメーター。 最初のパラメーターは、イベント ハンドラーが削除されるインスタンスです。 2 番目のパラメーターは削除するイベント ハンドラーです。 メソッドには `public` と `static` を指定する必要があります。戻り値はありません。  
  
 __Add*EventName*Handler__ アクセサー メソッドは、添付イベント ハンドラーの属性が要素で宣言されているとき、XAML 処理を容易にします。 __Add*EventName*Handler__ メソッドと __Remove*EventName*Handler__ メソッドはまた、添付イベントのイベント ハンドラー ストアへのコード アクセスを可能にします。  
  
 この一般的パターンには、フレームワークの実用的実装のための十分な精度がありません。サポートする言語とアーキテクチャで基礎イベントを識別する方法に関して、特定の XAML リーダー実装で異なるスキームが与えられる可能性があるためです。 そのような理由から、WPF は添付イベントをルーティング イベントとして実装します。イベント (<xref:System.Windows.RoutedEvent>) に使用する識別子が WPF イベント システムによって既に定義されています。 また、イベントのルーティングは、添付イベントの XAML 言語レベル概念で自然な実装です。  
  
 WPF 添付イベントの __Add*EventName*Handler__ 実装は、ルーティング イベントとハンドラーを引数として <xref:System.Windows.UIElement.AddHandler%2A> を呼び出すことで行われます。  
  
 この実装方法と一般的なルーティング イベント システムでは、添付イベントの処理が <xref:System.Windows.UIElement> 派生クラスまたは <xref:System.Windows.ContentElement> 派生クラスに制限されます。これらのクラスだけに <xref:System.Windows.UIElement.AddHandler%2A> 実装が与えられるためです。  
  
 たとえば、次のコードでは、添付イベントをルーティング イベントとして宣言する WPF 添付イベント方法を利用し、所有者クラス `Aquarium` で `NeedsCleaning` 添付イベントが定義されます。  
  
 [!code-csharp[WPFAquariumSln#AECode](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#aecode)]
 [!code-vb[WPFAquariumSln#AECode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#aecode)]  
  
 添付イベント識別子フィールド <xref:System.Windows.EventManager.RegisterRoutedEvent%2A> を設定するメソッドは、実際、非添付のルーティング イベントを登録するためのメソッドと同じです。 添付イベントとルーティング イベントはすべて、集中管理されている内部ストアに登録されます。 このイベント ストア実装により "インターフェイスとしてのイベント" という概念が可能になります。この概念に関する説明は「[ルーティング イベントの概要](routed-events-overview.md)」にあります。  
  
<a name="Raising"></a>
## <a name="raising-a-wpf-attached-event"></a>WPF 添付イベントを発生させる  
 通常、WPF 定義の既存の添付イベントはコードから発生させる必要がありません。 これらのイベントは一般的な "サービス" 概念モデルに従います。<xref:System.Windows.Input.InputManager> のようなサービス クラスがイベントの生成を担当します。  
  
 ただし、添付イベントの基礎を <xref:System.Windows.RoutedEvent> とする WPF モデルを基盤にカスタムの添付イベントを定義する場合、<xref:System.Windows.UIElement.RaiseEvent%2A> を利用し、任意の <xref:System.Windows.UIElement> または <xref:System.Windows.ContentElement> から添付イベントを発生させることができます。 ルーティング イベント (添付または非添付) を発生させるには、イベント ソースとして要素ツリーで特定の要素を宣言する必要があります。そのソースは <xref:System.Windows.UIElement.RaiseEvent%2A> 呼び出し元として報告されます。 ツリーのソースとして報告される要素を決定することはサービスの担当です。  
  
## <a name="see-also"></a>関連項目

- [ルーティング イベントの概要](routed-events-overview.md)
- [XAML 構文の詳細](xaml-syntax-in-detail.md)
- [WPF における XAML とカスタム クラス](xaml-and-custom-classes-for-wpf.md)
