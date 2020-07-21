---
title: '方法: システム リソースを破棄する'
ms.date: 07/20/2015
helpviewer_keywords:
- Using statement [Visual Basic], disposing of system resources
- Visual Basic code, control flow
- system resources, disposing of
- resources [Visual Basic], disposing of system
- system resources
- Using statement [Visual Basic], Using...End Using
- Using block
ms.assetid: 8be2b239-8090-419b-8e7e-bcaa75b0ecc8
ms.openlocfilehash: dd15c6746628f45b072d46eea40051ed9afb7921
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403499"
---
# <a name="how-to-dispose-of-a-system-resource-visual-basic"></a>方法: システム リソースを破棄する (Visual Basic)
`Using` ブロックを使用すると、コードがこのブロックを終了するときに、リソースが必ず破棄されることを保証できます。 これは、大量のメモリを消費するシステム リソースを使用している場合、または、他のコンポーネントでもそのシステム リソースを使いたい場合に役立ちます。  
  
### <a name="to-dispose-of-a-database-connection-when-your-code-is-finished-with-it"></a>コードでの使用が済んだ時点でデータベース接続を破棄するには  
  
1. データベース接続用の適切な [Imports ステートメント (.NET名前空間と型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md) を、ソース ファイル (この場合は <xref:System.Data.SqlClient>) の先頭に必ず追加します。  
  
2. `Using` ステートメントと `End Using` ステートメントを使用して、`Using` ブロックを作成します。 ブロック内に、データベース接続を処理するコードを配置します。  
  
3. 接続を宣言し、そのインスタンスを `Using` ステートメントの一部として作成します。  
  
    ```vb  
    ' Insert the following line at the beginning of your source file.  
    Imports System.Data.SqlClient  
    Public Sub AccessSql(ByVal s As String)  
        Using sqc As New System.Data.SqlClient.SqlConnection(s)  
            MsgBox("Connected with string """ & sqc.ConnectionString & """")  
        End Using  
    End Sub  
    ```  
  
     ハンドルされていない例外のケースを含め、ブロックを終了する方法に関係なくリソースが破棄されます。  
  
     スコープがブロックに限定されているため、`Using` ブロック外から `sqc` にアクセスできないことに注意してください。  
  
     同じ手法を、ファイル ハンドルや COM ラッパーなどのシステム リソースでも使用できます。 `Using` ブロックは、`Using` ブロックを終了した後に、リソースを確実に他のコンポーネントで使用できるようにしたいときに使用します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Data.SqlClient.SqlConnection>
- [制御フロー](index.md)
- [条件判断構造](decision-structures.md)
- [ループ構造](loop-structures.md)
- [その他の制御構造](other-control-structures.md)
- [入れ子になった制御構造](nested-control-structures.md)
- [Using ステートメント](../../../language-reference/statements/using-statement.md)
