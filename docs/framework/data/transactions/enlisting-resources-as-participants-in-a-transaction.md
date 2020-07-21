---
title: トランザクションの参加要素としてのリソースの参加
description: .NET トランザクションで参加要素としてリソースを参加させる トランザクションの各リソースは、リソース マネージャーによって管理され、トランザクション マネージャーによって調整されます。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 786a12c2-d530-49f4-9c59-5c973e15a11d
ms.openlocfilehash: c3c777593750b3a4f05ae97ed6e26e19f58e4d72
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141876"
---
# <a name="enlisting-resources-as-participants-in-a-transaction"></a>トランザクションの参加要素としてのリソースの参加

トランザクションに参加する各リソースは、リソース マネージャーによって管理され、その動作はトランザクション マネージャーによって調整されます。 この調整は、トランザクション マネージャーを介してトランザクションに参加したサブスクライバーへの通知によって行われます。

ここでは、単一または複数のリソースがトランザクションに参加する方法と、さまざまな種類の参加について説明します。 「[フェーズおよび複数フェーズでのトランザクションのコミット](committing-a-transaction-in-single-phase-and-multi-phase.md)」のトピックでは、参加リソース間でトランザクションのコミットメントを調整する方法について説明しています。

## <a name="enlisting-resources-in-a-transaction"></a>トランザクションへのリソースの参加

リソースをトランザクションに参加させるには、リソースをトランザクションに登録する必要があります。 <xref:System.Transactions.Transaction> クラスは、この機能を提供する一連のメソッドを定義しています。これらのメソッドの名前は **Enlist** で始まります。 さまざまな **Enlist** メソッドは、リソース マネージャーが持つ各種の参加リストにそれぞれ対応しています。 具体的には、揮発性リソースには <xref:System.Transactions.Transaction.EnlistVolatile%2A> メソッド、永続性リソースには <xref:System.Transactions.Transaction.EnlistDurable%2A> メソッドを使用します。 リソース マネージャーの永続性または揮発性とは、リソース マネージャーがエラーの回復をサポートするかどうかを意味します。 リソース マネージャーがエラーの回復をサポートする場合、フェーズ 1 (準備) 中にデータが永続ストレージに保存されます。したがって、リソース マネージャーがダウンした場合でも、回復時にトランザクションへの再参加を行い、TM から受信した通知に基づいて適切な動作を実行できます。 一般に、揮発性リソース マネージャーは、メモリ内のデータ構造 (たとえば、メモリ内のトランザクション ハッシュ テーブル) などの揮発性リソースを管理し、永続的リソース マネージャーは、より永続的なバッキング ストアを持つリソース (たとえば、バッキング ストアがディスクであるデータベース) を管理します。

簡単に説明すると、リソースが永続性をサポートするかどうかに応じて、<xref:System.Transactions.Transaction.EnlistDurable%2A> メソッドまたは <xref:System.Transactions.Transaction.EnlistVolatile%2A> メソッドのどちらを使用するかを決定した後、リソース マネージャーに <xref:System.Transactions.IEnlistmentNotification> インターフェイスを実装して、2 フェーズ コミット (2PC) に参加するようにリソースを登録する必要があります。 2PC の詳細については、「[単一フェーズおよび複数フェーズでのトランザクションのコミット](committing-a-transaction-in-single-phase-and-multi-phase.md)」を参照してください。

<xref:System.Transactions.Transaction.EnlistDurable%2A> および <xref:System.Transactions.Transaction.EnlistVolatile%2A> を複数回呼び出すことにより、これらのプロトコルのうち、複数のプロトコルに単一の参加要素を参加させることができます。

### <a name="durable-enlistment"></a>永続的参加リスト

<xref:System.Transactions.Transaction.EnlistDurable%2A> メソッドは、リソース マネージャーを永続性リソースとしてトランザクションに参加させるために使用します。  永続的リソース マネージャーがトランザクション中にダウンした場合、リソース マネージャーはオンラインに戻った後、フェーズ 2 が完了していない参加要素を <xref:System.Transactions.TransactionManager.Reenlist%2A> メソッドを使用してすべてのトランザクションに再参加させ、回復を実行します。回復プロセスが完了したら、<xref:System.Transactions.TransactionManager.RecoveryComplete%2A> を呼び出します。 回復の詳細については、「[回復の実行](performing-recovery.md)」を参照してください。

すべての <xref:System.Transactions.Transaction.EnlistDurable%2A> メソッドは、最初のパラメーターとして <xref:System.Guid> オブジェクトを使用します。 トランザクション マネージャーは、この <xref:System.Guid> を使用して、永続参加リストと特定のリソース マネージャーを関連付けます。 そのため、リソース マネージャーが再起動時に自身を他のリソース マネージャーと識別できるように、一貫して同じ <xref:System.Guid> を使用することが不可欠です。そうでない場合、回復が失敗する可能性があります。

