---
title: <example> - C# プログラミング ガイド
ms.date: 07/20/2015
f1_keywords:
- <example>
- example
helpviewer_keywords:
- <example> C# XML tag
- example C# XML tag
ms.assetid: 32d6e73b-2554-4abb-83ee-a1e321334fd2
ms.openlocfilehash: e8d26f82562cc5140662f5b32ea9fedf5481d8f8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287391"
---
# <a name="example-c-programming-guide"></a>\<example> (C# プログラミング ガイド)

## <a name="syntax"></a>構文

```xml
<example>description</example>
```

## <a name="parameters"></a>パラメーター

- `description`

  コード例の説明です。

## <a name="remarks"></a>Remarks

`<example>` タグを使用すると、メソッドまたは他のライブラリ メンバーの使用例を指定できます。 一般的に、[\<code>](./code.md) タグが使用されます。

コンパイル時に [-doc](../../language-reference/compiler-options/doc-compiler-option.md) を指定して、ドキュメント コメントをファイルに出力します。

## <a name="example"></a>例

[!code-csharp[csProgGuideDocComments#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#3)]

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [ドキュメント コメント用の推奨タグ](./recommended-tags-for-documentation-comments.md)
