---
ms.openlocfilehash: f78d15338aa49de5b729aca12964924a0df00ec6
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614835"
---
### <a name="improved-accessibility-for-some-net-sdk-tools"></a>一部の .NET SDK ツールのアクセシビリティが強化されました

#### <a name="details"></a>説明

.NET Framework SDK 4.7.1 では、さまざまなアクセシビリティの問題を修正することで、SvcConfigEditor.exe と SvcTraceViewer.exe のツールが改善されました。 その問題のほとんどは、名前の未定義や、特定の UI の自動化パターンが正しく実装されていないといった軽微なものです。 このような問題は、多くのユーザーが認識しないものですが、スクリーン リーダーのような支援技術を使用するお客様はこれらの SDK ツールのアクセシビリティの強化を実感されるでしょう。 実際に、この修正によって、キーボード フォーカスの順序のような以前の動作がいくつか変更されます。これらのツールのアクセシビリティの修正をすべて取得するには、app.config ファイルを次のようにします。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false"/>
</runtime>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| Version | 4.7.1       |
| 種類    | 再ターゲット中 |
