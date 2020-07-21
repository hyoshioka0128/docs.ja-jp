---
title: XML の使用によるコードのドキュメントの作成
ms.date: 07/20/2015
helpviewer_keywords:
- XML [Visual Basic], documenting code
- XML comments, Visual Basic
- Visual Basic code, documenting with XML
ms.assetid: a0d35dc7-c5f9-4d74-92ff-a1c6f28d5235
ms.openlocfilehash: f391fb909cfe4de8f27afb24d6db389e2c8cdfae
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84590930"
---
# <a name="document-your-code-with-xml-visual-basic"></a>XML の使用によるコードのドキュメントの作成 (Visual Basic)

Visual Basic では、XML を使用してコードを文書化できます。

## <a name="xml-documentation-comments"></a>XML ドキュメント コメント

Visual Basic には、プロジェクトの XML ドキュメントを自動的に作成する簡単な方法が用意されています。 型とメンバーの XML スケルトンを自動的に生成し、概要、各パラメーターの説明ドキュメント、その他の注釈を指定できます。 適切な設定により、XML ドキュメントは、ご利用のプロジェクトと同じルート ファイル名を使用して XML ファイルに自動的に出力されます。 詳細については、「[-doc](../../reference/command-line-compiler/doc.md)」を参照してください。

XML ファイルは、XML として使用したり、操作したりできます。 このファイルは、プロジェクトの出力 .exe または .dll ファイルと同じディレクトリにあります。

XML ドキュメントは `'''` で始まります。 これらのコメントの処理にはいくつか制限があります。

- ドキュメントは整形式の XML である必要があります。 XML が整形式ではない場合は、警告が生成され、エラーが発生したことを示すコメントがドキュメント ファイルに追加されます。

- 開発者は、独自のタグ セットを自由に作成できます。 推奨されるタグのセットがあります ([XML のコメント用タグ](../../language-reference/xmldoc/index.md)に関するページを参照してください)。 推奨されるタグの一部には特別な意味があります。

  - \<param> タグは、パラメーターの記述に使用します。 このタグがあると、コンパイラは、パラメーターが存在すること、およびすべてのパラメーターがドキュメントで記述されていることを確認します。 検証が失敗すると、コンパイラは警告を発行します。

  - `cref` 属性は任意のタグにアタッチでき、コード要素への参照を提供します。 コンパイラは、このコード要素が存在することを確認します。 検証が失敗すると、コンパイラは警告を発行します。 また、コンパイラは、`cref` 属性で記述されている型を探すときに、`Imports` ステートメントを優先します。

  - \<summary> タグは、型またはメンバーに関する追加情報を表示するために、Visual Studio の IntelliSense によって使用されます。

## <a name="related-sections"></a>関連項目

ドキュメント コメントを含む XML ファイルの作成方法の詳細については、次のトピックをご覧ください。

- [-doc](../../reference/command-line-compiler/doc.md)

- [XML のコメント用タグ](../../language-reference/xmldoc/index.md)

- [XML ファイルの処理](processing-the-xml-file.md)

- [方法: XML ドキュメントを作成する](how-to-create-xml-documentation.md)

- [Visual Studio の XML ツール](/visualstudio/xml-tools/xml-tools-in-visual-studio)

## <a name="see-also"></a>関連項目

- [Visual Basic でのアプリケーションの開発](../../developing-apps/index.md)
- [Visual Basic プログラミング ガイド](../index.md)
