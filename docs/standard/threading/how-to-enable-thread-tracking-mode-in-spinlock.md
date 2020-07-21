---
title: '方法: SpinLock のスレッド追跡モードを有効にする'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SpinLock, how to enable thread-tracking
ms.assetid: 62ee2e68-0bdd-4869-afc9-f0a57a11ae01
ms.openlocfilehash: 1a46655530948bb8732362dbd6d86ead495b0998
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84279531"
---
# <a name="how-to-enable-thread-tracking-mode-in-spinlock"></a>方法: SpinLock のスレッド追跡モードを有効にする
<xref:System.Threading.SpinLock?displayProperty=nameWithType> は低レベルの相互排他ロックであり、待機時間が非常に短いシナリオで使用できます。 <xref:System.Threading.SpinLock> は再入可能ではありません。 スレッドはロックを取得した後、ロックを正しく解放してから再度取得する必要があります。 通常、ロックを再取得しようとすると、デッドロックが発生し、デッドロックのデバッグが非常に困難になる場合があります。 開発の支援手段として、<xref:System.Threading.SpinLock?displayProperty=nameWithType> ではスレッド追跡モードがサポートされ、スレッドが既に保持しているロックを再取得しようとしたときに例外がスローされます。 これにより、ロックが正しく解放されたなかった位置を見つけやすくなります。 スレッド追跡モードを有効にするには、ブール入力パラメーターを受け取る <xref:System.Threading.SpinLock> コンストラクターを使用して、`true` の引数を渡します。 開発およびテスト フェーズの完了後は、パフォーマンスを向上させるため、スレッド追跡モードを無効にしてください。  
  
## <a name="example"></a>例  
 次の例はスレッド追跡モードを示しています。 以下のいずれかの結果の原因となるコード エラーをシミュレートするために、ロックを正しく解放する行がコメントアウトされています。  
  
- `true` (Visual Basic では `True`) の引数を使用して <xref:System.Threading.SpinLock> が作成された場合、例外がスローされる。  
  
- `false` (Visual Basic では `False`) の引数を使用して <xref:System.Threading.SpinLock> が作成された場合、デッドロックが発生する。  
  
 [!code-csharp[CDS_SpinLock#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#01)]
 [!code-vb[CDS_SpinLock#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_threadtracking.vb#01)]  
  
## <a name="see-also"></a>参照

- [SpinLock](spinlock.md)
