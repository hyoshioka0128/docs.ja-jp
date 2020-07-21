---
title: '方法: プロデューサー/コンシューマーのデータフロー パターンを実装する'
description: .NET の TPL データフロー ライブラリを使用して、プロデューサー/コンシューマー データフロー パターンを実装する方法について理解します。
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TPL dataflow library, implementing producer-consumer pattern
- Task Parallel Library, dataflows
- producer-consumer patterns, implementing [TPL]
ms.assetid: 47a1d38c-fe9c-44aa-bd15-937bd5659b0b
ms.openlocfilehash: e9ed8f84f1daca64fa60d8aed18aa2d9be1380e0
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768925"
---
# <a name="how-to-implement-a-producer-consumer-dataflow-pattern"></a>方法: プロデューサー/コンシューマーのデータフロー パターンを実装する
このドキュメントでは、TPL データフロー ライブラリを使用して、プロデューサー/コンシューマー パターンを実装する方法について説明します。 このパターンでは、"*プロデューサー*" がメッセージをメッセージ ブロックに送信し、"*コンシューマー*" がそのブロックからメッセージを読み取ります。  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]
  
## <a name="example"></a>例  
 次の例では、データフローを使用する基本的なプロデューサー/コンシューマー モデルを示します。 `Produce` メソッドは、データのランダム バイトを含む配列を <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601?displayProperty=nameWithType> オブジェクトに書き込み、`Consume` メソッドは <xref:System.Threading.Tasks.Dataflow.ISourceBlock%601?displayProperty=nameWithType> オブジェクトからバイトを読み取ります。 派生型ではなく、<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> と <xref:System.Threading.Tasks.Dataflow.ITargetBlock%601> のインターフェイス上で動作することで、さまざまなデータフロー ブロック型上で動作する再利用可能なコードを記述できます。 この例では、<xref:System.Threading.Tasks.Dataflow.BufferBlock%601> クラスを使用します。 <xref:System.Threading.Tasks.Dataflow.BufferBlock%601> クラスはソース ブロックとターゲット ブロックの両方として機能するため、プロデューサーおよびコンシューマーは共有されたオブジェクトを使用してデータを転送できます。  
  
 `Produce` メソッドはループ内で <xref:System.Threading.Tasks.Dataflow.DataflowBlock.Post%2A> メソッドを呼び出し、ターゲット ブロックにデータを同期的に書き込みます。 `Produce` メソッドはターゲット ブロックにすべてのデータを書き込んだ後、<xref:System.Threading.Tasks.Dataflow.IDataflowBlock.Complete%2A> メソッドを呼び出して、このブロックに使用可能なデータが追加されないように指示します。 `Consume` メソッドでは、[async](../../csharp/language-reference/keywords/async.md) 演算子と [await](../../csharp/language-reference/operators/await.md) 演算子 (Visual Basic では [Async](../../visual-basic/language-reference/modifiers/async.md) と [Await](../../visual-basic/language-reference/operators/await-operator.md)) を使用して、<xref:System.Threading.Tasks.Dataflow.ISourceBlock%601> オブジェクトから受信した合計バイト数を非同期的に計算します。 非同期的に動作するために、`Consume` メソッドは <xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A> メソッドを呼び出して、ソース ブロックに使用可能なデータがあるときとソース ブロックに使用可能なデータが追加されなくなったときに、通知を受信します。  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#1)]
 [!code-vb[TPLDataflow_ProducerConsumer#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#1)]  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 上記の例では、1 つのコンシューマーのみを使用してソース データを処理します。 アプリケーションに複数のコンシューマーがある場合は、次の例に示すように、<xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> メソッドを使用してソース ブロックからデータを読み取ります。  
  
 [!code-csharp[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_producerconsumer/cs/dataflowproducerconsumer.cs#2)]
 [!code-vb[TPLDataflow_ProducerConsumer#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_producerconsumer/vb/dataflowproducerconsumer.vb#2)]  
  
 <xref:System.Threading.Tasks.Dataflow.IReceivableSourceBlock%601.TryReceive%2A> メソッドは、データを使用できないときに `False` を返します。 複数のコンシューマーがソース ブロックに同時にアクセスする必要がある場合、この仕組みが、<xref:System.Threading.Tasks.Dataflow.DataflowBlock.OutputAvailableAsync%2A> の呼び出し後もデータを使用可能なことを保証します。  
  
## <a name="see-also"></a>関連項目

- [データフロー](dataflow-task-parallel-library.md)
