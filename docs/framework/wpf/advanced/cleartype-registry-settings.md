---
title: ClearType レジストリの設定
ms.date: 03/30/2017
helpviewer_keywords:
- ClearType [WPF], registry settings
- typography [WPF], ClearType registry settings
ms.assetid: 56f314bb-b30b-4f67-8492-8b8a9fa432ae
ms.openlocfilehash: bedd99fcf9b4ca1d10b4c24d7cff9de320e6fd12
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186176"
---
# <a name="cleartype-registry-settings"></a>ClearType レジストリの設定
このトピックでは、WPF アプリケーションで使用される Microsoft ClearType のレジストリ設定の概要について説明します。  

<a name="overview"></a>
## <a name="technology-overview"></a>テクノロジの概要  
 ディスプレイ デバイスにテキストをレンダリングする [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでは、ClearType 機能を使用してレンダリング エクスペリエンスが拡張されます。 ClearType は、ラップトップや Pocket PC の画面、フラット パネル モニターなど、既存の LCD (液晶ディスプレイ) でのテキストの読みやすさを向上させるために Microsoft によって開発されたソフトウェア テクノロジです。 ClearType は、LCD 画面の各ピクセル内の個々の垂直カラー ストライプ要素にアクセスすることによって機能します。 ClearType の詳細については、「[ClearType の概要](cleartype-overview.md)」を参照してください。  
  
 ClearType でレンダリングされるテキストの表示は、表示先のディスプレイ デバイスによって大きく異なる場合があります。 たとえば、一般的な赤、緑、青 (RGB) の順ではなく青、緑、赤の順でカラー ストライプ要素を実装するモニターもわずかに存在します。  
  
 また、ClearType でレンダリングされるテキストの表示は、各個人の色の感度レベルによっても大きく異なる場合があります。 他の人よりも色のわずかな違いを見分ける能力に長けている人もいます。  
  
 それぞれの場合において、各個人が最も読みやすい表示を実現するために、ClearType 機能を変更する必要があります。  
  
<a name="registry_settings"></a>
## <a name="registry-settings"></a>レジストリ設定  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、ClearType の機能を制御するために、4 つのレジストリ設定が指定されています。  
  
|設定|説明|  
|-------------|-----------------|  
|ClearType レベル|ClearType の色の鮮明度を示します。|  
|ガンマ レベル|ディスプレイ デバイスのピクセル カラー コンポーネントのレベルを示します。|  
|ピクセル構造|ディスプレイ デバイスのピクセルの配置を示します。|  
|テキストのコントラスト レベル|表示されるテキストのコントラストのレベルを示します。|  
  
 これらの設定には、所定の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の ClearType レジストリ設定の参照方法を認識している外部構成ユーティリティを使用してアクセスできます。 これらの設定は、Windows レジストリ エディターを使用して値に直接アクセスして作成または変更することもできます。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ClearType レジストリ設定が設定されていない場合 (既定の状態)、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションは Windows のシステム パラメーター情報でフォント スムージングの設定を照会します。  
  
> [!NOTE]
> ディスプレイ デバイス名の列挙については、`SystemParametersInfo` Win32 関数を参照してください。  
  
<a name="ClearType_level"></a>
## <a name="cleartype-level"></a>ClearType レベル  
 ClearType レベルを設定すると、個人の色の感度および知覚に基づいてテキストのレンダリングを調整できます。 人によっては、最高レベルの ClearType を使用するテキストのレンダリングでは最も読みやすい表示が実現されない場合があります。  
  
 ClearType レベルは、0 から 100 の範囲の整数値です。 既定のレベルは 100 です。これは、ClearType でディスプレイ デバイスの最大限のカラー ストライプ要素が使用されることを意味します。 ただし、ClearType レベルが 0 の場合、テキストはグレースケールでレンダリングされます。 ClearType レベルを 0 から 100 の間に設定することで、個人の色の感度に適した中間レベルを実現できます。  
  
### <a name="registry-setting"></a>レジストリ設定  
 ClearType レベルのレジストリ設定は、特定のディスプレイ デバイス名に対応する個々のユーザー設定の場所にあります。  
  
 `HKEY_CURRENT_USER\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 ユーザーのディスプレイ デバイス名ごとに `ClearTypeLevel` の DWORD 値が定義されます。 次のスクリーンショットは、ClearType レベルのレジストリ エディターの設定を示しています。  
  
 ![レジストリ エディターでの ClearType の設定。](./media/cleartype-registry-settings/cleartype-settings-registry-editor.png)  
  
> [!NOTE]
> [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでは、ClearType を使用する場合と使用しない場合のいずれかのモードでテキストがレンダリングされます。 ClearType を使用しないテキストのレンダリングは、グレースケール レンダリングと呼ばれます。  
  
<a name="gamma_level"></a>
## <a name="gamma-level"></a>ガンマ レベル  
 ガンマ レベルとは、ピクセル値と輝度間の非線形リレーションシップのことです。 ガンマ レベル設定は、ディスプレイ デバイスの物理特性に対応する必要があります。対応していない場合、レンダリング出力にゆがみが発生する場合があります。 たとえば、テキストの表示が広すぎたり狭すぎたりする場合や、色縁がグリフの縦線の端に表示される場合などがあります。  
  
 ガンマ レベルは、1000 から 2200 の範囲の整数値です。 既定のレベルは 1900 です。  
  
### <a name="registry-setting"></a>レジストリ設定  
 ガンマ レベルのレジストリ設定は、特定のディスプレイ デバイス名に対応するローカル マシン設定の場所にあります。  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 ユーザーのディスプレイ デバイス名ごとに `GammaLevel` の DWORD 値が定義されます。 次のスクリーンショットは、ガンマ レベルのレジストリ エディターの設定を示しています。  
  
 ![レジストリ エディターでの ClearType のガンマ レベルの設定](./media/cleartype-registry-settings/cleartype-gamma-level-settings-registry-editor.png)  
  
<a name="pixel_structure"></a>
## <a name="pixel-structure"></a>ピクセル構造  
 ピクセル構造は、ディスプレイ デバイスを構成するピクセルの種類を示します。 ピクセル構造は、次の 3 種類のいずれかとして定義されます。  
  
|種類|[値]|説明|  
|----------|-----------|-----------------|  
|フラット|0|ディスプレイ デバイスにピクセル構造がありません。 つまり、各色の光源がピクセル領域に均等に拡散しています。これは、グレースケール レンダリングと呼ばれます。 標準のディスプレイ デバイスはこのようにして機能します。 ClearType はレンダリングされたテキストには適用されません。|  
|RGB|1|ディスプレイ デバイスのピクセルは、赤、緑、青の順の 3 つのストライプで構成されます。 ClearType はレンダリングされたテキストに適用されます。|  
|BGR|2|ディスプレイ デバイスのピクセルは、青、緑、赤の順の 3 つのストライプで構成されます。 ClearType はレンダリングされたテキストに適用されます。 順序が RGB の場合の逆であることに注目してください。|  
  
 ピクセル構造は、0 から 2 の範囲の整数値に対応します。 既定のレベルは 0 です。これは、フラット ピクセル構造を表します。  
  
> [!NOTE]
> ディスプレイ デバイス名の列挙については、`EnumDisplayDevices` Win32 関数を参照してください。  
  
### <a name="registry-setting"></a>レジストリ設定  
 ピクセル構造のレジストリ設定は、特定のディスプレイ デバイス名に対応するローカル マシン設定の場所にあります。  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Avalon.Graphics\<displayName>`  
  
 ユーザーのディスプレイ デバイス名ごとに `PixelStructure` の DWORD 値が定義されます。 次のスクリーンショットは、ピクセル構造のレジストリ エディターの設定を示しています。  
  
 ![レジストリ エディターでの ClearType のガンマ レベルの設定](./media/cleartype-registry-settings/cleartype-gamma-level-settings-registry-editor.png)  
  
<a name="text_contrast_level"></a>
## <a name="text-contrast-level"></a>テキストのコントラスト レベル  
 テキストのコントラスト レベルを設定すると、グリフの縦線の幅に基づいてテキストのレンダリングを調整できます。 テキストのコントラスト レベルは 0 から 6 の範囲の整数値です。整数値を大きくすると、縦線の幅が広くなります。 既定のレベルは 1 です。  
  
### <a name="registry-setting"></a>レジストリ設定  
 テキストのコントラスト レベルのレジストリ設定は、特定のディスプレイ デバイス名に対応する個々のユーザー設定の場所にあります。  
  
 `HKEY_CURRENT_USER\Software\Microsoft\Avalon.Graphics\<displayName>`  
  
 ユーザーのディスプレイ デバイス名ごとに `TextContrastLevel` の DWORD 値が定義されます。 次のスクリーンショットは、テキストのコントラスト レベルのレジストリ エディターの設定を示しています。  
  
 ![レジストリ エディターでの ClearType の設定。](./media/cleartype-registry-settings/cleartype-settings-registry-editor.png)  
  
## <a name="see-also"></a>関連項目

- [ClearType の概要](cleartype-overview.md)
- [ClearType アンチエイリアシング](/windows/desktop/gdi/cleartype-antialiasing)
