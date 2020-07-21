---
title: 制限事項
ms.date: 07/20/2015
helpviewer_keywords:
- limits
- limitations [Visual Basic]
- limitations
- limits, Visual Basic code
- Visual Basic code, limitations
ms.assetid: cf1646b7-5d24-48c6-9616-bda8a4849d91
ms.openlocfilehash: 46294b68bda8a5d2d21c0e4efea6a78e6a265ffe
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403188"
---
# <a name="visual-basic-limitations"></a>Visual Basic の制限事項
以前のバージョンの Visual Basic では、変数名の長さ、モジュールで許可される変数の数、モジュール サイズなど、コードに上限が適用されていました。 Visual Basic .NET では、これらの制限が緩和され、コードをより自由に記述および配置できるようになりました。  
  
 物理的な制限は、コンパイル時の考慮事項よりも実行時のメモリに大きく依存します。 慎重なプログラミング プラクティスを使用し、大規模なアプリケーションを複数のクラスやモジュールに分割すれば、Visual Basic の内部的な制限が発生する可能性はほとんどありません。  
  
 極端な場合に発生する可能性があるいくつかの制限を以下に示します。  
  
- **名前の長さ:** 宣言されるすべてのプログラミング要素の名前には最大文字数があります。 要素名が修飾されている場合、この最大数は修飾文字列全体に適用されます。 「 [Declared Element Names](../language-features/declared-elements/declared-element-names.md)」を参照してください。  
  
- **行の長さ:** ソース コードの物理的な行の最大文字数は 65535 文字です。 行連結文字を使用すると、論理的なソース コード行が長くなる可能性があります。 「[方法:コード内でステートメントを分割および連結する](how-to-break-and-combine-statements-in-code.md)」をご覧ください。  
  
- **配列の次元:** 配列で宣言できる次元数には上限があります。 これにより、配列要素を指定する際に使用できるインデックスの数が制限されます。 「[Visual Basic における配列の次元](../language-features/arrays/array-dimensions.md)」をご覧ください。  
  
- **文字列の長さ:** 1 つの文字列に格納できる Unicode 文字数には上限があります。 「[文字列型 (String)](../../language-reference/data-types/string-data-type.md)」をご覧ください。  
  
- **環境文字列の長さ:** コマンド ライン引数として使用される環境文字列の最大文字数は 32768 文字です。 この制限はすべてのプラットフォームに適用されます。  
  
## <a name="see-also"></a>関連項目

- [プログラム構造とコード規則](program-structure-and-code-conventions.md)
- [Visual Basic の名前付け規則](naming-conventions.md)
