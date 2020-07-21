---
title: <seealso> - C# プログラミング ガイド
ms.date: 07/20/2015
f1_keywords:
- cref
- <seealso>
- seealso
helpviewer_keywords:
- cref [C#], see also
- seealso C# XML tag
- cref [C#]
- cross-references [C#], tags
- <seealso> C# XML tag
ms.assetid: 8e157f3f-f220-4fcf-9010-88905b080b18
ms.openlocfilehash: 1b801ac1b5a0a59d97ccc35ec78930d99223e846
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287221"
---
# <a name="seealso-c-programming-guide"></a>\<seealso> (C# プログラミング ガイド)

## <a name="syntax"></a>構文

```xml
<seealso cref="member"/>
```

## <a name="parameters"></a>パラメーター

- cref = "`member`"

  現在のコンパイル環境からの呼び出しに利用できる、メンバーまたはフィールドへの参照。 コンパイラは、指定されたコード要素が存在するかどうかを確認し、`member` を出力 XML 内の要素名に渡します。`member` は二重引用符 (" ") で囲む必要があります。

  ジェネリック型への cref 参照を作成する方法については、[cref 属性](./cref-attribute.md)に関するページを参照してください。

## <a name="remarks"></a>Remarks

`<seealso>` タグを使用して、「関連項目」セクションに表示するテキストを指定することができます。 [\<see>](./see.md) を使用すると、テキスト内からリンクを指定できます。

コンパイル時に [-doc](../../language-reference/compiler-options/doc-compiler-option.md) を指定して、ドキュメント コメントをファイルに出力します。

## <a name="example"></a>例

\<seealso> の使用例については、[\<summary>](./summary.md) を参照してください。

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [ドキュメント コメント用の推奨タグ](./recommended-tags-for-documentation-comments.md)
