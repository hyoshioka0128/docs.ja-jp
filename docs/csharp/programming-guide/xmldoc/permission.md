---
title: <permission> - C# プログラミング ガイド
ms.date: 07/20/2015
f1_keywords:
- permission
- <permission>
helpviewer_keywords:
- <permission> C# XML tag
- permission C# XML tag
ms.assetid: 769e93fe-8404-443f-bf99-577aa42b6a49
ms.openlocfilehash: bb7172042f0b472d03c3fa2d9dbd0d4d4265076b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287273"
---
# <a name="permission-c-programming-guide"></a>\<permission> (C# プログラミング ガイド)

## <a name="syntax"></a>構文

```xml
<permission cref="member">description</permission>
```

## <a name="parameters"></a>パラメーター

- cref = "`member`"

  現在のコンパイル環境からの呼び出しに利用できる、メンバーまたはフィールドへの参照。 コンパイラは、指定されたコード要素が存在し、出力の XML で `member` が正規要素名に変換されることを確認します。 *member* は、二重引用符 (" ") で囲む必要があります。

  ジェネリック型への cref 参照を作成する方法については、[cref 属性](./cref-attribute.md)に関するページを参照してください。

- `description`

  メンバーへのアクセスの説明です。

## <a name="remarks"></a>Remarks

`<permission>` タグを使用すると、メンバーのアクセスをドキュメント化できます。 <xref:System.Security.PermissionSet> クラスを使用すると、メンバーへのアクセスを指定できます。

コンパイル時に [-doc](../../language-reference/compiler-options/doc-compiler-option.md) を指定して、ドキュメント コメントをファイルに出力します。

## <a name="example"></a>例

[!code-csharp[csProgGuideDocComments#8](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#8)]

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [ドキュメント コメント用の推奨タグ](./recommended-tags-for-documentation-comments.md)
