---
title: UI オートメーションおよび画面の拡大縮小
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- scaling, screens
- screens, scaling
- UI (user interface), automation
- UI Automation
ms.assetid: 4380cad7-e509-448f-b9a5-6de042605fd4
ms.openlocfilehash: 2a68a74fa6aadcaba21f142d394a1f8a3d8af371
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179976"
---
# <a name="ui-automation-and-screen-scaling"></a>UI オートメーションおよび画面の拡大縮小
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
Windows Vista 以降では、ユーザーは、画面のほとんどのユーザー インターフェイス (UI) 要素が大きく表示されるように、1 インチあたりのドット (dpi) の設定を変更できます。 この機能は Windows で長い間使用されていましたが、以前のバージョンではスケーリングをアプリケーションで実装する必要がありました。 Windows Vista 以降、デスクトップ ウィンドウ マネージャーは、独自のスケーリングを処理しないすべてのアプリケーションに対して既定のスケーリングを実行します。 UI オートメーション クライアント アプリケーションでは、この機能を考慮に入れる必要があります。  
  
<a name="Scaling_in_Windows_Vista"></a>
## <a name="scaling-in-windows-vista"></a>Windows Vista での拡大縮小  
 デフォルトの dpi 設定は 96 で、96 ピクセルが 1 インチの幅または高さを占めています。 「インチ」の正確な寸法は、モニターのサイズと物理的な解像度によって異なります。 たとえば、幅 12 インチで水平方向の解像度 1280 ピクセルのモニターでは、96 ピクセルの水平線は 1 インチの約 9/10 の長さになります。  
  
 dpi 設定を変更することは、画面解像度を変更するのと同じではありません。 dpi スケーリングでは、画面上の物理ピクセル数は変わりません。 拡大縮小が適用されるのは、 [!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)] 要素のサイズと位置です。 拡大縮小しないよう明示的に指定されていないデスクトップとアプリケーションに対し、デスクトップ ウィンドウ マネージャー (DWM) はこの拡大縮小を自動的に実行できます。  
  
 実際には、ユーザーがスケール ファクターを 120 dpi に設定すると、画面上の縦または横のインチが 25% 大きくなります。 すべての寸法は、それに応じて拡大されます。 画面の左上隅からのアプリケーション ウィンドウのオフセットは、25% 増加します。 アプリケーションのスケーリングが有効で、アプリケーションが dpi 対応でない場合、ウィンドウのサイズは、ウィンドウに含まれるすべての[!INCLUDE[TLA2#tla_ui](../../../includes/tla2sharptla-ui-md.md)]要素のオフセットとサイズと共に同じ比率で増加します。  
  
> [!NOTE]
> デフォルトでは、DPI を認識しないアプリケーションのスケーリングは、ユーザーが dpi を 120 に設定した場合にはスケーリングを実行しませんが、dpi がカスタム値 144 以上に設定されている場合はスケーリングを実行します。 ただし、この既定の動作は、ユーザーがオーバーライドできます。  
  
 画面の拡大縮小は、画面座標に何らかの関わりを持つアプリケーションに新しい課題をもたらします。 現在、画面には物理座標と論理座標という 2 つの座標系が含まれています。 あるポイントの物理座標は、原点の左上からの実際のオフセット (ピクセル数) です。 論理座標は、ピクセル自体が拡大縮小された場合のオフセットです。  
  
 たとえば、ダイアログ ボックスを設計し、座標 (100, 48) にボタンを配置するとします。 このダイアログ ボックスが既定の 96 dpi に表示されている場合、ボタンは物理座標 (100, 48) にあります。 120dpiでは、(125,60)の物理的座標に位置する。 しかし、論理座標は任意のdpi設定で同じです:(100、48)。  
  
 論理座標は、dpi 設定に関係なく、オペレーティング システムとアプリケーションの動作を一貫させるため、重要です。 たとえば、 <xref:System.Windows.Forms.Cursor.Position%2A?displayProperty=nameWithType> は通常、論理座標を返します。 ダイアログ ボックス内の要素の上にカーソルを移動すると、dpi 設定に関係なく同じ座標が返されます。 (100, 100) でコントロールを描画すると、そのコントロールは、それらの論理座標に描画され、任意の dpi 設定で同じ相対位置を占めます。  
  
<a name="Scaling_in_UI_Automation_Clients"></a>
## <a name="scaling-in-ui-automation-clients"></a>UI オートメーション クライアントにおける拡大縮小  
 API[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]は論理座標を使用しません。 次のメソッドとプロパティが返す、あるいはパラメーターとして受け取るのは、物理座標です。  
  
- <xref:System.Windows.Automation.AutomationElement.GetClickablePoint%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.TryGetClickablePoint%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.ClickablePointProperty>  
  
- <xref:System.Windows.Automation.AutomationElement.FromPoint%2A>  
  
- <xref:System.Windows.Automation.AutomationElement.AutomationElementInformation.BoundingRectangle%2A>  
  
 既定では、96- dpi 以外の環境で実行されている UI オートメーション クライアント アプリケーションは、これらのメソッドとプロパティから正しい結果を取得できません。 たとえば、カーソルの位置は論理座標で表されるため、クライアントはそのカーソルの位置にある要素を取得するために、これらの座標をそのまま <xref:System.Windows.Automation.AutomationElement.FromPoint%2A> に渡すことができません。 さらに、アプリケーションはクライアント領域外にウィンドウを正しく配置することもできません。  
  
 解決方法は 2 つの部分で構成されます。  
  
1. 最初に、クライアント アプリケーションを dpi 対応にします。 これを行うには、起動時に Win32`SetProcessDPIAware`関数を呼び出します。 マネージド コードで、次の宣言によりこの関数を使用できるようになります。  
  
     [!code-csharp[Highlighter#101](../../../samples/snippets/csharp/VS_Snippets_Wpf/Highlighter/CSharp/NativeMethods.cs#101)]
     [!code-vb[Highlighter#101](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/Highlighter/VisualBasic/NativeMethods.vb#101)]  
  
     この関数は、プロセス全体を dpi 認識にします。 [たとえば、ハイライト表示のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/Highlighter)では、ハイライトの四角形を構成する 4 つのウィンドウは、論理座標ではなく、UI オートメーションから取得した物理座標に配置されます。 サンプルが dpi 対応でない場合、ハイライトはデスクトップ上の論理座標で描画され、非 96- dpi 環境での配置が正しく行われなくなる可能性があります。  
  
2. カーソルの座標を取得するには、Win32`GetPhysicalCursorPos`関数を呼び出します。 次の例に、この関数を宣言して使用する方法を示します。  
  
     [!code-csharp[UIAClient_snip#185](../../../samples/snippets/csharp/VS_Snippets_Wpf/UIAClient_snip/CSharp/ClientForm.cs#185)]
     [!code-vb[UIAClient_snip#185](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UIAClient_snip/VisualBasic/ClientForm.vb#185)]  
  
> [!CAUTION]
> <xref:System.Windows.Forms.Cursor.Position%2A?displayProperty=nameWithType> は使用しないでください。 拡大縮小される環境において、クライアント ウィンドウ外でのこのプロパティの動作は定義されていません。  
  
 dpi 対応ではないアプリケーションとの直接のクロスプロセス通信をアプリケーションで実行する場合は、Win32 関数`PhysicalToLogicalPoint`と`LogicalToPhysicalPoint`.  
  
## <a name="see-also"></a>関連項目

- [Highlighter Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/Highlighter)
