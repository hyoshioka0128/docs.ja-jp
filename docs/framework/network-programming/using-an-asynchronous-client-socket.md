---
title: 非同期クライアント ソケットの使用
description: この例では、非同期クライアント ソケットを示しています。 .NET Framework 非同期プログラミングでは、接続の処理中もアプリケーションの実行を続行できます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- sending data, sockets
- data requests, sockets
- asynchronous client sockets
- Socket class, asynchronous client sockets
- requesting data from Internet, sockets
- sockets, asynchronous client sockets
- receiving data, sockets
- protocols, sockets
- Internet, sockets
- client sockets
ms.assetid: fd85bc88-e06c-467d-a30d-9fd7cffcfca1
ms.openlocfilehash: 9cf46e9519bcecf4d7a20ff99b86fa5f66af2087
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502042"
---
# <a name="using-an-asynchronous-client-socket"></a>非同期クライアント ソケットの使用
ネットワーク操作が完了するまで待機している間、非同期クライアント ソケットはアプリケーションを一時停止しません。 標準の .NET Framework 非同期プログラミング モデルを使用して、1 つのスレッドでネットワーク接続を処理しながら、アプリケーションは元のスレッドで実行を継続します。 ネットワークの使用量が多いアプリケーションや、ネットワーク操作が完了するのを待機してから完了することができないアプリケーションの場合、非同期ソケットが適しています。  
  
 非同期メソッドの場合、<xref:System.Net.Sockets.Socket> クラスは .NET Framework の名前付けパターンに従います。たとえば、同期の <xref:System.Net.Sockets.Socket.Receive%2A> メソッドは非同期の <xref:System.Net.Sockets.Socket.BeginReceive%2A> メソッドと <xref:System.Net.Sockets.Socket.EndReceive%2A> メソッドに対応します。  
  
 非同期操作には、操作の結果を返すコールバック メソッドが必要です。 結果を知る必要がないアプリケーションの場合、コールバック メソッドは必要ありません。 このセクションのコード例では、ネットワーク デバイスへの接続を開始するメソッドと接続を完了するコールバック メソッド、データの送信を開始するメソッドと送信を完了するコールバック メソッド、およびデータの受信を開始するメソッドとデータの受信を終了するコールバック メソッドの使用方法を説明します。  
  
 非同期ソケットは、システム スレッド プールの複数のスレッドを使用して、ネットワーク接続を処理します。 1 つのスレッドは、データの送信または受信の開始を担当し、他のスレッドは、ネットワーク デバイスへの接続を完了し、データを送信または受信します。 以下の例では、<xref:System.Threading.ManualResetEvent?displayProperty=nameWithType> クラスのインスタンスを使用してメイン スレッドの実行を停止し、実行を続行できるようになったらシグナルを送ります。  
  
 次の例では、非同期ソケットをネットワーク デバイスに接続するために、`Connect` メソッドで **Socket** を開始してから <xref:System.Net.Sockets.Socket.Connect%2A?displayProperty=nameWithType> メソッドを呼び出し、ネットワーク デバイスを表すリモート エンドポイント、connect のコールバック メソッド、および状態オブジェクト (クライアントの **Socket**) を渡します。このオブジェクトは、非同期呼び出しの間で状態を渡すために使用されます。 この例では、指定した **Socket** を指定したエンドポイントに接続する `Connect` メソッドを実装します。 `connectDone` というグローバル **ManualResetEvent** があるとします。  
  
```vb  
Public Shared Sub Connect(remoteEP As EndPoint, client As Socket)  
    client.BeginConnect(remoteEP, _  
       AddressOf ConnectCallback, client)  
  
    connectDone.WaitOne()  
End Sub 'Connect  
```  
  
```csharp  
public static void Connect(EndPoint remoteEP, Socket client) {  
    client.BeginConnect(remoteEP,
        new AsyncCallback(ConnectCallback), client );  
  
   connectDone.WaitOne();  
}  
```  
  
 connect のコールバック メソッド `ConnectCallback` は <xref:System.AsyncCallback> デリゲートを実装します。 リモート デバイスが使用できるようになるとリモート デバイスに接続してから、**ManualResetEvent** `connectDone` を設定して接続が完了したというシグナルをアプリケーションのスレッドに送ります。 次のコードでは、`ConnectCallback` メソッドを実装します。  
  
