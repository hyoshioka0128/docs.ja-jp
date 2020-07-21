---
title: スタック ETW イベント
description: Stack ETW イベントについて説明します。これは、イベントの発生後にスタックトレースを生成するために、他のイベントと組み合わせて使用する必要があります。
ms.date: 03/30/2017
helpviewer_keywords:
- stack event [.NET Framework]
- ETW, stack event (CLR)
ms.assetid: f612fa5b-4b62-4593-a19e-85c9b1018dce
ms.openlocfilehash: cab496615c4ef17831895b72c8987917e3c06e77
ms.sourcegitcommit: cf5a800a33de64d0aad6d115ffcc935f32375164
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/20/2020
ms.locfileid: "86474138"
---
# <a name="stack-etw-event"></a>スタック ETW イベント
イベントの発生後にスタック トレースを生成するには、スタック イベントを他のイベントと併用する必要があります。 ランタイム プロバイダーが有効になると、ログに記録されます。 これは頻度が非常に高いイベントです。別のランタイム イベントが発生するたびに発生するためです。 そのような理由から、このイベントの使用には注意が必要です。  
  
 次の表に、キーワードとレベルを示します。 (詳細については、「 [CLR ETW Keywords and Levels](clr-etw-keywords-and-levels.md)」を参照してください)。  
  
|イベントを発生させるキーワード|Level|  
|-----------------------------------|-----------|  
|`StackKeyword` (0x40000000)|LogAlways(0)|  
  
 次の表に、イベント情報を示します。  
  
|Event|イベント ID|いつ発生するか|  
|-----------|--------------|-----------------|  
|`CLRStackWalk`|82|他のイベントを併用し、イベント後にスタック トレースを生成します。|  
  
 次の表に、イベント データを示します。  
  
|フィールド名|データ型|説明|  
|----------------|---------------|-----------------|  
|ClrInstanceID|win:Uint16|一意のランタイム識別子。|  
|Reserved1|win:UInt8|予約済み。|  
|Reserved2|win:UInt8|予約済み。|  
|FrameCount|win:UInt32|スタック トレースのフレーム数。|  
|スタック|win:Pointer|命令ポインターの列。|  
  
## <a name="see-also"></a>関連項目

- [CLR ETW イベント](clr-etw-events.md)
