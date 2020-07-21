---
title: Oracle BFILE
ms.date: 03/30/2017
ms.assetid: 341bbf84-4734-4d44-8723-ccedee954e21
ms.openlocfilehash: 40060a7ea8576e08140d972072d086606d640366
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149441"
---
# <a name="oracle-bfiles"></a>Oracle BFILE
.NET Framework Data Provider for Oracle には、<xref:System.Data.OracleClient.OracleBFile> クラスが含まれています。このクラスは、Oracle <xref:System.Data.OracleClient.OracleType.BFile> データ型で使用されます。  
  
 Oracle の **BFILE** データ型は、最大 4 GB までのバイナリ データへの参照を含む Oracle の **LOB** データ型です。 Oracle の **BFILE** は、データがサーバー上にではなくオペレーティング システムの物理ファイルに保存されるという点で、他の Oracle の **LOB** データ型と異なります。 **BFILE** データ型のデータ アクセスは読み取り専用であることに注意してください。  
  
 **LOB** データ型と異なる **BFILE** データ型のその他の特徴としては、次のものがあります。  
  
- 非構造化データの保持。  
  
- サーバー側チャンキングのサポート。  
  
- 参照コピーのセマンティクスの使用。 たとえば、**BFILE** 上でコピー操作を行う場合、ファイルへの参照である **BFILE** ロケーターだけがコピーされます。 ファイル内のデータはコピーされません。  
  
 **BFILE** データ型は、大きいサイズの LOB の参照用として使用してください。データベースへの保存には適しません。 **BFILE** データ型を使用すると、クライアント、サーバー、および通信において、**LOB** データ型よりも、いっそう多くのオーバーヘッドを必要とします。 少量のデータを取得するだけの場合は、**BFILE** へのアクセスがいっそう効果的です。 オブジェクト全体を取得したい場合は、データベースに常駐する LOB へのアクセスがいっそう効果的です。  
  
 NULL 以外の **OracleBFile** オブジェクトは、基になる物理ファイルの場所を定義する次の 2 つのエンティティに関連付けられます。  
  
1. Oracle DIRECTORY オブジェクト。ファイル システムのディレクトリに対するデータベースのエイリアスです。  
  
2. 基になる物理ファイルのファイル名。このファイルは、DIRECTORY オブジェクトに関連付けられたディレクトリに配置されています。  
  
## <a name="example"></a>例  
 次の C# の例では、Oracle テーブルに **BFILE** を作成し、**OracleBFile** オブジェクトの形式で取得する方法について説明します。 この例では、<xref:System.Data.OracleClient.OracleDataReader> オブジェクトと **OracleBFile** の **Seek** および **Read** メソッドを使用する方法について説明します。 このサンプルを使用するには、はじめに "c:\\\bfiles" というディレクトリと "MyFile.jpg" というファイルを Oracle サーバーに作成する必要があります。  
  
```csharp  
using System;  
using System.IO;  
using System.Data;  
using System.Data.OracleClient;  
  
public class Sample  
{  
   public static void Main(string[] args)  
   {  
      OracleConnection connection = new OracleConnection(  
        "Data Source=Oracle8i;Integrated Security=yes");  
      connection.Open();  
  
      OracleCommand command = connection.CreateCommand();  
      command.CommandText =
        "CREATE or REPLACE DIRECTORY MyDir as 'c:\\bfiles'";  
      command.ExecuteNonQuery();  
      command.CommandText =
        "DROP TABLE MyBFileTable";  
      try {  
        command.ExecuteNonQuery();  
      }  
      catch {  
      }  
      command.CommandText =
        "CREATE TABLE MyBFileTable(col1 number, col2 BFILE)";  
      command.ExecuteNonQuery();  
      command.CommandText =
        "INSERT INTO MyBFileTable values ('2', BFILENAME('MyDir', " +  
        "'MyFile.jpg'))";  
      command.ExecuteNonQuery();  
      command.CommandText = "SELECT * FROM MyBFileTable";  
  
        byte[] buffer = new byte[100];  
  
      OracleDataReader reader = command.ExecuteReader();  
      using (reader) {  
          if (reader.Read()) {  
                OracleBFile bFile = reader.GetOracleBFile(1);  
                using (bFile) {  
                  bFile.Seek(0, SeekOrigin.Begin);  
                  bFile.Read(buffer, 0, 100);  
              }  
          }  
      }  
  
      connection.Close();  
   }  
  
}  
```  
  
## <a name="see-also"></a>関連項目

- [Oracle および ADO.NET](oracle-and-adonet.md)
- [ADO.NET の概要](ado-net-overview.md)
