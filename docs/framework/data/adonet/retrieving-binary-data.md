---
title: バイナリ データの取得
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 56c5a9e3-31f1-482f-bce0-ff1c41a658d0
ms.openlocfilehash: c914a9b0780e2e87e177502b0f9faff0e7c4b617
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149051"
---
# <a name="retrieving-binary-data"></a>バイナリ データの取得
既定では、データの行全体が使用可能になるとすぐに、**DataReader** によって受信データが行として読み込まれます。 バイナリ ラージ オブジェクト (BLOB) には、1 行に収まらない数ギガバイトのデータが含まれる場合があるため、別の処理が必要です。 **Command.ExecuteReader** メソッドには、<xref:System.Data.CommandBehavior> 引数を受け取って **DataReader** の既定の動作を変更するオーバーロードがあります。 **ExecuteReader** メソッドに <xref:System.Data.CommandBehavior.SequentialAccess> を渡すと、データの行を読み込む代わりに、データを受け取った時点で順次読み込むように、**DataReader** の既定の動作を変更できます。 これは BLOB やその他の大きなデータ構造を読み込む場合に理想的な処理です。 この動作は、データ ソースによって異なる場合があります。 たとえば、Microsoft Access から BLOB を返すと、受け取ったデータから順に読み込むのではなく、BLOB 全体をメモリに読み込みます。  
  
 **SequentialAccess** を使用するように **DataReader** を設定するときは、返されたフィールドにアクセスする順序に注意してください。 使用可能になるとすぐに行全体を読み込む **DataReader** の既定の動作では、次の行が読み取られるまでは、返されたフィールドに任意の順序でアクセスできます。 しかし、**SequentialAccess** を使用しているときは、**DataReader** によって返された各フィールドに順番にアクセスする必要があります。 たとえば、クエリが 3 つの列 (3 番目の列は BLOB) を返す場合、最初のフィールドおよび 2 番目のフィールドの値は、3 番目のフィールドの BLOB データにアクセスする前に返す必要があります。 最初のフィールドまたは 2 番目のフィールドの前に 3 番目のフィールドにアクセスした場合は、最初のフィールドと 2 番目のフィールドの値は使用できなくなります。 これは、**SequentialAccess** によって、**DataReader** はデータを順番に返すように変更されており、**DataReader** による読み取りが通過した後のデータは使用できなくなるためです。  
  
 BLOB フィールドのデータにアクセスするときは、**DataReader** の **GetBytes** 型または **GetChars** 型のアクセサーを使用します。これらのアクセサーでは、データは配列に設定されます。 文字データには **GetString** を使用することもできます。ただし、 システム リソースを節約するためには、BLOB 値全体を 1 つの文字列変数に読み込むことは望ましくありません。 特定のバッファー サイズのデータを返すように指定する代わりに、返されたデータから読み込む先頭バイトまたは先頭文字の開始位置を指定できます。 **GetBytes** と **GetChars** では、返されたバイト数または文字数を表す `long` 値が返されます。 **GetBytes** または **GetChars** に null 配列を渡した場合、返される long 値は BLOB の総バイト数または総文字数になります。 オプションで、データ読み込みの開始位置を示す、配列内のインデックスを指定できます。  
  
## <a name="example"></a>例  
 次の例では、Microsoft SQL Server の **pubs** サンプル データベースから、発行者 ID とロゴを取得します。 発行者 ID (`pub_id`) は文字フィールドであり、ロゴはイメージ、つまり、BLOB です。 **logo** フィールドはビットマップなので、この例では、**GetBytes** を使用してバイナリ データを返します。 フィールドには順番にアクセスする必要があるため、現在の行のデータに対して発行者 ID はロゴの前にアクセスされることに注意してください。  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim command As SqlCommand = New SqlCommand( _  
  "SELECT pub_id, logo FROM pub_info", connection)  
  
