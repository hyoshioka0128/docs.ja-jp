---
title: -delaysign
ms.date: 03/10/2018
helpviewer_keywords:
- delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
- -delaysign compiler option [Visual Basic]
ms.assetid: c76e61a4-1884-4252-9fb2-377f99caa690
ms.openlocfilehash: c9bb302e2b34ebe1f51cf39bb3db1094d420d7f4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408700"
---
# <a name="-delaysign"></a>-delaysign

アセンブリに完全に署名するか、部分的に署名するかを指定します。

## <a name="syntax"></a>構文

```console
-delaysign[+ | -]
```

## <a name="arguments"></a>引数

`+` &#124; `-`  
任意。 完全署名されたアセンブリを作成する場合は、`-delaysign-` を使用します。 公開キーをアセンブリに配置し、署名済みハッシュ用に領域を予約する場合は、`-delaysign+` を使用します。 既定値は、`-delaysign-` です。

## <a name="remarks"></a>Remarks

`-delaysign` オプションは、[-keyfile](keyfile.md) または [-keycontainer](keycontainer.md) と共に使用しない場合、無効になります。

アセンブリに完全に署名するように指定すると、コンパイラはマニフェスト (アセンブリ メタデータ) を含むファイルをハッシュし、秘密キーでそのハッシュに署名します。 結果として得られるデジタル署名は、マニフェストを含むファイルに格納されます。 アセンブリを遅延署名に設定すると、コンパイラは署名の計算も格納も行いませんが、後で署名を追加できるようにファイルに領域を確保します。

たとえば、`-delaysign+` を使用すると、組織の開発者は、テスト担当者がグローバル アセンブリ キャッシュに登録して使用できるアセンブリの署名なしのテスト バージョンを配布できます。 アセンブリの作業が完了すると、組織の秘密キーの担当者がアセンブリに完全に署名できるようになります。 このコンパートメント化により、すべての開発者がアセンブリを操作できるようになると同時に、組織の秘密キーを漏えいから保護します。

アセンブリへの署名の詳細については、「[厳密な名前付きアセンブリの作成と使用](../../../standard/assembly/create-use-strong-named.md)」を参照してください。

### <a name="to-set--delaysign-in-the-visual-studio-integrated-development-environment"></a>Visual Studio 統合開発環境で -delaysign を設定するには

1. **ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[署名]** タブをクリックします。

3. **[遅延署名のみ]** ボックスに値を設定します。

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-keyfile](keyfile.md)
- [-keycontainer](keycontainer.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
