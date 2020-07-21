---
title: OracleDataReader を使用した複数の REF CURSOR からのデータの取得
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: 361e9bd4-447d-44b7-8629-3c11f1a7ffbb
ms.openlocfilehash: 8ece2617dd81161cb19a08d62f14d37c0f8c1f33
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149038"
---
# <a name="retrieving-data-from-multiple-ref-cursors-using-an-oracledatareader"></a>OracleDataReader を使用した複数の REF CURSOR からのデータの取得
この Microsoft Visual Basic の例では、2 つの REF CURSOR パラメーターを返し、<xref:System.Data.OracleClient.OracleDataReader> を使用して値を読み取る PL/SQL ストアド プロシージャを実行します。  
  
```vb  
Private Sub Button1_Click( _  
  ByVal sender As Object, ByVal e As System.EventArgs)  _  
  Handles Button1.Click  
  
  Dim connString As New String( _  
      "Data Source=Oracle9i;User ID=scott;Password=tiger;")  
  Using conn As New OracleConnection(connString)  
    Dim cmd As New OracleCommand()  
    Dim rdr As OracleDataReader  
  
    conn.Open()  
    cmd.Connection = conn  
    cmd.CommandText = "CURSPKG.OPEN_TWO_CURSORS"  
    cmd.CommandType = CommandType.StoredProcedure  
    cmd.Parameters.Add(New OracleParameter( _  
      "EMPCURSOR", OracleType.Cursor)).Direction = _  
      ParameterDirection.Output  
    cmd.Parameters.Add(New OracleParameter(_  
      "DEPTCURSOR", OracleType.Cursor)).Direction = _  
      ParameterDirection.Output  
  
    rdr = cmd.ExecuteReader(CommandBehavior.CloseConnection)  
    While (rdr.Read())  
        REM do something with the values from the EMP table
    End While  
  
    rdr.NextResult()  
    While (rdr.Read())  
        REM do something with the values from the DEPT table
    End While  
    rdr.Close()  
  End Using  
End Sub
```  
  
## <a name="see-also"></a>関連項目

- [Oracle REF CURSOR](oracle-ref-cursors.md)
- [ADO.NET の概要](ado-net-overview.md)
