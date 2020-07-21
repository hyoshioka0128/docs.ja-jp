---
ms.openlocfilehash: 5e2e8d1ec5d698d1c1649c2a0a1b4b77dbdf4022
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621279"
---
### <a name="wpf-printing-stack-update"></a>WPF での印刷スタックの更新

#### <a name="details"></a>説明

<xref:System.Printing.PrintQueue?displayProperty=fullName> を使う WPF の印刷 API は、非推奨になった XPS 印刷 API ではなく Windows ドキュメント印刷パッケージ API を呼び出すようになりました。 この変更はサービス性を考慮して行われたもので、ユーザーも開発者も、動作または API の使用の変化を目にすることはありません。 Windows 10 Creators Update で実行すると、新しい印刷スタックは既定で有効になります。 以前のバージョンの Windows では、以前の印刷スタックが引き続き同じように動作します。

#### <a name="suggestion"></a>提案される解決策

Windows 10 Creators Update で以前のスタックを使用するには、<code>HKEY_CURRENT_USER\Software\Microsoft\.NETFramework\Windows Presentation Foundation\Printing</code> レジストリ キーの <code>UseXpsOMPrinting</code> REG_DWORD 値を <code>1</code> に設定します。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.7|
|種類|ランタイム|
