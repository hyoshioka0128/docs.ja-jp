---
ms.openlocfilehash: 1d2e4a058008676c6ea85becebd4bb9220569ef3
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621363"
---
### <a name="wpf-spell-checking-in-text-enabled-controls-will-not-work-in-windows-10-for-languages-not-in-the-oss-input-language-list"></a>OS の入力言語リストにない言語の場合、Windows 10 でテキスト対応コントロールの WPF スペル チェックが動作しなくなる

#### <a name="details"></a>説明

プラットフォームのスペル チェック機能は入力言語リストに存在する言語でしか使用できないため、 Windows 10 での実行時には、WPF テキスト対応コントロール向けのスペル チェック機能が動作しないことがあります。Windows 10 では、使用可能なキーボードのリストに言語を追加すると、対応するオンデマンド機能 (FOD) パッケージが自動的にダウンロードおよびインストールされ、スペル チェック機能が提供されます。 入力言語リストに言語を追加することで、スペル チェック機能がサポートされます。

#### <a name="suggestion"></a>提案される解決策

Windows 10 でスペルチェックを動作させるには、スペルチェック対象の言語またはテキストを入力言語として追加する必要があることに注意してください。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.6|
|種類|ランタイム|
