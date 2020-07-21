---
title: SyncLock ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.SyncLock
- SyncLock
helpviewer_keywords:
- threading [Visual Basic], locks
- SyncLock statement [Visual Basic]
- locks, threads
ms.assetid: 14501703-298f-4d43-b139-c4b6366af176
ms.openlocfilehash: fd932a20af274faf2b56136a94675b28399989b8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404162"
---
# <a name="synclock-statement"></a>SyncLock ステートメント
ブロックを実行する前に、ステートメント ブロックの排他ロックを取得します。  
  
## <a name="syntax"></a>構文  
  
```vb  
SyncLock lockobject  
    [ block ]  
End SyncLock  
```  
  
## <a name="parts"></a>指定項目  
 `lockobject`  
 必須です。 オブジェクト参照として評価される式。  
  
 `block`  
 任意。 ロックが取得されたときに実行されるステートメントのブロック。  
  
 `End SyncLock`  
 `SyncLock` ブロックを終了します。  
  
## <a name="remarks"></a>Remarks  
 `SyncLock` ステートメントは、複数のスレッドがステートメント ブロックを同時に実行しないようにします。 `SyncLock` は、ブロックを実行する他のスレッドがなくなるまで、各スレッドがそのブロックに入らないようにします。  
  
 `SyncLock` の最も一般的な使用方法は、複数のスレッドによってデータが同時に更新されないようにすることです。 データを操作するステートメントが中断せずに完了する必要がある場合は、`SyncLock` ブロック内に配置します。  
  
 排他ロックによって保護されているステートメント ブロックは、*クリティカル セクション*と呼ばれることもあります。  
  
## <a name="rules"></a>ルール  
  
- 分岐。 ブロック外から `SyncLock` ブロックに分岐することはできません。  
  
- ロック オブジェクトの値。 `lockobject` の値を `Nothing` にすることはできません。 `SyncLock` ステートメントで使用する前に、ロック オブジェクトを作成する必要があります。  
  
     `SyncLock` ブロックの実行中に `lockobject` の値を変更することはできません。 このメカニズムでは、ロック オブジェクトが変更されないようにする必要があります。  
  
- `SyncLock` ブロックで [Await](../operators/await-operator.md) 演算子を使用することはできません。  
  
## <a name="behavior"></a>動作  
  
- メカニズム。 スレッドが `SyncLock` ステートメントに達すると、`lockobject` 式が評価され、式によって返されたオブジェクトの排他ロックを取得するまで実行が中断されます。 別のスレッドが `SyncLock` ステートメントに達すると、最初のスレッドが `End SyncLock` ステートメントを実行するまでロックは取得されません。  
  
- 保護されたデータ。 `lockobject` が `Shared` 変数の場合は、排他ロックによって、クラスのインスタンス内のスレッドが、他のスレッドが実行している間は `SyncLock` ブロックを実行できなくなります。 これにより、すべてのインスタンス間で共有されているデータが保護されます。  
  
     `lockobject` がインスタンス変数 (`Shared` ではなく) の場合は、ロックにより、現在のインスタンスで実行されているスレッドが、同じインスタンス内の別のスレッドと同時に `SyncLock` ブロックを実行できなくなります。 これにより、個々のインスタンスによって保持されるデータが保護されます。  
  
- 取得と解放。 `SyncLock` ブロックは、`Try` ブロックが `lockobject` に対して排他ロックを取得する `Try...Finally` コンストラクションと同様に動作し、`Finally` ブロックによって解放されます。 このため、`SyncLock` ブロックは、ブロックを終了する方法に関係なく、ロックの解放を保証します。 これは、ハンドルされない例外が発生した場合でも当てはまります。  
  
- フレームワークの呼び出し。 `SyncLock` ブロックは、<xref:System.Threading> 名前空間の `Monitor` クラスの `Enter` および `Exit` メソッドを呼び出すことによって、排他ロックを取得したり解放したりします。  
  
## <a name="programming-practices"></a>プログラミング プラクティス  
 `lockobject` 式は、常に、クラスに排他的に属しているオブジェクトに評価される必要があります。 現在のインスタンスに属するデータを保護するには `Private` オブジェクト変数を宣言し、すべてのインスタンスに共通のデータを保護するには `Private Shared` オブジェクト変数を宣言する必要があります。  
  
 インスタンス データ用のロック オブジェクトを指定するために、`Me` キーワードを使用しないでください。 クラスの外部のコードにクラスのインスタンスへの参照が含まれている場合、その参照を、ユーザーのものとはまったく異なる `SyncLock` ブロックのロック オブジェクトとして使用して、さまざまなデータを保護することができます。 このようにして、ユーザーのクラスとその他のクラスは、関連付けられていない `SyncLock` ブロックの実行を互いにブロックできます。 同様に、文字列のロックも問題になる可能性があります。同じ文字列を使用するコードがプロセス内に他にも存在した場合、そのコードも同じロックを共有するためです。  
  
 また、共有データのロック オブジェクトを指定するために、`Me.GetType` メソッドを使用しないでください。 これは、`GetType` は常に、指定されたクラス名に対して同じ `Type` オブジェクトを返すためです。 外部コードは、クラスで `GetType` を呼び出し、使用しているものと同じロック オブジェクトを取得することができます。 これにより、2 つのクラスが `SyncLock` ブロックから互いにブロックされることになります。  
  
## <a name="examples"></a>使用例  
  
### <a name="description"></a>説明  
 次の例では、メッセージの単純なリストを保持するクラスを示します。 これは、メッセージを配列内に保持し、その配列の最後に使用された要素を変数に保持します。 `addAnotherMessage` プロシージャは、最後の要素をインクリメントし、新しいメッセージを格納します。 これら 2 つの操作は、`SyncLock` および `End SyncLock` ステートメントによって保護されます。最後の要素がインクリメントされた後、他のすべてのスレッドが最後の要素を再度インクリメントできるようになる前に、新しいメッセージが格納される必要があるためです。  
  
 `simpleMessageList` クラスがそのすべてのインスタンス間で 1 つのメッセージ リストを共有している場合、変数 `messagesList` および `messagesLast` は `Shared` として宣言されます。 この場合、変数 `messagesLock` も `Shared` にして、すべてのインスタンスで 1 つのロック オブジェクトが使用されるようにする必要があります。  
  
### <a name="code"></a>コード  
 [!code-vb[VbVbalrThreading#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrThreading/VB/Class1.vb#1)]  
  
### <a name="description"></a>説明  
 次の例では、スレッドと `SyncLock` を使用しています。 `SyncLock` ステートメントが存在する限り、このステートメント ブロックはクリティカル セクションとなり、`balance` が負の数になることはありません。 `SyncLock` および `End SyncLock` ステートメントをコメント アウトして、`SyncLock` キーワードを残すことによる影響を確認できます。  
  
### <a name="code"></a>コード  
 [!code-vb[VbVbalrThreading#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrThreading/VB/class2.vb#21)]  
  
### <a name="comments"></a>コメント  
  
## <a name="see-also"></a>関連項目

- <xref:System.Threading.Monitor?displayProperty=nameWithType>
- <xref:System.Threading.Interlocked?displayProperty=nameWithType>
- [同期プリミティブの概要](../../../standard/threading/overview-of-synchronization-primitives.md)
