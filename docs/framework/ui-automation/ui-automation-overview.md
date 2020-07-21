---
title: UI オートメーションの概要
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, overview
- user interface, see UI
- accessibility, UI automation
ms.assetid: 65847654-9994-4a9e-b36d-2dd5d998770b
ms.openlocfilehash: 6f938302967e1b519105769717d326e5042a7bce
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179918"
---
# <a name="ui-automation-overview"></a>UI オートメーションの概要
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]は、をサポート[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]するすべてのオペレーティング システムで使用できる、Microsoft Windows の新しいアクセシビリティ フレームワークです。  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] は、デスクトップ上のほとんどの [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 要素へのプログラムによるアクセスを提供し、スクリーン リーダーなどの補助技術製品が [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] に関する情報をエンド ユーザーに提供したり、標準入力方式以外の方法で [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] を操作したりできるようにします。 また、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] は、自動テスト スクリプトが [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]と対話できるようにします。  
  
> [!NOTE]
> [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] では、 **[別のユーザーとして実行]** コマンドを使用して別々のユーザーが開始したプロセス間の通信を行うことはできません。  
  
 UI オートメーション クライアント アプリケーションを作成すると、そのアプリケーションは、複数のフレームワーク上で動作することが保証されます。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コアは、 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]のさまざまな部分の基になるフレームワークのあらゆる差異をマスクします。 たとえば`Content`、[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]ボタンのプロパティ、Win32`Caption`ボタンのプロパティ、および HTML イメージの`ALT`プロパティは、<xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.Name%2A>ビュー内の[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]1 つのプロパティにマップされます。  
  