```vb  
Private Shared Sub ConnectCallback(ar As IAsyncResult)  
    Try  
        ' Retrieve the socket from the state object.  
        Dim client As Socket = CType(ar.AsyncState, Socket)  
  
        ' Complete the connection.  
        client.EndConnect(ar)  
  
        Console.WriteLine("Socket connected to {0}", _  
            client.RemoteEndPoint.ToString())  
  
        ' Signal that the connection has been made.  
        connectDone.Set()  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'ConnectCallback  
```  
  
```csharp  
private static void ConnectCallback(IAsyncResult ar) {  
    try {  
        // Retrieve the socket from the state object.  
        Socket client = (Socket) ar.AsyncState;  
  
        // Complete the connection.  
        client.EndConnect(ar);  
  
        Console.WriteLine("Socket connected to {0}",  
            client.RemoteEndPoint.ToString());  
  
        // Signal that the connection has been made.  
        connectDone.Set();  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
 例のメソッド `Send` は指定した文字列データを ASCII 形式でエンコードし、指定したソケットが示すネットワーク デバイスに非同期に送信します。 次の例では、`Send` メソッドを実装します。  
  
```vb  
Private Shared Sub Send(client As Socket, data As [String])  
    ' Convert the string data to byte data using ASCII encoding.  
    Dim byteData As Byte() = Encoding.ASCII.GetBytes(data)  
  
    ' Begin sending the data to the remote device.  
    client.BeginSend(byteData, 0, byteData.Length, SocketFlags.None, _  
        AddressOf SendCallback, client)  
End Sub 'Send  
```  
  
```csharp  
private static void Send(Socket client, String data) {  
    // Convert the string data to byte data using ASCII encoding.  
    byte[] byteData = Encoding.ASCII.GetBytes(data);  
  
    // Begin sending the data to the remote device.  
    client.BeginSend(byteData, 0, byteData.Length, SocketFlags.None,  
        new AsyncCallback(SendCallback), client);  
}  
```  
  
 send のコールバック メソッド `SendCallback` は <xref:System.AsyncCallback> デリゲートを実装します。 ネットワーク デバイスに受信する準備が整ったらデータを送信します。 次の例では、`SendCallback` メソッドを実装します。 `sendDone` というグローバル **ManualResetEvent** があるとします。  
  
```vb  
Private Shared Sub SendCallback(ar As IAsyncResult)  
    Try  
        ' Retrieve the socket from the state object.  
        Dim client As Socket = CType(ar.AsyncState, Socket)  
  
        ' Complete sending the data to the remote device.  
        Dim bytesSent As Integer = client.EndSend(ar)  
        Console.WriteLine("Sent {0} bytes to server.", bytesSent)  
  
        ' Signal that all bytes have been sent.  
        sendDone.Set()  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'SendCallback  
