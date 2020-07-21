---
title: オブジェクトの状態と変更の追跡
ms.date: 03/30/2017
ms.assetid: 7a808b00-9c3c-479a-aa94-717280fefd71
ms.openlocfilehash: a9df200f4d2e5f64bf5883c7bc513ba7129dcaad
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781275"
---
# <a name="object-states-and-change-tracking"></a>オブジェクトの状態と変更の追跡

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] オブジェクトは常に、いずれかの "*状態*" にあります。 たとえば、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] が新しいオブジェクトを作成すると、そのオブジェクトは `Unchanged` 状態です。 ユーザーが作成する新しいオブジェクトは <xref:System.Data.Linq.DataContext> にとって不明であり、`Untracked` 状態です。 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> が正常に実行されると、すべてのオブジェクトが [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] にとって既知となり、`Unchanged` 状態になります  (データベースから削除されたオブジェクトは例外です。これは `Deleted` 状態であり、<xref:System.Data.Linq.DataContext> インスタンスの中で使用できません)。

## <a name="object-states"></a>オブジェクトの状態

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] オブジェクトで有効な状態を次の表に示します。

|状態|説明|
|-----------|-----------------|
|`Untracked`|[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって追跡されないオブジェクト。 具体的には次のものがあります。<br /><br /> -   現在の <xref:System.Data.Linq.DataContext> を通じて照会されないオブジェクト (新規作成されたオブジェクトなど)。<br />-   逆シリアル化を通じて作成されたオブジェクト<br />-   異なる <xref:System.Data.Linq.DataContext> を通じて照会されるオブジェクト。|
|`Unchanged`|現在の <xref:System.Data.Linq.DataContext> を使用して取得され、作成後に変更された履歴がないオブジェクト。|
|`PossiblyModified`|<xref:System.Data.Linq.DataContext> に "*アタッチ*" されているオブジェクト。 詳細については、「[N 層アプリケーションでのデータ取得および CUD 操作 (LINQ to SQL)](data-retrieval-and-cud-operations-in-n-tier-applications.md)」を参照してください。|
|`ToBeInserted`|現在の <xref:System.Data.Linq.DataContext> を使用して取得されていないオブジェクト。 この場合、`INSERT` 中にデータベースの <xref:System.Data.Linq.DataContext.SubmitChanges%2A> が発生します。|
|`ToBeUpdated`|取得後に変更された履歴があるオブジェクト。 この場合、`UPDATE` 中にデータベースの <xref:System.Data.Linq.DataContext.SubmitChanges%2A> が発生します。|
|`ToBeDeleted`|削除がマークされているオブジェクト。`DELETE` 中にデータベースの <xref:System.Data.Linq.DataContext.SubmitChanges%2A> が発生します。|
|`Deleted`|データベース内で削除されたオブジェクト。 これは最後の状態であり、次の状態に移行できません。|

## <a name="inserting-objects"></a>オブジェクトの挿入

`Inserts` を使用して、<xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> を明示的に要求できます。 または、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、更新する必要がある既知のオブジェクトの 1 つに接続しているオブジェクトを見つけることによって、`Inserts` を推論できます。 たとえば、`Untracked` オブジェクトを <xref:System.Data.Linq.EntitySet%601> に追加するか、<xref:System.Data.Linq.EntityRef%601> を `Untracked` オブジェクトに設定すると、グラフ内の追跡オブジェクトを通じて、`Untracked` オブジェクトにアクセスできるようになります。 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> の実行中、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は追跡オブジェクトをスキャンして、追跡されていないアクセス可能な永続オブジェクトを見つけます。 このようなオブジェクトは、データベースへの挿入候補です。

また、継承階層内のクラスの場合、<xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> (`o`) は、"*識別子*" として指定されているメンバーの値が、オブジェクト `o` の型に一致するように設定します。 既定の識別子の値の型が一致する場合、この操作によって、識別子の値が既定値で上書きされます。 詳細については、「[継承のサポート](inheritance-support.md)」を参照してください。

> [!IMPORTANT]
> `Table` に追加されたオブジェクトは、ID キャッシュにはありません。 ID キャッシュは、データベースから取得されたもののみを反映します。 <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A> を呼び出した後、<xref:System.Data.Linq.DataContext.SubmitChanges%2A> が正常終了するまで、追加されたエンティティはデータベースに対するクエリで使用されません。

## <a name="deleting-objects"></a>オブジェクトの削除

適切な `o` で <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>(o) を呼び出すことにより、追跡オブジェクト <xref:System.Data.Linq.Table%601> に削除のマークを付けることができます。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、<xref:System.Data.Linq.EntitySet%601> からのオブジェクトの削除は更新操作と見なされ、対応する外部キー値は null に設定されます。 操作の対象 (`o`) はテーブルから削除されません。 たとえば、`cust.Orders.DeleteOnSubmit(ord)` は、外部キー `cust` を null に設定することによって `ord` と `ord.CustomerID` のリレーションシップが切断される更新を表します。 `ord` に対応する行の削除は行われません。

テーブルからオブジェクトを削除すると (<xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A>)、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって次の処理が実行されます。

- <xref:System.Data.Linq.DataContext.SubmitChanges%2A> を呼び出すときに、そのオブジェクトに対して `DELETE` 操作が実行されます。

- 関連オブジェクトが読み込まれているかどうかにかかわらず、関連オブジェクトに削除は反映されません。 特に、リレーションシップ プロパティを更新するために関連オブジェクトが読み込まれることはありません。

- <xref:System.Data.Linq.DataContext.SubmitChanges%2A> が正常に実行されると、オブジェクトは `Deleted` 状態に設定されます。 その結果、その `id` で、オブジェクトまたはその <xref:System.Data.Linq.DataContext> を使用することはできません。 データベース内でオブジェクトが削除された後でも、<xref:System.Data.Linq.DataContext> インスタンスによって保持される内部キャッシュは、取得されたオブジェクトや新規として追加されたオブジェクトを消去しません。

<xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> によって追跡されたオブジェクトでのみ、<xref:System.Data.Linq.DataContext> を呼び出すことができます。 `Untracked` オブジェクトの場合は、<xref:System.Data.Linq.Table%601.Attach%2A> を呼び出す前に <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> を呼び出す必要があります。 <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> オブジェクトで `Untracked` を呼び出すと、例外がスローされます。

> [!NOTE]
> テーブルからオブジェクトを削除すると、<xref:System.Data.Linq.DataContext.SubmitChanges%2A> が呼び出されたときに、対応する SQL `DELETE` コマンドが [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって生成されることになります。 この処理によって、キャッシュからオブジェクトが削除されたり、関連オブジェクトに削除が反映されることはありません。
>
> 削除されたオブジェクトの `id` を再要求するには、新しい <xref:System.Data.Linq.DataContext> インスタンスを使用します。 関連オブジェクトをクリーンアップするには、データベースの "*連鎖削除*" 機能を使用するか、関連オブジェクトを手動で削除します。
>
> 関連オブジェクトは、データベースの場合とは異なり、特別な順序で削除する必要はありません。

## <a name="updating-objects"></a>オブジェクトの更新

変更の通知を確認することで、`Updates` を検出できます。 通知は、プロパティ Set アクセス操作子の <xref:System.ComponentModel.INotifyPropertyChanging.PropertyChanging> イベントを通じて提供されます。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、オブジェクトへの最初の変更が通知されると、オブジェクトのコピーを作成し、オブジェクトを、`Update` ステートメントを生成する候補と見なします。

<xref:System.ComponentModel.INotifyPropertyChanging> を実装していないオブジェクトの場合、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、オブジェクトが最初に実体化されたときの値のコピーを保持します。 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> を呼び出すと、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、現在の値と元の値を比較して、オブジェクトが変更されたかどうかが判断されます。

リレーションシップの更新の場合、子から親への参照 (つまり、外部キーに対応する参照) が基準と見なされます。 逆方向 (つまり、親から子) の参照はオプションです。 リレーションシップ クラス (<xref:System.Data.Linq.EntitySet%601> および <xref:System.Data.Linq.EntityRef%601>) は、一対多および一対一のリレーションシップで双方向の参照が一致することを保証します。 オブジェクト モデルが <xref:System.Data.Linq.EntitySet%601> または <xref:System.Data.Linq.EntityRef%601> を使用していない場合、かつ、逆方向の参照が存在する場合は、ユーザーが、リレーションシップが更新されるときに前方参照と一致するようにする必要があります。

要求される参照と対応する外部キーの両方を更新する場合は、両者が一致する必要があります。 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> を呼び出したときに 2 つが同期しない場合は、<xref:System.InvalidOperationException> 例外がスローされます。 外部キー値を変更するだけで、基になる行を更新することはできますが、オブジェクト グラフの接続と、リレーションシップの双方向の一貫性を保持するには、参照を変更する必要があります。

## <a name="see-also"></a>関連項目

- [背景情報](background-information.md)
- [挿入、更新、および削除の各操作](insert-update-and-delete-operations.md)
