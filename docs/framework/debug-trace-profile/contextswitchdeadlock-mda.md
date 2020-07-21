---
title: contextSwitchDeadlock MDA
description: COM コンテキストの遷移中にデッドロックが検出されたときにアクティブ化される、.NET での contextSwitchDeadlock ロックマネージデバッグアシスタント (MDA) について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- deadlocks [.NET Framework]
- pumping messages
- STA message pumping
- single-threaded COM components
- MDAs (managed debugging assistants), context switching deadlocks
- managed debugging assistants (MDAs), context switching deadlocks
- ContextSwitchDeadlock MDA
- message pumping
- context switching deadlocks
ms.assetid: 26dfaa15-9ddb-4b0a-b6da-999bba664fa6
ms.openlocfilehash: 52db4f2c88bac4e8cac621cca989fa10acb43f94
ms.sourcegitcommit: a2c8b19e813a52b91facbb5d7e3c062c7188b457
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2020
ms.locfileid: "85416019"
---
# <a name="contextswitchdeadlock-mda"></a>contextSwitchDeadlock MDA

`contextSwitchDeadlock` マネージド デバッグ アシスタント (MDA) は、COM コンテキストの遷移の試行中にデッドロックが検出されるとアクティブ化されます。

## <a name="symptoms"></a>現象

最も一般的な症状は、マネージド コードから実行されたアンマネージド COM コンポーネントの呼び出しから戻らないことです。  別の症状として、メモリの使用量が時間と共に増加する場合もあります。

## <a name="cause"></a>原因

最も考えられる原因として、シングルスレッド アパートメント (STA) スレッドがメッセージ ポンプを行っていないことがあります。 STA スレッドが、メッセージ ポンプを行わずに待機しているか、または時間のかかる操作を実行していて、メッセージ キューのポンプを許可していません。

メモリ使用量が時間の経過と共に増加する症状は、ファイナライザー スレッドがアンマネージ COM コンポーネント上の `Release` を呼び出そうとして、そのコンポーネントが戻らない場合に発生します。  このため、ファイナライザーは他のオブジェクトを再利用できなくなります。

既定では、Visual Basic コンソール アプリケーションのメイン スレッドのスレッド処理モデルは STA です。 STA スレッドが共通言語ランタイムまたはサードパーティ コントロールを通じて COM 相互運用性を直接または間接的に使用する場合、この MDA がアクティブ化されます。  Visual Basic コンソール アプリケーションでこの MDA がアクティブ化されるのを防ぐには、メイン メソッドに <xref:System.MTAThreadAttribute> 属性を適用するか、またはメッセージをポンプするようにアプリケーションを変更します。

次のすべての条件が満たされる場合、この MDA が誤ってアクティブ化される可能性があります。

- アプリケーションがライブラリを通じて直接または間接的に STA スレッドから COM コンポーネントを作成する。

- デバッガーでアプリケーションが中断され、ユーザーがアプリケーションを続行したか、またはステップ操作を実行した。

- アンマネージ デバッグが有効になっていない。

MDA が誤ってアクティブ化されたかどうかを判断するには、すべてのブレークポイントを無効にし、アプリケーションを再び実行して、中断なしで実行させます。 MDA がアクティブ化されない場合は、最初のアクティブ化は誤りだった可能性があります。 その場合は、MDA を無効にして、デバッグ セッションとの干渉を防ぎます。

> [!NOTE]
> この MDA は、Visual Studio の既定のセットに含まれています。 Mda を無効にする方法の詳細については、「[マネージデバッグアシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md#enable-and-disable-mdas)」を参照してください。

## <a name="resolution"></a>解決策

STA メッセージ ポンプに関する COM 規則に従います。

## <a name="effect-on-the-runtime"></a>ランタイムへの影響

この MDA は CLR に影響しません。 COM コンテキストに関するデータを報告するだけです。

## <a name="output"></a>出力

現在のコンテキストおよびターゲット コンテキストを説明するメッセージです。

## <a name="configuration"></a>構成

```xml
<mdaConfig>
  <assistants>
    <contextSwitchDeadlock />
  </assistants>
</mdaConfig>
```

## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [マネージド デバッグ アシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md)
- [相互運用マーシャリング](../interop/interop-marshaling.md)
