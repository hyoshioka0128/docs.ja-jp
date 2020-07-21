---
title: End ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.End
- End
helpviewer_keywords:
- execution [Visual Basic], ending
- files [Visual Basic], closing
- End keyword [Visual Basic], End statements
- programs [Visual Basic], quitting
- code, exiting
- program termination
- End statement [Visual Basic]
- execution [Visual Basic], stopping
ms.assetid: 0e64467c-0f34-4aab-9ddd-43f8b9d55d90
ms.openlocfilehash: fe17a82662c4014069c77f2da76723a051ab9084
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404707"
---
# <a name="end-statement"></a>End ステートメント
直ちに実行を終了します。  
  
## <a name="syntax"></a>構文  
  
```vb  
End  
```  
  
## <a name="remarks"></a>Remarks  
 プロシージャの任意の場所に `End` ステートメントを配置して、アプリケーション全体の実行を強制的に停止することができます。 `End` によって、`Open` ステートメントを使用して開いたファイルがすべて閉じられ、アプリケーションのすべての変数がクリアされます。 オブジェクトへの参照を保持している他のプログラムがなくなり、そのコードが実行されなくなると、アプリケーションはすぐに終了します。  
  
> [!NOTE]
> `End` ステートメントを使用すると、コードの実行は突然停止され、`Dispose` または `Finalize` メソッド、またはその他の Visual Basic コードは呼び出されません。 他のプログラムに保持されているオブジェクト参照は無効になります。 `Try` または `Catch` ブロック内に `End` ステートメントが存在すると、制御は対応する `Finally` ブロックには渡されません。  
  
 `Stop` ステートメントでは実行が中断されますが、`End` とは異なり、コンパイル済みの実行可能 (.exe) ファイルで検出されていない限り、ファイルを閉じたり、変数をクリアしたりしません。  
  
 `End` を使用すると、開いている可能性のあるリソースを処理することなくアプリケーションが終了するため、使用する前に完全に終了するようにします。 たとえば、アプリケーションでフォームを開いている場合は、コントロールが `End` ステートメントに到達する前にフォームを閉じる必要があります。  
  
 `End` は慎重に使用し、すぐに停止する必要がある場合にのみ使用してください。 プロシージャを終了する通常の方法 ([Return ステートメント](return-statement.md)と [Exit ステートメント](exit-statement.md)) では、プロシージャが完全に終了されるだけでなく、呼び出し元のコードにも正常に終了する機会が与えられます。 たとえば、コンソール アプリケーションでは、`Main` プロシージャから単に `Return` を実行できます。  
  
> [!IMPORTANT]
> `End` ステートメントを使用すると、<xref:System> 名前空間内の <xref:System.Environment> クラスの <xref:System.Environment.Exit%2A> メソッドが呼び出されます。 <xref:System.Environment.Exit%2A> を使用するには `UnmanagedCode` アクセス許可が必要です。 そうしないと、<xref:System.Security.SecurityException> エラーが発生します。  
  
 追加のキーワードが続く場合、[End \<keyword> ステートメント](end-keyword-statement.md)を使用して、適切なプロシージャまたはブロックの定義の終わりを示します。 たとえば、`End Function` を使用して `Function` プロシージャの定義を終了します。  
  
## <a name="example"></a>例  
 次の例では、`End` ステートメントを使用して、ユーザーから要求された場合にコードの実行を終了します。  
  
 [!code-vb[VbVersHelp60Controls#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVersHelp60Controls/VB/Form1.vb#64)]  
  
## <a name="smart-device-developer-notes"></a>スマート デバイス開発者向けのメモ  
 このステートメントはサポートされていません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Security.Permissions.SecurityPermissionFlag>
- [Stop ステートメント](stop-statement.md)
- [End \<keyword> ステートメント](end-keyword-statement.md)
