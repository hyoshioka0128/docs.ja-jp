---
title: <see> - C# プログラミング ガイド
ms.date: 07/20/2015
f1_keywords:
- <see>
- see
helpviewer_keywords:
- cref [C#], <see> tag
- <see> C# XML tag
- cross-references [C#]
- see C# XML tag
ms.assetid: 0200de01-7e2f-45c4-9094-829d61236383
ms.openlocfilehash: 0f10feb0931c6d38c817fdecb925f68d439abb59
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287247"
---
# <a name="see-c-programming-guide"></a>\<see> (C# プログラミング ガイド)

## <a name="syntax"></a>構文

```xml
<see cref="member"/>
```

## <a name="parameters"></a>パラメーター

- cref = "`member`"

  現在のコンパイル環境からの呼び出しに利用できる、メンバーまたはフィールドへの参照。 コンパイラは、指定されたコード要素が存在するかどうかを確認し、`member` を出力 XML 内の要素名に渡します。 *メンバー*は二重引用符 (" ") で囲む必要があります。

## <a name="remarks"></a>Remarks

`<see>` タグを使用すると、テキスト内からリンクを指定できます。 テキストが「関連項目」セクションに配置されていることを示すには、[\<seealso>](./seealso.md) を使用します。 コード要素のドキュメント ページへの内部ハイパーリンクを作成するには、[cref 属性](./cref-attribute.md)を使用します。

コンパイル時に [-doc](../../language-reference/compiler-options/doc-compiler-option.md) を指定して、ドキュメント コメントをファイルに出力します。

次の例では、「概要」セクション内の `<see>` タグを示しています。

[!code-csharp[csProgGuideDocComments#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#12)]

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [ドキュメント コメント用の推奨タグ](./recommended-tags-for-documentation-comments.md)
