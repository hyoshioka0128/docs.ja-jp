---
title: XamlName の文法
ms.date: 03/30/2017
helpviewer_keywords:
- DottedXamlName grammar [XAML Services]
- grammar [XAML Services], DottedXamlName
- grammar [XAML Services], XamlName
- names in XAML [XAML Services]
- XamlName grammar [XAML Services]
ms.assetid: 11e4cada-41d2-494d-9531-0d3df4dfcbe3
ms.openlocfilehash: 2fc74990b15caaa9b58e6eea5b0212ea22505674
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "81433050"
---
# <a name="xamlname-grammar"></a>XamlName の文法

XamlName 文法は、XAML 言語仕様 [MS-XAML] で定義されている特定の文法です。

## <a name="from-the-xaml-specification"></a>XAML 仕様から

[MS-XAML] 仕様では、型とプロパティに使用される一連の有効なシンボル識別子を識別する文法 XamlName が定義されています。

XamlName 型の文字列値は、次の文法に準拠している必要があります。

```xaml
XamlName ::= NameStartChar ( NameChar )*
NameStartChar ::= LetterCharacter | '_'
NameChar ::= NameStartChar | DecimalDigit | CombiningCharacter
LetterCharacter ::= UnicodeLu | UnicodeLl | UnicodeLo | UnicodeLt | UnicodeNl
DecimalDigit ::= UnicodeNd
CombiningCharacter ::= UnicodeMn | UnicodeMc
```

Unicode 文字データベースで定義されている次の一般的なカテゴリ値を想定しています。

| ユニコードカテゴリ   | 説明                   |
|--------------------|-------------------------------|
| ルー語                 | Letter, Uppercase (字、大文字)             |
| Ll                 | Letter, Lowercase (字、小文字)             |
| Lt                 | Letter, Titlecase (字、タイトル文字)             |
| Lm                 | Letter, Modifier (字、修飾)              |
| Lo                 | Letter, Other (字、その他)                 |
| Mn                 | マーク、非間隔             |
| Mc                 | Mark, Spacing Combining (結合文字、幅あり)       |
| Nd                 | 数値、小数               |
| Nl                 | Number, Letter (数、字)                |

XAML では、プロパティとイベント修飾参照、およびアタッチされたメンバーに対して使用される 2 番目の文法 DXamlName を定義します。 詳細については、「 と<xref:System.Windows.DependencyProperty> [XAML の概要 (WPF)](../fundamentals/xaml.md)」を参照してください。

型が DXamlName の文字列値は、次の文法に準拠する必要があります。

```xaml
DottedXamlName ::= XamlName '.' XamlName
```

## <a name="remarks"></a>解説

完全な仕様については、 [ \[MS-XAML\]](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))を参照してください。
