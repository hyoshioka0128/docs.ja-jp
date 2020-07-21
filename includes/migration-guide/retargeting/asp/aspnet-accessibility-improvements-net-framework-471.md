---
ms.openlocfilehash: 418bcdca1e9a325894891d7b0e080ce035e2d1b4
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614684"
---
### <a name="aspnet-accessibility-improvements-in-net-framework-471"></a>.NET Framework 4.7.1 の ASP.NET アクセシビリティ機能の強化

#### <a name="details"></a>説明

.NET Framework 4.7.1 以降、ASP.NET のお客様のサポートを改善する目的で、ASP.NET Web コントロールによる Visual Studio のアクセシビリティ テクノロジの処理方法が向上しています。  この機能強化には次の変更内容が含まれています。

- [詳細の表示] ウィザードの [フィールドの追加] ダイアログや ListView ウィザードの [ListView の構成] ダイアログなど、コントロールで不足していた UI アクセシビリティ パターンを実装するための変更。
- データ ページャー フィールド エディターなど、ハイ コントラスト モードでの表示を改善するための変更。
- DataPager コントロールの [ページャーのフィールドを編集] ウィザードの [フィールド] ダイアログ、[ObjectContext の構成] ダイアログ、[データ ソースの構成] ウィザードの [データの選択の構成] ダイアログなど、キーボードの操作性を改善するための変更。

#### <a name="suggestion"></a>提案される解決策

**以上の変更を選択する方法と選択しない方法** Visual Studio デザイナーの場合、.NET Framework 4.7.1 以降で実行しなければ、以上の変更から改善を得ることはありません。 Web アプリケーションの場合、次のいずれかの手法をとることで、以上の変更によって機能が強化されます。

- Visual Studio 2017 15.3 以降をインストールする。このバージョンからは既定で、次の項目にある AppContext スイッチで新しいアクセシビリティ機能に対応しています。
- 下の例のように、devenv.exe.config ファイルの `<runtime>` セクションに `Switch.UseLegacyAccessibilityFeatures` AppContext スイッチを追加し、それを `false` に設定することで、以前のアクセシビリティ動作を無効にする。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
<runtime>
...
<!-- AppContextSwitchOverrides value attribute is in the form of 'key1=true/false;key2=true/false'  -->
<AppContextSwitchOverrides value="Switch.UseLegacyAccessibilityFeatures=false" />
...
</runtime>
</configuration>
```

.NET Framework 4.7.1 以降を対象とするアプリケーションで以前のアクセシビリティ動作を残す場合、この AppContext スイッチを明示的に `true` に設定することで以前のアクセシビリティ機能を選択できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.1       |
| 種類    | 再ターゲット中 |
