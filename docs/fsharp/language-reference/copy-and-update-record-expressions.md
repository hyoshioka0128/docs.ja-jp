---
title: レコード式のコピーと更新
description: 既存のレコードまたは匿名レコードをコピーし、指定されたフィールドを更新し、更新されたレコードまたは匿名レコードを返す「コピーおよび更新式」を記述する方法を説明します。
author: ChrSteinert
ms.date: 06/12/2019
ms.openlocfilehash: bec3e0ac2fb34e358b199c509c4599b55d7bf35e
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81739285"
---
# <a name="copy-and-update-record-expressions"></a>レコード式のコピーと更新

*コピーおよび更新レコード式*は、既存のレコードをコピーし、指定されたフィールドを更新して、更新されたレコードを返す式です。

## <a name="syntax"></a>構文

```fsharp
{ record-name with
    updated-labels }

{| anonymous-record-name with
    updated-labels |}
```

## <a name="remarks"></a>解説

レコードと匿名レコードは既定で変更できないので、既存のレコードを更新することはできません。 更新されたレコードを作成するには、レコードのすべてのフィールドを再指定する必要があります。 このタスクを簡略化するために、*コピー式と更新式*を使用できます。 この式は既存のレコードを受け取り、式の指定されたフィールドと、式で指定された欠落フィールドを使用して、同じタイプの新しいレコードを作成します。

これは、既存のレコードをコピーし、フィールド値の一部を変更する必要がある場合に役立ちます。

たとえば、新しく作成されたレコードを取ります。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1905.fs)]

そのレコードの 2 つのフィールドだけを更新するには、*コピーおよび更新レコード式*を使用します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet1906.fs)]

## <a name="see-also"></a>関連項目

- [レコード](records.md)
- [匿名のレコード](anonymous-records.md)
- [F# 言語リファレンス](index.md)
