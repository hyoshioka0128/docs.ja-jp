---
title: marshalCleanupError MDA
description: 一時的な構造のクリーンアップ中に予期しないエラーが発生したために呼び出される、marshalCleanupError マネージデバッグアシスタント (MDA) を確認します。
ms.date: 03/30/2017
helpviewer_keywords:
- cleanup operations
- marshaling, run-time errors
- managed debugging assistants (MDAs), marshaling
- MDAs (managed debugging assistants), marshaling
- marshaling cleanup error
- MarshalCleanupError MDA
- memory, cleanup errors
ms.assetid: 2f5d9e7c-ae51-4155-a435-54347aa1f091
ms.openlocfilehash: 3c7498d6f51484de3a2e84d611a2634f53724ab6
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051612"
---
# <a name="marshalcleanuperror-mda"></a>marshalCleanupError MDA
共通言語ランタイム (CLR) が、ネイティブ コードとマネージド コードの境界間でのデータ型のマーシャリングに使用した一時的な構造体とメモリをクリーンアップしようとしたときにエラーが発生すると、`marshalCleanupError` マネージド デバッグ アシスタント (MDA) がアクティブ化されます。  
  
## <a name="symptoms"></a>現象  
 ネイティブ コードとマネージド コードの遷移を実行する場合、スレッド カルチャなどのランタイム状態が復元されない場合、または<xref:System.Runtime.InteropServices.SafeHandle> をクリーンアップしようしてエラーが発生した場合に、メモリ リークが発生します。  
  
## <a name="cause"></a>原因  
 一時的な構造体のクリーンアップ中に予期しないエラーが発生しました。  
  
## <a name="resolution"></a>解決方法  
 すべての <xref:System.Runtime.InteropServices.SafeHandle> デストラクター、ファイナライザー、カスタム マーシャラーの実装を調べ、エラーがないかどうかをレビューします。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 この MDA は CLR に影響しません。  
  
## <a name="output"></a>出力  
 クリーンアップ中に失敗した操作を報告するメッセージ。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <marshalCleanupError />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.MarshalAsAttribute>
- [マネージド デバッグ アシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md)
- [相互運用マーシャリング](../interop/interop-marshaling.md)
