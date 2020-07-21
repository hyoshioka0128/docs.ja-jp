---
title: HTTP、TCP、または名前付きパイプを使用した非同期シナリオ
ms.date: 03/30/2017
ms.assetid: a4d62402-43a4-48a4-9ced-220633ebc4ce
ms.openlocfilehash: 6ae96c0aac5010adf37eb78ed57d1549885ece58
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185782"
---
# <a name="asynchronous-scenarios-using-http-tcp-or-named-pipe"></a>HTTP、TCP、または名前付きパイプを使用した非同期シナリオ
ここでは、マルチスレッド要求で HTTP、TCP、または名前付きパイプを使用したときの、さまざまな非同期要求/応答シナリオでのアクティビティおよび転送について説明します。  
  
## <a name="asynchronous-requestreply-without-errors"></a>エラーを伴わない非同期要求/応答  
 ここでは、マルチスレッド クライアントを使用したときの、非同期要求/応答シナリオでのアクティビティおよび転送について説明します。  
  
 呼び出し元アクティビティは、`beginCall` が返され、`endCall` が返されると終了します。 コールバックが呼び出されたときは、そのコールバックが返されます。  
  
 呼び出されたアクティビティは、`beginCall` が返され、`endCall` が返されると終了します。または、そのアクティビティからコールバックが呼び出された場合は、コールバックが返されると終了します。  
  
### <a name="asynchronous-client-without-callback"></a>コールバックを伴わない非同期クライアント  
  
#### <a name="propagation-is-enabled-on-both-sides-using-http"></a>HTTP を使用して、両方の側で伝達が有効になっている場合  
 ![propagateActivity が両側で true に設定されているコールバックのない非同期クライアント。](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-client-no-callback.gif)
  
 の`propagateActivity=true`場合、プロセス メッセージは、転送先のプロセス アクション アクティビティを示します。  
  
 HTTP ベースのシナリオでは、最初に送信するメッセージで "バイトを受信" が呼び出され、要求の有効期間だけ存在します。  
  
#### <a name="propagation-is-disabled-on-either-sides-using-http"></a>HTTP を使用して、両方の側で伝達が無効になっている場合  
 どちらの`propagateActivity=false`側でも、ProcessMessage はどのプロセスアクションアクティビティを転送するかを示しません。 したがって、新しい ID を使用して、新しい一時的な "アクションを処理" アクティビティが呼び出されます。 非同期応答と ServiceModel コード内の要求が一致する場合は、アクティビティ ID をローカル コンテキストから取得できます。 その ID を使用して、実際の "アクションを処理" アクティビティに転送できます。  
  
 ![propagateActivity がどちらの側でも false に設定されているコールバックのない非同期クライアント。](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-scenario-propagation-disabled-either-side.gif)  

 HTTP ベースのシナリオでは、最初に送信するメッセージで "バイトを受信" が呼び出され、要求の有効期間だけ存在します。  
  
 プロセス アクション アクティビティは、呼び出し`propagateActivity=false`元または呼び出し先で、応答メッセージに Action ヘッダーが含まれていない場合に、非同期クライアントで作成されます。  
  
#### <a name="propagation-is-enabled-on-both-sides-using-tcp-or-named-pipe"></a>TCP または名前付きパイプを使用して、両方の側で伝達が有効になっている場合  
 ![propagateActivity が両側と名前付きパイプ/TCP のどちらで true に設定されているコールバックを持たない非同期クライアント。](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-scenario-propagation-enabled-using-tcp.gif)  
  
 名前付きパイプまたは TCP ベースのシナリオでは、クライアントが開かれるときに "バイトを受信" が呼び出され、接続の有効期間だけ存在します。  
  
 最初のイメージと同様に、 `propagateActivity=true`if を指定すると、ProcessMessage はどのプロセスアクションアクティビティを転送するかを示します。  
  
#### <a name="propagation-is-disabled-on-either-sides-using-tcp-or-named-pipe"></a>TCP または名前付きパイプを使用して、両方の側で伝達が無効になっている場合  
 名前付きパイプまたは TCP ベースのシナリオでは、クライアントが開かれるときに "バイトを受信" が呼び出され、接続の有効期間だけ存在します。  
  
 2 番目のイメージと同様`propagateActivity=false`に、どちらの側でも ProcessMessage は、どの ProcessAction アクティビティを転送するかを示しません。 したがって、新しい ID を使用して、新しい一時的な "アクションを処理" アクティビティが呼び出されます。 非同期応答と ServiceModel コード内の要求が一致する場合は、アクティビティ ID をローカル コンテキストから取得できます。 その ID を使用して、実際の "アクションを処理" アクティビティに転送できます。  
  
 ![propagateActivity がどちらの側でも、名前付きパイプ/TCP 側でも false に設定されているコールバックのない非同期クライアント。](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-scenario-propagation-disabled-using-tcp.gif)  

### <a name="asynchronous-client-with-callback"></a>コールバックを伴う非同期クライアント  
 このシナリオでは、コールバックと `endCall` に対するアクティビティ G と A’、およびその転送 (送受信) が追加されています。  
  
 このセクションでは、 で HTTP`propagateActivity`=`true`を使用する方法のみを示します。 ただし、追加のアクティビティと転送は、他の場合にも適用されます (つまり`propagateActivity`=`false`、TCP または名前付きパイプを使用)。  
  
 クライアントがユーザー コードを呼び出して結果の準備が完了したことを通知すると、コールバックは新しいアクティビティ (G) を作成します。 ユーザー コードは、次に、コールバック内 (図 5 を参照) またはコールバック外 (図 6 を参照) で `endCall` を呼び出します。 どのユーザー アクティビティ`endCall`が呼び出されたかは不明であるため、このアクティビティには`A’`というラベルが付けられます。 A’ と A が同じである場合もありますし、異なる場合もあります。  
  
 ![コールバック、コールバックのエンドコールを持つ非同期クライアントを示します。](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-client-callback-endcall-in-callback.gif)  

 ![コールバック、コールバックの外部呼び出しを含む非同期クライアントを示します。](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-client-callback-endcall-outside-callback.gif)  

### <a name="asynchronous-server-with-callback"></a>コールバックを伴う非同期サーバー  
 ![コールバックを使用して非同期サーバーを表示します。](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-server-callback.gif)  

 チャネル スタックは、"メッセージを受信" でクライアントをコールバックします。この処理のトレースは、"要求を処理" アクティビティ自体で出力されます。  
  
## <a name="asynchronous-requestreply-with-errors"></a>エラーを伴う非同期要求/応答  
 エラー メッセージは、`endCall` 中に受信されます。 この点を除き、アクティビティおよび転送は前のシナリオと同様です。  
  
## <a name="asynchronous-one-way-with-or-without-errors"></a>エラーを伴う/伴わない非同期一方向要求/応答  
 クライアントに返される応答やエラーはありません。
