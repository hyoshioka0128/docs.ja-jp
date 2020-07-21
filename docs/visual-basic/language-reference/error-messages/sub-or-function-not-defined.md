---
title: Sub または Function が定義されていません。
ms.date: 07/20/2015
f1_keywords:
- vbrID35
ms.assetid: 661fdb90-ee7d-40ce-b30b-5e7267bd957a
ms.openlocfilehash: 9eb13d943f9f1cffc984847f7339111e06f5aa6b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84373928"
---
# <a name="sub-or-function-not-defined-visual-basic"></a>Sub または Function が定義されていません。(Visual Basic)
呼び出されるには、`Sub` または `Function` が定義されている必要があります。 このエラーでは以下の原因が考えられます。  
  
- プロシージャ名のスペルが間違っています。  
  
- **[参照]** ダイアログ ボックスで、プロジェクトへの参照を明示的に追加せずに、別のプロジェクトからプロシージャを呼び出そうとしています。  
  
- 呼び出し元のプロシージャから参照できないプロシージャを指定しています。  
  
- 指定したライブラリまたはコード リソースにない Windows ダイナミックリンク ライブラリ (DLL) ルーチンまたは Macintosh コードリソース ルーチンを宣言しています。  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
1. プロシージャ名のスペルが正しいことを確認します。  
  
2. **[参照]** ダイアログボックスで、呼び出すプロシージャを含むプロジェクトの名前を見つけます。 それが表示されない場合、 **[参照]** ボタンをクリックして検索します。 プロジェクト名の左側にあるチェック ボックスをオンにして、 **[OK]** をクリックします。  
  
3. ルーチンの名前を確認します。  
  
## <a name="see-also"></a>関連項目

- [エラーの種類](../../programming-guide/language-features/error-types.md)
- [プロジェクト内の参照の管理](/visualstudio/ide/managing-references-in-a-project)
- [Sub ステートメント](../statements/sub-statement.md)
- [Function ステートメント](../statements/function-statement.md)
