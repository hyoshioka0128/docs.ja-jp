---
ms.openlocfilehash: 3eab96149be1e40d528cfd552bbe05ca766cf4e8
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620270"
---
### <a name="systemthreadingtaskstask-no-longer-throw-objectdisposedexception-after-object-is-disposed"></a>System.Threading.Tasks.Task は、オブジェクトが破棄された後、ObjectDisposedException をスローしなくなりました

#### <a name="details"></a>説明

<xref:System.Threading.Tasks.Task.System%23IAsyncResult%23AsyncWaitHandle>を除き、<xref:System.Threading.Tasks.Task?displayProperty=fullName> メソッドでオブジェクトが破棄された後も <xref:System.ObjectDisposedException?displayProperty=fullName> の例外がスローされることがなくなりました。この変更により、キャッシュされたタスクを使用できるようになりました。 たとえば、メソッドで新しいタスクを割り当てる代わりに、既に完了した操作を表す、キャッシュされたタスクを返すことができます。 これは、タスクの任意のコンシューマーによって破棄されてしまうと、使用不可能になってしまう以前の .NET Framework のバージョンでは不可能でした。

#### <a name="suggestion"></a>提案される解決策

オブジェクトが破棄されたとき、Task メソッドが <xref:System.ObjectDisposedException?displayProperty=fullName> をスローしなくなったことに注意してください。 アプリが、タスクが破棄されたことを確認するために、この例外に依存していた場合は、<xref:System.Threading.Tasks.Task.Status> を使用してタスクのステータスを明示的に確認するように、アプリを更新する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム|
