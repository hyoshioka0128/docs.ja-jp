---
title: nameof 式 - C# リファレンス
ms.date: 04/23/2020
f1_keywords:
- nameof_CSharpKeyword
- nameof
helpviewer_keywords:
- nameof expression [C#]
ms.assetid: 33601bf3-cc2c-4496-846d-f9679bccf2a7
ms.openlocfilehash: d71acf0cf7d5cdcfa5310455af2120fa1f82d567
ms.sourcegitcommit: 8b02d42f93adda304246a47f49f6449fc74a3af4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82135920"
---
# <a name="nameof-expression-c-reference"></a>nameof 式 (C# リファレンス)

`nameof` 式を使うと、変数、型、またはメンバーの名前が文字列定数として生成されます。

[!code-csharp-interactive[nameof expression](snippets/NameOfOperator.cs#Examples)]

前の例で示されているように、型と名前空間の場合、生成される名前は通常[完全修飾](~/_csharplang/spec/basic-concepts.md#fully-qualified-names)ではありません。

[逐語的識別子](../tokens/verbatim.md)の場合、次の例に示すように、`@` 文字は名前の一部ではありません。

[!code-csharp-interactive[nameof verbatim](snippets/NameOfOperator.cs#Verbatim)]

`nameof` 式はコンパイル時に評価され、実行時には影響を与えません。

`nameof` 式を使って、引数をチェックするコードの保守性を高めることができます。

[!code-csharp[nameof and argument check](snippets/NameOfOperator.cs#ExceptionMessage)]

`nameof` 式は C# 6 以降で使用できます。

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、[C# 言語仕様](~/_csharplang/spec/introduction.md)の「[Nameof 式](~/_csharplang/spec/expressions.md#nameof-expressions)」セクションをご覧ください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# 演算子](index.md)
