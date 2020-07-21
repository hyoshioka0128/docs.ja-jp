---
title: <remarks> - C# プログラミング ガイド
ms.date: 07/20/2015
f1_keywords:
- remarks
- <remarks>
helpviewer_keywords:
- remarks C# XML tag
- <remarks> C# XML tag
ms.assetid: f8641391-31f3-4735-af7a-c502a5b6a251
ms.openlocfilehash: 739027786e02e559d86f990bf614e261b497c76f
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287286"
---
# <a name="remarks-c-programming-guide"></a>\<remarks> (C# プログラミング ガイド)

## <a name="syntax"></a>構文

```xml
<remarks>description</remarks>
```

## <a name="parameters"></a>パラメーター

- `Description`

  メンバーの説明。

## <a name="remarks"></a>Remarks

`<remarks>` タグを使用して、型の情報を追加し、[\<summary>](./summary.md) で指定された情報を補足します。 この情報はオブジェクト ブラウザー ウィンドウに表示されます。

コンパイル時に [-doc](../../language-reference/compiler-options/doc-compiler-option.md) を指定して、ドキュメント コメントをファイルに出力します。

## <a name="example"></a>例

[!code-csharp[csProgGuideDocComments#9](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDocComments/CS/DocComments.cs#9)]

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [ドキュメント コメント用の推奨タグ](./recommended-tags-for-documentation-comments.md)
