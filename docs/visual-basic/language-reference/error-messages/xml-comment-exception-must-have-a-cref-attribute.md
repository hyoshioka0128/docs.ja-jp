---
title: XML コメントの例外には 'cref' 属性を指定しなければなりません
ms.date: 07/20/2015
f1_keywords:
- bc42319
- vbc42319
helpviewer_keywords:
- BC42319
ms.assetid: 62eeeba3-6811-48be-b1ef-c2e4feda3177
ms.openlocfilehash: c498675ab6ae616fb63d3d76ef60bcac7e247145
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406509"
---
# <a name="xml-comment-exception-must-have-a-cref-attribute"></a>XML コメントの例外には 'cref' 属性を指定しなければなりません

\<exception> タグは、メソッドによってスローされる可能性のある例外を文書化する方法を提供します。 必須の `cref` 属性は、ドキュメント生成機能によってチェックされるメンバーの名前を指定します。 メンバーが存在する場合、そのメンバーはドキュメント ファイル内の正規要素名に変換されます。

**エラー ID:** BC42319

## <a name="to-correct-this-error"></a>このエラーを解決するには

次のように、例外に `cref` 属性を追加します。

```xml
<exception cref="member">description</exception>
```

## <a name="see-also"></a>関連項目

- [\<exception>](../xmldoc/exception.md)
- [方法: XML ドキュメントを作成する](../../programming-guide/program-structure/how-to-create-xml-documentation.md)
- [XML のコメント用タグ](../xmldoc/index.md)
