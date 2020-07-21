---
title: エラーの種類
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions, types
- errors [Visual Basic], types
- errors [Visual Basic], logic
- errors [Visual Basic], syntax
- logic errors [Visual Basic], Visual Basic
- run-time errors [Visual Basic], types of errors
- syntax errors [Visual Basic], Visual Basic
ms.assetid: 3048aabf-8c97-4e13-9150-853769cb5f6f
ms.openlocfilehash: 107d93429ad0440ed18169bc6b6ca7b2e21cb77a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405145"
---
# <a name="error-types-visual-basic"></a>エラーの種類 (Visual Basic)
Visual Basic では、エラーは構文エラー、実行時エラー、論理エラーという 3 つのカテゴリのいずれかに分類されます。

## <a name="syntax-errors"></a>構文エラー
 "*構文エラー*" は、コードの記述時に表示されるエラーです。 Visual Studio を使用している場合は、**コード エディター** ウィンドウでコードを入力すると Visual Basic でコードが確認され、単語のスペルミスや言語要素の不適切な使用などの誤りがあった場合は警告が表示されます。 コマンド ラインからコンパイルすると、Visual Basic にはコンパイラ エラーが、構文エラーに関する情報とともに表示されます。 構文エラーは、最も一般的なエラーの種類です。 コーディング環境では、発生したらすぐに、簡単に修正できます。

> [!NOTE]
> `Option Explicit` ステートメントは、構文エラーを回避するための 1 つの手段です。 これにより、アプリケーションで使用するすべての変数を事前に宣言することが強制されます。 そのため、それらの変数をコード内で使用するときは、あらゆる表記エラーを即座に見つけて修正することができます。

## <a name="run-time-errors"></a>実行時エラー
 "*実行時エラー*" は、コードをコンパイルして実行した後でのみ表示されるエラーです。 これには、構文エラーがなく正しく見えるにもかかわらず、実行できないコードが含まれます。 たとえば、ファイルを開くためのコード行を正しく記述したとします。 しかし、そのファイルが存在しない場合は、アプリケーションでファイルを開くことができず、例外がスローされます。 ほとんどの実行時エラーは、問題のあるコードを書き直すか、[例外処理](../../language-reference/statements/try-catch-finally-statement.md)を使用して、再コンパイル後に再実行することによって修正できます。
  
## <a name="logic-errors"></a>論理エラー
 "*論理エラー*" は、アプリケーションの使用中に表示されるエラーです。 ほとんどの場合は、開発者による想定の誤り、またはユーザーの操作に対する応答として望ましくないか、予期しない結果です。 たとえば、キーの誤入力によってメソッドに誤った情報が提供されることがあります。そうでない場合は、常に有効な値がメソッドに渡されるという、想定をしている場合があります。 論理エラーは[例外処理](../../language-reference/statements/try-catch-finally-statement.md)を使用して処理できますが (たとえば、引数が `Nothing` であるかどうかをテストし、<xref:System.ArgumentNullException> をスローするなど)、ほとんどの場合、ロジックのエラーを修正し、アプリケーションを再コンパイルして対処する必要があります。

## <a name="see-also"></a>関連項目

- [Try...Catch...Finally ステートメント](../../language-reference/statements/try-catch-finally-statement.md)
- [デバッガーの基本事項](/visualstudio/debugger/debugger-feature-tour)
