---
title: ファイル エンコーディング
ms.date: 07/20/2015
helpviewer_keywords:
- character encodings
- files [Visual Basic], encoding
- Unicode, file encoding
- file encoding
ms.assetid: ea2c5f5f-bbb1-4150-9928-b9951fa6bc57
ms.openlocfilehash: f906b2f2d747a7950c70a24549bbf5423e5b87b4
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401746"
---
# <a name="file-encodings-visual-basic"></a>ファイル エンコーディング (Visual Basic)

ファイル エンコーディングは、文字エンコーディングとも呼ばれ、テキストを処理するときの文字の表現方法を指定します。 言語で処理できる (または処理できない) 文字という観点から、あるエンコードが他のエンコーディングよりも望ましいということがありますが、一般的には Unicode が好まれます。

ファイルに対する読み取りと書き込みでは、ファイル エンコーディングが適切に一致しないと、例外が発生したり、不正な結果となる場合があります。

## <a name="types-of-encodings"></a>エンコーディングの種類

ファイルを扱うときには、Unicode は最適なエンコーディングです。 Unicode は、世界共通の文字エンコーディング規則で、技術的な記号や出版で使用される特殊文字などを含む、現在のコンピューティングで使用されるすべての文字を、16 ビットのコード値で表します。

これまでの文字エンコーディング規則は、Windows ANSI 文字セットなどの従来からある文字セットで構成されており、8 ビットのコード値や 8 ビット値の組み合わせを使用して、特定の言語や地域で使用する文字を表していました。

## <a name="encoding-class"></a>Encoding クラス

<xref:System.Text.Encoding> クラスは文字エンコーディングを表します。 次の表は、利用可能なエンコーディングの型の一覧とそれぞれの説明です。

|name|[説明]|
|---|---|
|<xref:System.Text.ASCIIEncoding>|Unicode 文字の ASCII 文字エンコードを表します。|
|<xref:System.Text.UnicodeEncoding>|Unicode 文字の UTF-16 エンコーディングを表します。|
|<xref:System.Text.UTF32Encoding>|Unicode 文字の UTF-32 エンコーディングを表します。|
|<xref:System.Text.UTF7Encoding>|Unicode 文字の UTF-7 エンコードを表します。|
|<xref:System.Text.UTF8Encoding>|Unicode 文字の UTF-8 エンコードを表します。|

## <a name="see-also"></a>参照

- [ファイルの読み取り](reading-from-files.md)
- [ファイルへの書き込み](writing-to-files.md)