<xref:System.Transactions.Transaction.EnlistDurable%2A> メソッドの第 2 パラメーターは、トランザクション通知を受信するためにリソース マネージャーが実装するオブジェクトへの参照です。 使用するオーバーロードにより、リソース マネージャーが単一フェーズ コミット (SPC) の最適化をサポートするかどうかがトランザクション マネージャーに通知されます。 ほとんどの場合、2 フェーズ コミット (2PC) に参加するために <xref:System.Transactions.IEnlistmentNotification> インターフェイスを実装します。 ただし、コミット プロセスを最適化する場合は、SPC 用の <xref:System.Transactions.ISinglePhaseNotification> インターフェイスの実装を検討することもできます。 SPC の詳細については、「[フェーズおよび複数フェーズでのトランザクションのコミット](committing-a-transaction-in-single-phase-and-multi-phase.md)」および「[単一フェーズ コミットおよび昇格可能単一フェーズ通知を使用した最適化](optimization-spc-and-promotable-spn.md)」を参照してください。

第 3 パラメーターは <xref:System.Transactions.EnlistmentOptions> 列挙体であり、その値は <xref:System.Transactions.EnlistmentOptions.None> または <xref:System.Transactions.EnlistmentOptions.EnlistDuringPrepareRequired> のいずれかです。 この値が <xref:System.Transactions.EnlistmentOptions.EnlistDuringPrepareRequired> に設定されている場合、トランザクション マネージャーから Prepare 通知を受信したときに、参加リストが追加リソース マネージャーを参加させる可能性があります。 ただし、この種類の参加リストは単一フェーズ コミットの最適化の条件を満たさないことに注意してください。

### <a name="volatile-enlistment"></a>揮発性参加リスト

キャッシュなどの揮発性リソースを管理する参加要素は、<xref:System.Transactions.Transaction.EnlistVolatile%2A> メソッドを使用して参加させる必要があります。 このようなオブジェクトは、トランザクションの結果を取得したり、システム障害の後で、参加しているトランザクションの状態を回復したりできない場合があります。

前に述べたように、リソース マネージャーはメモリ内の揮発性リソースを管理する場合、揮発性参加リストを作成します。 <xref:System.Transactions.Transaction.EnlistVolatile%2A> を使用する利点の 1 つに、トランザクションの不要なエスカレーションを強制しないことがあります。 トランザクションのエスカレーションの詳細については、「[トランザクション管理のエスカレーション](transaction-management-escalation.md)」のトピックを参照してください。 揮発的な参加を行うことは、トランザクション マネージャーによる参加リストの処理方法、およびトランザクション マネージャーがリソース マネージャーに期待することの両方に相違が生じることを意味します。 これは、揮発性リソース マネージャーが回復を実行しないためです。 揮発性リソース マネージャーが回復を実行せず、<xref:System.Transactions.Transaction.EnlistVolatile%2A> を必要とする <xref:System.Guid> メソッドを呼び出さないため、<xref:System.Transactions.TransactionManager.Reenlist%2A> メソッドは <xref:System.Guid> パラメーターを取得しません。

永続的参加リストの場合と同様に、どのオーバーロード メソッドを使用して参加する場合でも、リソース マネージャーが単一フェーズ コミットの最適化をサポートするかどうかがトランザクション マネージャーに示されます。 揮発性リソース マネージャーが回復を実行できないため、準備フェーズ中、回復情報は揮発性参加リストに書き込まれません。 したがって、<xref:System.Transactions.PreparingEnlistment.RecoveryInformation%2A> メソッドを呼び出すと、<xref:System.InvalidOperationException> になります。

次の例は、<xref:System.Transactions.Transaction.EnlistVolatile%2A> メソッドを使用して、このようなオブジェクトを参加要素としてトランザクションに参加させる方法を示しています。

[!code-csharp[Tx_Enlist#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/tx_enlist/cs/enlist.cs#1)]
[!code-vb[Tx_Enlist#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/tx_enlist/vb/enlist.vb#1)]

### <a name="optimizing-performance"></a>パフォーマンスの最適化

<xref:System.Transactions.Transaction> クラスは、PSPE (Promotable Single Phase Enlistment) を参加させるための <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> メソッドも提供しています。 これにより、永続的リソース マネージャー (RM) は、MSDTC による管理のために後で必要に応じてエスカレートできるトランザクションをホストおよび "所有" できます。 詳細については、「[単一フェーズ コミットおよび昇格可能単一フェーズ通知を使用した最適化](optimization-spc-and-promotable-spn.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [単一フェーズ コミットおよび昇格可能単一フェーズ通知を使用した最適化](optimization-spc-and-promotable-spn.md)
- [単一フェースおよび複数フェーズでのトランザクションのコミット](committing-a-transaction-in-single-phase-and-multi-phase.md)
