---
title: <param> - C# プログラミング ガイド
ms.date: 07/20/2015
f1_keywords:
- param
- <param>
helpviewer_keywords:
- <param> C# XML tag
- param C# XML tag
ms.assetid: 46d329b1-5b84-4537-9e17-73ca97313e4e
ms.openlocfilehash: 396ed716c246091a674268020261069f36dd2be8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287325"
---
# <a name="param-c-programming-guide"></a>\<param> (C# プログラミング ガイド)

## <a name="syntax"></a>構文

```xml
<param name="name">description</param>
```

## <a name="parameters"></a>パラメーター

- `name`

  メソッド パラメーターの名前です。 名前は二重引用符 (" ") で囲みます。

- `description`

  パラメーターの説明です。

## <a name="remarks"></a>Remarks

`<param>` タグは、メソッドのいずれかのパラメーターを記述するために、メソッド宣言のコメントで使用する必要があります。 複数のパラメーターをドキュメント化するには、複数の `<param>` タグを使用します。

`<param>` タグのテキストは、IntelliSense、オブジェクト ブラウザー、コード コメント Web レポートに表示されます。

コンパイル時に [-doc](../../language-reference/compiler-options/doc-compiler-option.md) を指定して、ドキュメント コメントをファイルに出力します。

## <a name="example"></a>例

[!code-csharp[csProgGuideDocComments#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#1)]

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [ドキュメント コメント用の推奨タグ](./recommended-tags-for-documentation-comments.md)
