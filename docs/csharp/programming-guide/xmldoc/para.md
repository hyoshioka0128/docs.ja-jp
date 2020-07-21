---
title: <para> - C# プログラミング ガイド
ms.date: 07/20/2015
f1_keywords:
- <para>
- para
helpviewer_keywords:
- <para> C# XML tag
- para C# XML tag
ms.assetid: c74b8705-29df-40b1-bff5-237492b0e978
ms.openlocfilehash: d1fe81b1752d066c6b2e1ffe27f0c43fc4068edf
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287299"
---
# <a name="para-c-programming-guide"></a>\<para> (C# プログラミング ガイド)

## <a name="syntax"></a>構文

```xml
<para>content</para>
```

## <a name="parameters"></a>パラメーター

- `content`

  段落のテキストです。

## <a name="remarks"></a>Remarks

`<para>` タグは、[\<summary>](./summary.md)、[\<remarks>](./remarks.md)、または [\<returns>](./returns.md) などのタグ内で使用します。このタグを使用すると、テキストに構造を追加することができます。

コンパイル時に [-doc](../../language-reference/compiler-options/doc-compiler-option.md) を指定して、ドキュメント コメントをファイルに出力します。

## <a name="example"></a>例

`<para>` の使用例については、[\<summary>](./summary.md) を参照してください。

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [ドキュメント コメント用の推奨タグ](./recommended-tags-for-documentation-comments.md)
