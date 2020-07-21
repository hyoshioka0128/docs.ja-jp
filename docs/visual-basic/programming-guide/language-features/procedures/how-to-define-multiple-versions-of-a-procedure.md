---
title: '方法: プロシージャの複数のバージョンを定義する'
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], defining
- Visual Basic code, procedures
- procedures [Visual Basic], overloading
- procedures [Visual Basic], multiple versions
- procedure overloading [Visual Basic], multiple versions
ms.assetid: 71ccdd66-1b00-4b66-bee4-6926c0d696f4
ms.openlocfilehash: 870a18dbf3a7e28b7d7b612e853beeec6908cf6f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84387934"
---
# <a name="how-to-define-multiple-versions-of-a-procedure-visual-basic"></a>方法: プロシージャの複数のバージョンを定義する (Visual Basic)
同じ名前を使用し、バージョンごとに異なるパラメーター リストを使用して、"*オーバーロード*" することにより、複数のバージョンのプロシージャを定義できます。 オーバーロードの目的は、名前で区別する必要なく、プロシージャの密接に関連する複数のバージョンを定義することです。  
  
 詳細については、「 [Procedure Overloading](./procedure-overloading.md)」を参照してください。  
  
### <a name="to-define-multiple-versions-of-a-procedure"></a>プロシージャの複数のバージョンを定義するには  
  
1. 定義するプロシージャのバージョンごとに、`Sub` または `Function` 宣言ステートメントを記述します。 すべての宣言で同じプロシージャ名を使用します。  
  
2. 各宣言の `Sub` または `Function` キーワードの前に [Overloads](../../../language-reference/modifiers/overloads.md) キーワードを指定します。 必要に応じて、宣言で `Overloads` を省略することもできますが、宣言のいずれかに含めた場合は、すべての宣言に含める必要があります。  
  
3. 各宣言ステートメントの後に、呼び出し元のコードでそのバージョンのパラメーター リストと一致する引数が指定されたときにそのケースを処理するプロシージャ コードを記述します。 呼び出し元のコードでどのパラメーターが指定されているかをテストする必要はありません。 Visual Basic は、プロシージャの一致するバージョンに制御を渡します。  
  
4. プロシージャの各バージョンを、必要に応じて `End Sub` または `End Function` ステートメントで終了します。  
  
## <a name="example"></a>例  
 次の例では、顧客の残高に対してトランザクションを転記する `Sub` プロシージャを定義します。 `Overloads` キーワードを使用して、プロシージャの 2 つのバージョンを定義します。1 つは顧客を名前で受け入れ、もう 1 つは口座番号で受け入れます。  
  
 [!code-vb[VbVbcnProcedures#72](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#72)]  
  
 呼び出し元のコードは、`String` または `Integer` として顧客 ID を取得し、どちらの場合も同じ呼び出しステートメントを使用できます。  
  
 `post` プロシージャのこれらのバージョンを呼び出す方法については、「[How to: Call an Overloaded Procedure (方法: オーバーロードされたプロシージャを呼び出す)](./how-to-call-an-overloaded-procedure.md)」をご覧ください。  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 オーバーロードされた各バージョンのプロシージャ名が同じであり、パラメーター リストが異なることを確認します。  
  
## <a name="see-also"></a>関連項目

- [手順](./index.md)
- [プロシージャのパラメーターと引数](./procedure-parameters-and-arguments.md)
- [プロシージャのトラブルシューティング](./troubleshooting-procedures.md)
- [方法: 省略可能なパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-optional-parameters.md)
- [方法: 不特定数のパラメーターを受け取るプロシージャをオーバーロードする](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)
- [プロシージャのオーバーロードに関する注意事項](./considerations-in-overloading-procedures.md)
- [オーバーロードの解決](./overload-resolution.md)
