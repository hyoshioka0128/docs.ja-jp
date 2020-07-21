---
title: 名前 '<name>' は宣言されていません。
ms.date: 10/10/2018
f1_keywords:
- bc30451
- vbc30451
helpviewer_keywords:
- BC30451
ms.assetid: 765f099b-e21e-47c6-a906-a065444e56b3
ms.openlocfilehash: 6fa4639b97e4314d8752ae520e94a58a189b7cbb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397169"
---
# <a name="name-name-is-not-declared"></a>名前 '\<name>' は宣言されていません。
ステートメントでプログラミング要素を参照していますが、名前が完全に一致する要素をコンパイラが見つけることができません。  
  
 **エラー ID:** BC30451  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. 参照元のステートメントで名前のスペルを確認します。 Visual Basic では、大文字と小文字が区別されませんが、スペルに他の何らかの違いがあった場合は完全に異なる名前と見なされます。 アンダースコア (`_`) も名前の一部であり、スペルに含まれます。  
  
2. オブジェクトとそのメンバーの間にメンバー アクセス演算子 (`.`) を指定していることを確認します。 たとえば、 <xref:System.Windows.Forms.TextBox> という名前の `TextBox1`コントロールがある場合、このコントロールの <xref:System.Windows.Forms.TextBoxBase.Text%2A> プロパティにアクセスするには、「 `TextBox1.Text`」と入力する必要があります。 代わりに「 `TextBox1Text`」と入力した場合、別の名前と見なされます。  
  
3. スペルが正しく、オブジェクト メンバー アクセスの構文が正しい場合は、要素が宣言されていることを確認します。 詳細については、[宣言された要素](../../programming-guide/language-features/declared-elements/index.md)に関するページを参照してください。  
  
4. プログラミング要素が宣言されている場合、それがスコープ内にあることを確認します。 参照元のステートメントがプログラミング要素を宣言している領域の外部にある場合は、要素名を修飾する必要がある場合があります。 詳細については、「 [Scope in Visual Basic](../../programming-guide/language-features/declared-elements/scope.md)」を参照してください。  

5. 完全修飾型または型とメンバー名を使用していない (たとえば、コードで `System.Reflection.MethodInfo.Name` ではなく `MethodInfo.Name` としてプロパティを参照している) 場合は、[Imports ステートメント](../statements/imports-statement-net-namespace-and-type.md)を追加します。

6. SDK スタイルのプロジェクト (`<Project Sdk="Microsoft.NET.Sdk">` 行で始まる \*.vbproj ファイルによるプロジェクト) をコンパイルしようとし、エラーメッセージで、Microsoft.VisualBasic.dll アセンブリの型またはメンバーが参照されている場合は、Visual Basic ランタイム ライブラリへの参照を使用してコンパイルするようにアプリケーションを構成します。 既定で、ライブラリのサブセットは、SDK スタイルのプロジェクトのアセンブリに埋め込まれます。

   たとえば、次の例では、<xref:Microsoft.VisualBasic.CompilerServices.Conversions.ChangeType%2A?displayProperty=fullName> メソッドが見つからないため、コンパイルに失敗します。 アプリケーションに含まれている Visual Basic ランタイムのサブセットに埋め込まれていません。  

   [!code-vb[BC30451](~/samples/snippets/visualbasic/language-reference/error-messages/bc30451/program1.vb?highlight=7)]

   このエラーに対処するには、次の Visual Basic プロジェクト ファイルに示すように、プロジェクトの `<PropertyGroup>` セクションに `<VBRuntime>Default</VBRuntime>` 要素を追加します。

   [!code-xml[BC30451](~/samples/snippets/visualbasic/language-reference/error-messages/bc30451/vbruntime.vbproj?highlight=6)]

## <a name="see-also"></a>関連項目

- [宣言と定数の概要](../keywords/declarations-and-constants-summary.md)
- [Visual Basic の名前付け規則](../../programming-guide/program-structure/naming-conventions.md)
- [宣言された要素の名前](../../programming-guide/language-features/declared-elements/declared-element-names.md)
- [宣言された要素の参照](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
