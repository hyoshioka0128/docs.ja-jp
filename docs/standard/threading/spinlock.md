---
title: SpinLock
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- synchronization primitives, SpinLock
ms.assetid: f9af93bb-7a0d-4ba5-afe8-74f48b6b6958
ms.openlocfilehash: a5202be5e3055702954ad7a1565999ad2496eaea
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84291124"
---
# <a name="spinlock"></a>SpinLock
<xref:System.Threading.SpinLock> 構造体は低レベルで相互排他的な同期プリミティブであり、ロックの取得を待機する間にスピンします。 マルチコア コンピューターでは、待機時間が短いことが予測され、競合を最小限に抑えられる場合、パフォーマンスは他の種類のロックよりも <xref:System.Threading.SpinLock> の方が優れています。 ただし、プロファイルにより、<xref:System.Threading.Monitor?displayProperty=nameWithType> メソッドまたは <xref:System.Threading.Interlocked> メソッドがプログラムのパフォーマンスを大幅に低下させていることがわかった場合にのみ、<xref:System.Threading.SpinLock> を使用することをお勧めします。  
  
 <xref:System.Threading.SpinLock> では、ロックをまだ取得していない場合でも、スレッドのタイム スライスが生成される可能性があります。 スレッドの優先順位の逆転を避ける場合と、ガベージ コレクターを進める場合にこのようになります。 <xref:System.Threading.SpinLock> を使用する場合は、スレッドが一定時間ロックを保持できないことと、スレッドがロックを保持している間はブロックできないことを確認してください。  
  
 SpinLock は値の型であるため、2 つのコピーで同じロックを参照する場合は、参照渡しで明示的に渡す必要があります。  
  
 この型の使用方法の詳細については、「<xref:System.Threading.SpinLock?displayProperty=nameWithType>」を参照してください。 例については、「[方法: 下位レベルの同期に SpinLock を使用する](how-to-use-spinlock-for-low-level-synchronization.md)」を参照してください。  
  
 <xref:System.Threading.SpinLock> では*スレッド*-*追跡* モードがサポートされ、開発フェーズ中に使用することができ、特定の時間にロックを保持しているスレッドの追跡に役立ちます。 スレッド追跡モードはデバッグに非常に役立ちますが、パフォーマンスが低下する可能性があるため、リリース バージョンのプログラムでは無効にすることをお勧めします。 詳細については、「[方法: SpinLock のスレッド追跡モードを有効にする](how-to-enable-thread-tracking-mode-in-spinlock.md)」を参照してください。  
  
## <a name="see-also"></a>参照

- [スレッド処理オブジェクトと機能](threading-objects-and-features.md)
