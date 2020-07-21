---
title: 既定の動作をオーバーライドするときの開発者の責任
ms.date: 03/30/2017
ms.assetid: c6909ddd-e053-46a8-980c-0e12a9797be1
ms.openlocfilehash: 4bfb108e81f64ea368c6bcc846553eb1af5c23b1
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792728"
---
# <a name="responsibilities-of-the-developer-in-overriding-default-behavior"></a>既定の動作をオーバーライドするときの開発者の責任
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、以下の要件を満たすことは強制ではないものの、これらの要件を満たさなかった場合の動作は未定義です。  
  
- オーバーライドするメソッドでは、<xref:System.Data.Linq.DataContext.SubmitChanges%2A> も <xref:System.Data.Linq.Table%601.Attach%2A> も呼び出さないでください。 オーバーライド メソッドでこれらのメソッドを呼び出した場合、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] から例外がスローされます。  
  
- オーバーライド メソッドは、トランザクションの開始、コミット、および中断には使用できません。 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 操作はトランザクションの下で実行されます。 入れ子になった内側のトランザクションは、外側のトランザクションと干渉する可能性があります。 読み込みのオーバーライド メソッドでは、<xref:System.Transactions.Transaction> 内で実行されている操作でないことを確認した場合にのみ、トランザクションを開始できます。  
  
- オーバーライド メソッドでは、該当するオプティミスティック コンカレンシーの対応付けに従うことが望まれます。 オプティミスティック コンカレンシーの競合が発生したときに、オーバーライド メソッドは <xref:System.Data.Linq.ChangeConflictException> をスローすることが望まれています。 この例外は [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によってキャッチされるため、<xref:System.Data.Linq.DataContext.SubmitChanges%2A> で指定されている <xref:System.Data.Linq.DataContext.SubmitChanges%2A> オプションを適切に処理できます。  
  
- 作成 (`Insert`) および `Update` のオーバーライド メソッドでは、操作が正常に完了した場合、データベースによって生成された列の値を、対応するオブジェクト メンバーに反映することが望まれます。  
  
     たとえば、`Order.OrderID` が ID 列 ("*自動インクリメント*" の主キー) に割り当てられている場合、`InsertOrder()` オーバーライド メソッドでは、データベースによって生成された ID を取得して、`Order.OrderID` メンバーにその ID を設定する必要があります。 同様に、タイムスタンプ型のメンバーは、データベースが生成したタイムスタンプ値に更新して、更新後のオブジェクトの一貫性を維持する必要があります。 データベースが生成した値を反映しなかった場合、データベースと、<xref:System.Data.Linq.DataContext> が追跡するオブジェクトとの間で、矛盾が生じる可能性があります。  
  
- 正しい動的 API を呼び出す必要があります。 たとえば、更新のオーバーライド メソッドで呼び出すことができるのは <xref:System.Data.Linq.DataContext.ExecuteDynamicUpdate%2A> のみです。 呼び出した動的メソッドが対象の操作に一致するかどうかについて、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、検出や検査は行いません。 適合しないメソッドを呼び出した場合 (たとえば、更新するオブジェクトについて <xref:System.Data.Linq.DataContext.ExecuteDynamicDelete%2A> を呼び出した場合)、結果は未定義です。  
  
- オーバーライド メソッドでは、決められた操作を実行することが望まれます。 Eager Loading、遅延読み込み、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] など、<xref:System.Data.Linq.DataContext.SubmitChanges%2A> 操作のセマンティクスでは、決められたサービスをオーバーライド メソッドで提供する必要があります。 たとえば、読み込みのオーバーライドで、データベースの内容をチェックせずに空のコレクションを返した場合、データの矛盾につながる可能性があります。  
  
## <a name="see-also"></a>関連項目

- [挿入、更新、および削除の各操作のカスタマイズ](customizing-insert-update-and-delete-operations.md)
