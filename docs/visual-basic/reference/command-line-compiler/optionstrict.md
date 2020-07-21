---
title: -optionstrict
ms.date: 07/20/2015
f1_keywords:
- -optionstrict
helpviewer_keywords:
- -optionstrict compiler option [Visual Basic]
- optionstrict compiler option [Visual Basic]
- /optionstrict compiler option [Visual Basic]
ms.assetid: c7b10086-0fa4-49db-b3c8-4ae0db5957da
ms.openlocfilehash: 3dd12971a082869c32b6292ed45e2014b8b0e2c0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400540"
---
# <a name="-optionstrict"></a>-optionstrict

厳密な型のセマンティクスが強制され、暗黙的な型変換が制限されます。

## <a name="syntax"></a>構文

```console
-optionstrict[+ | -]
-optionstrict[:custom]
```

## <a name="arguments"></a>引数

`+` &#124; `-`  
任意。 `-optionstrict+` オプションは、暗黙的な型変換を制限します。 このオプションの既定値は `-optionstrict-` です。 `-optionstrict+` オプションは `-optionstrict` と同じです。 どちらも制限が少ない型のセマンティクスに使用できます。

`custom`  
必須です。 厳密な言語セマンティクスが守られていないときに警告します。

## <a name="remarks"></a>Remarks

`-optionstrict+` が有効な場合は、拡大型の変換のみを暗黙的に行うことができます。 整数型のオブジェクトへの `Decimal` 型オブジェクトの割り当てなど、暗黙的な縮小の型変換は、エラーとして報告されます。

暗黙的な縮小の型変換に関する警告を生成するには、`-optionstrict:custom` を使用します。 特定の警告を無視するには `-nowarn:numberlist` を使用し、特定の警告をエラーとして扱うには `-warnaserror:numberlist` を使用します。

### <a name="to-set--optionstrict-in-the-visual-studio-ide"></a>Visual Studio IDE で -optionstrict を設定するには

1. **ソリューション エクスプローラー**でプロジェクトを選択します。 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **[コンパイル]** タブをクリックします。

3. **[Option Strict]** ボックスで値を変更します。

### <a name="to-set--optionstrict-programmatically"></a>-optionstrict をプログラムで設定するには

「[Option Strict ステートメント](../../language-reference/statements/option-strict-statement.md)」を参照してください。

## <a name="example"></a>例

次のコードでは、厳密な型のセマンティクスを使用して `Test.vb` がコンパイルされます。

```console
vbc -optionstrict+ test.vb
```

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-optioncompare](optioncompare.md)
- [-optionexplicit](optionexplicit.md)
- [-optioninfer](optioninfer.md)
- [-nowarn](nowarn.md)
- [-warnaserror (Visual Basic)](warnaserror.md)
- [コンパイル コマンド ラインのサンプル](sample-compilation-command-lines.md)
- [Option Strict ステートメント](../../language-reference/statements/option-strict-statement.md)
- [[Visual Basic の既定値] ([オプション] ダイアログ ボックス - [プロジェクト])](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
