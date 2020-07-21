---
title: UI オートメーション プロバイダーの概要
ms.date: 03/30/2017
helpviewer_keywords:
- UI Automation, providers
- providers, UI Automation
ms.assetid: 859557b8-51e1-4d15-92e8-318d2dcdb2f7
ms.openlocfilehash: 1f780ffc37b0aff93a3358c1980d271fe10c1321
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179886"
---
# <a name="ui-automation-providers-overview"></a>UI オートメーション プロバイダーの概要
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 UI オートメーション プロバイダーを使用すれば、コントロールで UI オートメーション クライアント アプリケーションと通信することができます。 一般に、各コントロールまたは [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] 内のその他の要素はプロバイダーによって表現されます。 プロバイダーは、要素に関する情報を公開し、必要に応じて、クライアント アプリケーションがコントロールと対話できるようにするコントロール パターンを実装します。  
  
 通常、クライアント アプリケーションはプロバイダーと直接連動する必要はありません。 Win32、Windows フォーム、または[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]フレームワークを使用するアプリケーションの標準コントロールのほとんどは、自動的にシステムに[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]公開されます。 カスタム コントロールを実装するアプリケーションがそれらのコントロール用の [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] プロバイダーを実装することもできます。クライアント アプリケーションがそれらにアクセスするために特別な手順を実行する必要はありません。  
  
 このトピックでは、特に Windows フォーム[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]ウィンドウおよび Win32 ウィンドウのコントロールに対して、コントロール開発者がプロバイダーを実装する方法の概要を示します。  
  
<a name="Types_of_Providers"></a>
## <a name="types-of-providers"></a>プロバイダーの種類  
 UI オートメーション プロバイダーは、クライアント側プロバイダーとサーバー側プロバイダーの 2 つのカテゴリに分類されます。  
  
### <a name="client-side-providers"></a>クライアント側プロバイダー  
 クライアント側プロバイダーは、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]をサポートしていないか部分的にサポートしているアプリケーションと通信する UI オートメーション クライアントによって実装されます。 クライアント側のプロバイダは、通常、Windows メッセージを送受信することによって、プロセス境界を越えてサーバーと通信します。  
  
 Win32、Windows フォーム、または[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]アプリケーションのコントロール用の UI オートメーション プロバイダはオペレーティング システムの一部として提供されるため、クライアント アプリケーションが独自のプロバイダを実装する必要はめったにないので、この概要では、それらについては詳しく説明していません。  
  
### <a name="server-side-providers"></a>サーバー側プロバイダー  
 サーバー側プロバイダーは、カスタム コントロール、または Win32、Windows フォーム、または[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]以外の UI フレームワークに基づくアプリケーションによって実装されます。  
  
 また、サーバー側プロバイダーは、サーバーからクライアントに要求するインターフェイスを [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] コア システムに公開することにより、プロセス境界を越えてクライアント アプリケーションと通信します。  
  
<a name="AutomationProviderConcepts"></a>
## <a name="ui-automation-provider-concepts"></a>UI オートメーション プロバイダーの概念  
 ここでは、UI オートメーション プロバイダーを実装するために理解しておく必要があるいくつかの重要な概念について簡単に説明します。  
  
### <a name="elements"></a>要素  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 要素は、UI オートメーション クライアントからアクセス可能な [!INCLUDE[TLA#tla_ui](../../../includes/tlasharptla-ui-md.md)] の一部です。 例として、アプリケーション ウィンドウ、ペイン、ボタン、ツールヒント、リスト ボックス、およびリスト項目が含まれています。  
  
### <a name="navigation"></a>「ナビゲーション」  
 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 要素は、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーとしてクライアントに公開されます。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] は、要素間を移動することによって、ツリーを構成します。 ナビゲーションは、親、兄弟、または子を指す要素ごとに、プロバイダーによって有効にされます。  
  
 ツリーのクライアント ビューの詳細については、「 UI[オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]  
  
### <a name="views"></a>ビュー  
 次の表に示すように、クライアントは 3 つのプリンシパル ビューで [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] ツリーを表示できます。  
  
|||  
|-|-|  
|列ビュー|すべての要素が含まれます。|  
|コントロール ビュー|コントロールである要素が含まれます。|  
|コンテンツ ビュー|コンテンツである要素が含まれます。|  
  
 ツリーのクライアント ビューの詳細については[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]、「 [UI オートメーション ツリーの概要](ui-automation-tree-overview.md)」を参照してください。  
  
 コンテンツ要素またはコントロール要素としての要素の定義はプロバイダー実装で行う必要があります。 コントロール要素はコンテンツ要素であることもないこともありますが、コンテンツ要素はすべてコントロール要素です。  
  
### <a name="frameworks"></a>フレームワーク  
 フレームワークは、画面のある領域で子コントロール、ヒット テスト、およびレンダリングを管理するコンポーネントです。 たとえば、HWND と呼ばれる Win32 ウィンドウは、メニュー バー、ステータス バー、ボタン[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]などの複数の要素を含むフレームワークとして機能します。  
  
 リスト ボックスやツリー ビューなどの Win32 コンテナー コントロールには、子項目をレンダリングしてヒット テストを実行するための独自のコードが含まれているため、フレームワークと見なされます。 これに対して、 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] リスト ボックスは、包含する [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] ウィンドウによってレンダリングやヒット テストが処理されるため、フレームワークではありません。  
  
 アプリケーション内の [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] はさまざまなフレームワークで構成することができます。 たとえば、HWND アプリケーション ウィンドウには、HWND のコンボ ボックスなどのコンポーネントを含むダイナミック HTML (DHTML) が含まれている場合があります。  
  
### <a name="fragments"></a>fragments  
 フラグメントは、特定のフレームワーク内の要素のサブツリー全体です。 サブツリーのルート ノードにある要素はフラグメント ルートと呼ばれます。 フラグメント ルートには親はありませんが、他のフレームワーク (通常は Win32 ウィンドウ (HWND) 内でホストされます。  
  
### <a name="hosts"></a>Hosts  
 すべてのフラグメントのルート ノードは、要素 (通常は Win32 ウィンドウ (HWND) でホストされている必要があります。 例外は、他の要素でホストされないデスクトップです。 カスタム コントロールのホストは、アプリケーション ウィンドウやトップ レベル コントロールのグループを含めることができるその他のウィンドウではなく、コントロール自体の HWND です。  
  
 フラグメントのホストは、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] サービスを提供するうえで重要な役割を果たします。 このホストがフラグメント ルートへの移動を可能にし、いくつかの既定のプロパティを提供するため、カスタム プロバイダーはそれらを実装する必要がありません。  
  
## <a name="see-also"></a>関連項目

- [サーバー側 UI オートメーション プロバイダーの実装](server-side-ui-automation-provider-implementation.md)
