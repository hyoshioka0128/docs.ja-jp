---
title: REF CURSOR の例
ms.date: 03/30/2017
ms.assetid: c257da03-c6c9-4cf8-b591-b7740a962c40
ms.openlocfilehash: dc82648ff5a565c9b4d6fa593433ee1e22249d93
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149136"
---
# <a name="ref-cursor-examples"></a>REF CURSOR の例
REF CURSOR の例は、REF CURSOR の使い方を説明する、次の 3 つの Microsoft Visual Basic の例によって構成されています。  
  
|サンプル|説明|  
|------------|-----------------|  
|[OracleDataReader の REF CURSOR パラメーター](ref-cursor-parameters-in-an-oracledatareader.md)|この例では、REF CURSOR パラメーターを返し、<xref:System.Data.OracleClient.OracleDataReader> として値を読み込む PL/SQL ストアド プロシージャを実行します。|  
|[OracleDataReader を使用した複数の REF CURSOR からのデータの取得](retrieving-data-from-multiple-ref-cursors.md)|この例では、2 つの REF CURSOR パラメーターを返し、**OracleDataReader** を使用して値を読み込む PL/SQL ストアド プロシージャを実行します。|  
|[1 つまたは複数の REF CURSOR を使用した DataSet の値の設定](filling-a-dataset-using-one-or-more-ref-cursors.md)|この例では、2 つの REF CURSOR パラメーターを返し、返された行を <xref:System.Data.DataSet> に入力する PL/SQL ストアド プロシージャを実行します。|  
  
 これらの例を使用するには、必要に応じて Oracle テーブルを作成し、さらに PL/SQL パッケージとパッケージ本体を作成する必要があります。  
  
## <a name="creating-the-oracle-tables"></a>Oracle テーブルの作成  
 これらの例では、Oracle Scott/Tiger スキーマで定義されたテーブルを使用します。 Oracle Scott/Tiger スキーマは、ほとんどの Oracle のインストールに含まれています。 このスキーマが含まれていない場合は、{OracleHome}\rdbms\admin\scott.sql にある SQL コマンド ファイルを使用して、これらの例で使用されているテーブルとインデックスを作成します。  
  
## <a name="creating-the-oracle-package-and-package-body"></a>Oracle パッケージとパッケージ本体の作成  
 これらの例では、次の PL/SQL パッケージとパッケージ本体がサーバー上に必要になります。 次の Oracle パッケージを Oracle サーバー上に作成します。  
  
```sql
CREATE OR REPLACE PACKAGE CURSPKG AS
    TYPE T_CURSOR IS REF CURSOR;
    PROCEDURE OPEN_ONE_CURSOR (N_EMPNO IN NUMBER,
                               IO_CURSOR IN OUT T_CURSOR);
    PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,
                                DEPTCURSOR OUT T_CURSOR);  
END CURSPKG;  
/
```  
  
 Oracle サーバーで、次の Oracle パッケージ本体を作成します。  
  
```sql
CREATE OR REPLACE PACKAGE BODY CURSPKG AS  
    PROCEDURE OPEN_ONE_CURSOR (N_EMPNO IN NUMBER,  
                               IO_CURSOR IN OUT T_CURSOR)  
    IS
        V_CURSOR T_CURSOR;
    BEGIN
        IF N_EMPNO <> 0
        THEN  
             OPEN V_CURSOR FOR
             SELECT EMP.EMPNO, EMP.ENAME, DEPT.DEPTNO, DEPT.DNAME
                  FROM EMP, DEPT
                  WHERE EMP.DEPTNO = DEPT.DEPTNO
                  AND EMP.EMPNO = N_EMPNO;  
  
        ELSE
             OPEN V_CURSOR FOR
             SELECT EMP.EMPNO, EMP.ENAME, DEPT.DEPTNO, DEPT.DNAME
                  FROM EMP, DEPT
                  WHERE EMP.DEPTNO = DEPT.DEPTNO;  
  
        END IF;  
        IO_CURSOR := V_CURSOR;
    END OPEN_ONE_CURSOR;
  
    PROCEDURE OPEN_TWO_CURSORS (EMPCURSOR OUT T_CURSOR,  
                                DEPTCURSOR OUT T_CURSOR)  
    IS
        V_CURSOR1 T_CURSOR;
        V_CURSOR2 T_CURSOR;
    BEGIN
        OPEN V_CURSOR1 FOR SELECT * FROM EMP;  
        OPEN V_CURSOR2 FOR SELECT * FROM DEPT;  
        EMPCURSOR  := V_CURSOR1;
        DEPTCURSOR := V_CURSOR2;
    END OPEN_TWO_CURSORS;
END CURSPKG;  
/  
```  
  
## <a name="see-also"></a>関連項目

- [Oracle REF CURSOR](oracle-ref-cursors.md)
- [ADO.NET の概要](ado-net-overview.md)
