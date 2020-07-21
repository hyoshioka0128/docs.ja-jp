---
title: 文字セットとマーシャリング - .NET
description: CharSet の値によって、.NET でデータをネイティブ コードにマーシャリングする方法がどのように変わるかについて説明します。
ms.date: 01/18/2019
ms.openlocfilehash: 39566593aa38bacfa41b44a8af8cc2dfb294d766
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85416110"
---
# <a name="charsets-and-marshaling"></a>文字セットとマーシャリング

`char` 値、`string` オブジェクト、および `System.Text.StringBuilder` オブジェクトのマーシャリング方法は、P/Invoke または構造体どちらかの `CharSet` フィールド値によって変わります。 P/Invoke の `CharSet` を設定するには、P/Invoke を宣言するときに <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> フィールドを設定します。 型の `CharSet` を設定するには、クラスまたは構造体宣言の <xref:System.Runtime.InteropServices.StructLayoutAttribute.CharSet?displayProperty=nameWithType> フィールドを設定します。 これらの属性フィールドが設定されていない場合、言語コンパイラによって使用する `CharSet` が決まります。 C# と Visual Basic は既定で <xref:System.Runtime.InteropServices.CharSet.Ansi> 文字セットを使用します。

次の表は、各文字セット間のマッピングと、その文字セットを使ってマーシャリングした場合に文字または文字列がどのように表現されるかを示しています。

| `CharSet` の値 | Windows            | Unix 上での .NET Core 2.2 以前 | Unix 上での .NET Core 3.0 以降および Mono |
|-----------------|--------------------|-----------------------------------|------------------------------------------|
| `Ansi`          | `char` (システム既定の [Windows (ANSI) コード ページ](/windows/win32/intl/code-pages))      | `char` (UTF-8)                    | `char` (UTF-8)                           |
| `Unicode`       | `wchar_t` (UTF-16) | `char16_t` (UTF-16)               | `char16_t` (UTF-16)                      |
| `Auto`          | `wchar_t` (UTF-16) | `char16_t` (UTF-16)               | `char` (UTF-8)                           |

文字セットを選択するときは、必ずネイティブ表現で期待される表現を必ず把握しておいてください。