```  
  
```csharp  
private static void SendCallback(IAsyncResult ar) {  
    try {  
        // Retrieve the socket from the state object.  
        Socket client = (Socket) ar.AsyncState;  
  
        // Complete sending the data to the remote device.  
        int bytesSent = client.EndSend(ar);  
        Console.WriteLine("Sent {0} bytes to server.", bytesSent);  
  
        // Signal that all bytes have been sent.  
        sendDone.Set();  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
 クライアント ソケットからデータを読み取るには、非同期呼び出しの間で値を渡す状態オブジェクトが必要です。 次のクラスは、クライアント ソケットからデータを受信する状態オブジェクトの例です。 クライアント ソケットのフィールド、受信したデータのバッキング フィールド、受信データ文字列を保持する <xref:System.Text.StringBuilder> が含まれています。 これらのフィールドを状態オブジェクトに格納することで、複数の呼び出し間で値を保持し、クライアント ソケットからデータ読み取ることができます。  
  
```vb  
Public Class StateObject  
    ' Client socket.  
    Public workSocket As Socket = Nothing
    ' Size of receive buffer.  
    Public BufferSize As Integer = 256  
    ' Receive buffer.  
    Public buffer(256) As Byte
    ' Received data string.  
    Public sb As New StringBuilder()  
End Class 'StateObject  
```  
  
```csharp  
public class StateObject {  
    // Client socket.  
    public Socket workSocket = null;  
    // Size of receive buffer.  
    public const int BufferSize = 256;  
    // Receive buffer.  
    public byte[] buffer = new byte[BufferSize];  
    // Received data string.  
    public StringBuilder sb = new StringBuilder();  
}  
```  
  
 例の `Receive` メソッドは、状態オブジェクトを設定してから、**BeginReceive** メソッドを呼び出してクライアント ソケットからデータを非同期に読み取ります。 `Receive` メソッドを実装する例を次に示します。  
  
```vb  
Private Shared Sub Receive(client As Socket)  
    Try  
        ' Create the state object.  
        Dim state As New StateObject()  
        state.workSocket = client  
  
        ' Begin receiving the data from the remote device.  
        client.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
            AddressOf ReceiveCallback, state)  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'Receive  
```  
  
```csharp  
private static void Receive(Socket client) {  
    try {  
        // Create the state object.  
        StateObject state = new StateObject();  
        state.workSocket = client;  
  
        // Begin receiving the data from the remote device.  
        client.BeginReceive( state.buffer, 0, StateObject.BufferSize, 0,  
            new AsyncCallback(ReceiveCallback), state);  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
 receive のコールバック メソッド `ReceiveCallback` は **AsyncCallback** デリゲートを実装します。 このコールバック メソッドはネットワーク デバイスからデータを受信し、メッセージ文字列を構築します。 また、ネットワークからデータ バッファーに 1 から数バイトのデータを読み取ってから、クライアントから送信されたデータが完了するまで、**BeginReceive** メソッドを再び呼び出します。 クライアントからすべてのデータを読み取ると、`ReceiveCallback` は **ManualResetEvent** `sendDone` を設定することで、データが完了したというシグナルをアプリケーション スレッドに送ります。  
  
 次のコード例では、`ReceiveCallback` メソッドを実装します。 受け取った文字列を保持する `response` というグローバル文字列と、`receiveDone` というグローバル **ManualResetEvent** があります。 ネットワーク セッションを正常に終了するには、サーバーがクライアント ソケットをシャットダウンする必要があります。  
  
```vb  
Private Shared Sub ReceiveCallback(ar As IAsyncResult)  
    Try  
        ' Retrieve the state object and the client socket
        ' from the asynchronous state object.  
        Dim state As StateObject = CType(ar.AsyncState, StateObject)  
        Dim client As Socket = state.workSocket  
  
        ' Read data from the remote device.  
        Dim bytesRead As Integer = client.EndReceive(ar)  
  
        If bytesRead > 0 Then  
            ' There might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(state.buffer, 0, _  
                bytesRead))  
  
            '  Get the rest of the data.  
            client.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
                AddressOf ReceiveCallback, state)  
        Else  
            ' All the data has arrived; put it in response.  
            If state.sb.Length > 1 Then  
                response = state.sb.ToString()  
            End If  
            ' Signal that all bytes have been received.  
            receiveDone.Set()  
        End If  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'ReceiveCallback  
```  
  
```csharp  
private static void ReceiveCallback( IAsyncResult ar ) {  
    try {  
        // Retrieve the state object and the client socket
        // from the asynchronous state object.  
        StateObject state = (StateObject) ar.AsyncState;  
        Socket client = state.workSocket;  
        // Read data from the remote device.  
        int bytesRead = client.EndReceive(ar);  
        if (bytesRead > 0) {  
            // There might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(state.buffer,0,bytesRead));  
                //  Get the rest of the data.  
            client.BeginReceive(state.buffer,0,StateObject.BufferSize,0,  
                new AsyncCallback(ReceiveCallback), state);  
        } else {  
            // All the data has arrived; put it in response.  
            if (state.sb.Length > 1) {  
                response = state.sb.ToString();  
            }  
            // Signal that all bytes have been received.  
            receiveDone.Set();  
        }  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
## <a name="see-also"></a>関連項目

- [同期クライアント ソケットの使用](using-a-synchronous-client-socket.md)
- [リッスン (ソケットで)](listening-with-sockets.md)
- [非同期クライアント ソケットの例](asynchronous-client-socket-example.md)