UI オートメーションは、.NET Framework を実行しているサポートされている Windows オペレーティング システムですべての機能を提供します[(.NET Framework のシステム要件](../get-started/system-requirements.md)または .NET Core のバージョンを参照してください.  
  
 UI オートメーション プロバイダーは、組み込みのブリッジ ング サービスを通じて Microsoft アクティブ ユーザー補助クライアント アプリケーションのいくつかのサポートを提供します。  
  
<a name="Providers_and_Clients"></a>
## <a name="providers-and-clients"></a>プロバイダーおよびクライアント  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] には、次の表に示す 4 つの主要なコンポーネントがあります。  
  
|コンポーネント|説明|  
|---------------|-----------------|  
|プロバイダー API (UI オートメーション プロバイダー.dll と UI オートメーションタイプ.dll)|UI オートメーション プロバイダーによって実装されるインターフェイス定義のセット。 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 要素に関する情報を提供し、プログラムによる入力に応答するオブジェクトです。|  
|クライアント API (UIAutomationClient.dll および UIAutomationTypes.dll)|UI オートメーション クライアント アプリケーションが、 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] に関する情報を取得し、コントロールに入力を送信することを可能にする、各種マネージド コードのセット。|  
|UiAutomationCore.dll|プロバイダーとクライアントの間の通信を処理する、基になるコード ( [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コアとも呼ばれます)。|  
|UIAutomationClientsideProviders.dll|従来の標準コントロールに使用する UI オートメーション プロバイダーのセット。 ([!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]コントロールには[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].このサポートは、クライアント アプリケーションで自動的に利用できます。|  
  
 ソフトウェア開発者の観点からは、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]を使用するには、カスタム コントロール用のサポートを作成する (プロバイダー API を使用) か、または [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コアを使用して [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 要素と通信するアプリケーションを作成する (クライアント API を使用)、という 2 つの方法があります。 主要な目的に応じて、ドキュメントの該当箇所を参照してください。 次の各セクションでは、概念の詳細と、実際的な方法について説明します。  
  
|Section|主題|対象ユーザー|  
|-------------|--------------------|--------------|  
|[UI オートメーションの基礎](index.md)(このセクション)|概念についての広範な概要。|すべて。|  
|[マネージド コードの UI オートメーション プロバイダー](ui-automation-providers-for-managed-code.md)|プロバイダー API を使用する際に役立つ概要と「方法」トピック。|コントロールの開発者。|  
|[マネージド コードの UI オートメーション クライアント](ui-automation-clients-for-managed-code.md)|クライアント API を使用する際に役立つ概要と「方法」トピック。|クライアント アプリケーションの開発者。|  
|[UI オートメーション コントロール パターン](ui-automation-control-patterns.md)|コントロール パターンをプロバイダーで実装する方法と、クライアントで使用可能な機能に関する情報。|すべて。|  
|[UI オートメーション テキスト パターン](ui-automation-text-pattern.md)|Text コントロール パターンをプロバイダーで実装する方法と、クライアントで使用可能な機能に関する情報。|すべて。|  
|[UI オートメーション コントロール型](ui-automation-control-types.md)|さまざまなコントロール型でサポートされるプロパティとコントロール パターンに関する情報。|すべて。|  
  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] の名前空間、それらの名前空間を含む DLL、およびそれらを使用する対象ユーザーを次の表に示します。  
  
|名前空間|参照される DLL|対象ユーザー|  
|---------------|---------------------|--------------|  
|<xref:System.Windows.Automation>|UIAutomationClientUIAutomationTypes|UI オートメーション クライアントの開発者。 <xref:System.Windows.Automation.AutomationElement> オブジェクトの検索、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントの登録、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のコントロール パターンの利用の際に使用します。|  
|<xref:System.Windows.Automation.Provider>|UIAutomationProviderUIAutomationTypes|[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]以外のフレームワークの UI オートメーション プロバイダーの開発者。|  
|<xref:System.Windows.Automation.Text>|UIAutomationClientUIAutomationTypes|[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]以外のフレームワークで使用する UI オートメーション プロバイダーの開発者が、TextPattern コントロール パターンを実装する際に使用します。|  
|<xref:System.Windows.Automation.Peers>|PresentationFramework|[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]で使用する UI オートメーション プロバイダーの開発者。|  
  
<a name="UI_Automation_Model"></a>
## <a name="ui-automation-model"></a>UI オートメーション モデル  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] は、 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] のすべての部分を、クライアント アプリケーションに対して、 <xref:System.Windows.Automation.AutomationElement>として公開します。 各要素は、デスクトップをルート要素とするツリー構造に格納されます。 クライアントでは、ツリーの未加工ビューを、コントロール ビューまたはコンテンツ ビューとしてフィルター処理できます。 アプリケーションでは、カスタム ビューを作成することもできます。  
  
 <xref:System.Windows.Automation.AutomationElement> オブジェクトは、それらが表す [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 要素の一般的なプロパティを公開します。 これらのプロパティの 1 つにコントロール型があります。これは、その基本的な外観と機能を認識可能な単一のエンティティとして定義するもので、ボタンやチェック ボックスなどがその例です。  
  
 また、各要素は、そのコントロール型に固有のプロパティを提供するコントロール パターンも公開します。 コントロール パターンは、クライアントが要素に関するより詳細な情報を取得し、入力を提供できるようにするメソッドも公開します。  
  
> [!NOTE]
> コントロール型とコントロール パターンの間には、1 対 1 の対応はありせん。 1 つのコントロール パターンが複数のコントロール型でサポートされる場合もありますし、1 つのコントロールが複数のコントロール パターンをサポートし、各パターンがそのコントロールの動作の異なる側面を公開する場合もあります。 たとえば、1 つのコンボ ボックスは、少なくとも 2 つのコントロール パターンを持ちます。1 つは、それを展開して折りたたむ機能を表し、もう 1 つは、選択機構を表します。 詳しくは、「 [UI Automation Control Types](ui-automation-control-types.md)」をご覧ください。  
  
 また、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] は、クライアント アプリケーションにイベントを通じて情報を提供します。 WinEvents と[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は異なり、イベントはブロードキャスト メカニズムに基づいていません。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] のクライアントは、特定のイベント通知を登録し、特定の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロパティとコントロール パターン情報を自身のイベント ハンドラーに渡すように要求することができます。 また、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] イベントには、原因となった要素への参照が含まれています。 プロバイダーはイベントを選択的に発生させることによってパフォーマンスを向上させることができますが、クライアントがリッスンしているかどうかによって異なります  
  
## <a name="see-also"></a>関連項目

- [UI Automation Tree Overview](ui-automation-tree-overview.md)
- [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)
- [UI オートメーション プロパティの概要](ui-automation-properties-overview.md)
- [UI オートメーション イベントの概要](ui-automation-events-overview.md)
- [UI オートメーションのセキュリティの概要](ui-automation-security-overview.md)
