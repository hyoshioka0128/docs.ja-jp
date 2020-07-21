---
title: Error ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.error
helpviewer_keywords:
- Error statement [Visual Basic], syntax
- Error statement [Visual Basic]
- Error keyword [Visual Basic]
- run-time errors [Visual Basic], codes
- errors [Visual Basic], simulating
ms.assetid: 85cd5c59-5224-4f02-aaf5-fcfefab17a29
ms.openlocfilehash: 35ba1f19654d1d23ac1ec73564bc36b0af4f6777
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404746"
---
# <a name="error-statement"></a>Error ステートメント
エラーの発生をシミュレートします。  
  
## <a name="syntax"></a>構文  
  
```vb  
Error errornumber  
```  
  
## <a name="parts"></a>指定項目  
 `errornumber`  
 必須です。 任意の有効なエラー番号を指定できます。  
  
## <a name="remarks"></a>Remarks  
 `Error` ステートメントは下位互換性のためにサポートされています。 新しいコードでは、特にオブジェクトを作成する場合に、`Err` オブジェクトの `Raise` メソッドを使用して、実行時エラーを生成します。  
  
 `errornumber` を定義している場合、`Err` オブジェクトのプロパティに次の既定値が代入されると、`Error` ステートメントによって、エラー ハンドラーが呼び出されます。  
  
|プロパティ|[値]|  
|--------------|-----------|  
|`Number`|`Error` ステートメントの引数として指定された値。 任意の有効なエラー番号を指定できます。|  
|`Source`|現在の Visual Basic プロジェクトの名前。|  
|`Description`|指定した `Number` の `Error` 関数の戻り値に対応する文字列式 (この文字列が存在する場合)。 文字列が存在しない場合は、`Description` に長さゼロの文字列 ("") が格納されます。|  
|`HelpFile`|該当する Visual Basic ヘルプ ファイルの完全修飾ドライブ、パス、およびファイル名。|  
|`HelpContext`|`Number` プロパティに対応するエラーについての該当する Visual Basic ヘルプ ファイル コンテキスト ID。|  
|`LastDLLError`|ゼロ。|  
  
 エラー ハンドラーが存在しない場合、または有効なものがない場合は、`Err` オブジェクトのプロパティからエラーメッセージが作成され、表示されます。  
  
> [!NOTE]
> 一部の Visual Basic ホストアプリケーションでは、オブジェクトを作成できない場合があります。 ホスト アプリケーションでクラスとオブジェクトを作成できるかどうかを判断するには、そのドキュメントを参照してください。  
  
## <a name="example"></a>例  
 この例では、`Error` ステートメントを使用して、エラー番号 11 を生成しています。  
  
```vb  
On Error Resume Next   ' Defer error handling.  
Error 11   ' Simulate the "Division by zero" error.  
```  
  
## <a name="requirements"></a>必要条件  
 **名前空間:** [Microsoft.VisualBasic](../runtime-library-members.md)  
  
 **アセンブリ:** Visual Basic ランタイム ライブラリ (Microsoft.VisualBasic.dll)  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ErrObject.Clear%2A>
- <xref:Microsoft.VisualBasic.Information.Err%2A>
- <xref:Microsoft.VisualBasic.ErrObject.Raise%2A>
- [On Error ステートメント](on-error-statement.md)
- [Resume ステートメント](resume-statement.md)
- [エラー メッセージ](../error-messages/index.md)