' Writes the BLOB to a file (*.bmp).  
Dim stream As FileStream
' Streams the binary data to the FileStream object.  
Dim writer As BinaryWriter
' The size of the BLOB buffer.  
Dim bufferSize As Integer = 100
' The BLOB byte() buffer to be filled by GetBytes.  
Dim outByte(bufferSize - 1) As Byte
' The bytes returned from GetBytes.  
Dim retval As Long
' The starting position in the BLOB output.  
Dim startIndex As Long = 0
  
' The publisher id to use in the file name.  
Dim pubID As String = ""
  
' Open the connection and read data into the DataReader.  
connection.Open()  
Dim reader As SqlDataReader = command.ExecuteReader(CommandBehavior.SequentialAccess)  
  
Do While reader.Read()  
  ' Get the publisher id, which must occur before getting the logo.  
  pubID = reader.GetString(0)  
  
  ' Create a file to hold the output.  
  stream = New FileStream( _  
    "logo" & pubID & ".bmp", FileMode.OpenOrCreate, FileAccess.Write)  
  writer = New BinaryWriter(stream)  
  
  ' Reset the starting byte for a new BLOB.  
  startIndex = 0  
  
  ' Read bytes into outByte() and retain the number of bytes returned.  
  retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize)  
  
  ' Continue while there are bytes beyond the size of the buffer.  
  Do While retval = bufferSize  
    writer.Write(outByte)  
    writer.Flush()  
  
    ' Reposition start index to end of the last buffer and fill buffer.  
    startIndex += bufferSize  
    retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize)  
  Loop  
  
  ' Write the remaining buffer.  
  writer.Write(outByte, 0 , retval - 1)  
  writer.Flush()  
  
  ' Close the output file.  
  writer.Close()  
  stream.Close()  
Loop  
  
' Close the reader and the connection.  
reader.Close()  
connection.Close()  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
SqlCommand command = new SqlCommand(  
  "SELECT pub_id, logo FROM pub_info", connection);  
  
// Writes the BLOB to a file (*.bmp).  
FileStream stream;
// Streams the BLOB to the FileStream object.  
BinaryWriter writer;
  
// Size of the BLOB buffer.  
int bufferSize = 100;
// The BLOB byte[] buffer to be filled by GetBytes.  
byte[] outByte = new byte[bufferSize];
// The bytes returned from GetBytes.  
long retval;
// The starting position in the BLOB output.  
long startIndex = 0;
  
// The publisher id to use in the file name.  
string pubID = "";
  
// Open the connection and read data into the DataReader.  
connection.Open();  
SqlDataReader reader = command.ExecuteReader(CommandBehavior.SequentialAccess);  
  
while (reader.Read())  
{  
  // Get the publisher id, which must occur before getting the logo.  
  pubID = reader.GetString(0);
  
  // Create a file to hold the output.  
  stream = new FileStream(  
    "logo" + pubID + ".bmp", FileMode.OpenOrCreate, FileAccess.Write);  
  writer = new BinaryWriter(stream);  
  
  // Reset the starting byte for the new BLOB.  
  startIndex = 0;  
  
  // Read bytes into outByte[] and retain the number of bytes returned.  
  retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize);  
  
  // Continue while there are bytes beyond the size of the buffer.  
  while (retval == bufferSize)  
  {  
    writer.Write(outByte);  
    writer.Flush();  
  
    // Reposition start index to end of last buffer and fill buffer.  
    startIndex += bufferSize;  
    retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize);  
  }  
  
  // Write the remaining buffer.  
  writer.Write(outByte, 0, (int)retval);  
  writer.Flush();  
  
  // Close the output file.  
  writer.Close();  
  stream.Close();  
}  
  
// Close the reader and the connection.  
reader.Close();  
connection.Close();  
```  
  
## <a name="see-also"></a>関連項目

- [SQL Server のバイナリ データと大きな値のデータ](./sql/sql-server-binary-and-large-value-data.md)
- [ADO.NET の概要](ado-net-overview.md)
