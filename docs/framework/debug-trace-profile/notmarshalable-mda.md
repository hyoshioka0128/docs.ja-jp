---
title: notMarshalable MDA
description: NotMarshalable マネージデバッグアシスタントを確認します。これは、呼び出しが処理されない場合、または COM インターフェイスポインターのコンテキストが間違っている場合にアクティブ化される可能性があります。
ms.date: 03/30/2017
helpviewer_keywords:
- managed debugging assistants (MDAs), interface pointer not marshalable
- interface pointer not marshalable MDA
- MDAs (managed debugging assistants), interface pointer not marshalable
- marshaling, run-time errors
- managed debugging assistants (MDAs), marshaling
- marshalable interface pointers
- MDAs (managed debugging assistants), marshaling
- notMarshalable MDA
ms.assetid: 96e7b2c1-843f-4d64-b519-740c3a18b50a
ms.openlocfilehash: b464d914a8d83504daaf4cb276914da7798262dc
ms.sourcegitcommit: c23d9666ec75b91741da43ee3d91c317d68c7327
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85803795"
---
# <a name="notmarshalable-mda"></a>notMarshalable MDA
共通言語ランタイム (CLR: Common Language Runtime) がコンテキスト間でインターフェイスをマーシャリングするときに、有効な登録済みのプロキシやスタブのない COM インターフェイス ポインター、または不正な `IMarshal` インターフェイスの実装を検出すると、`notMarshalable` マネージド デバッグ アシスタント (MDA: Managed Debugging Assistant) がアクティブになります。  
  
## <a name="symptoms"></a>現象  
 呼び出しが処理されないか、COM インターフェイス ポインターの不正なコンテキストで発生します。  
  
## <a name="cause"></a>原因  
 コンテキスト間でインターフェイスのマーシャリングを試みたときに、有効な登録済みのプロキシやスタブがないか、`IMarshal` が不正です。  
  
## <a name="resolution"></a>解決策  
 プロキシ スタブを登録済みであることと、`IMarshal` の実装が有効であることを確認します。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 この MDA は、ランタイムに影響しません。  
  
## <a name="output"></a>出力  
 問題を説明するメッセージ。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <notMarshalable/>  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [マネージド デバッグ アシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md)
- [相互運用マーシャリング](../interop/interop-marshaling.md)
