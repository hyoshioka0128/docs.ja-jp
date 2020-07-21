---
title: invalidGCHandleCookie MDA
description: InvalidGCHandleCookie managed デバッグアシスタント (MDA) を確認します。これは、無効な IntPtr クッキーから GCHandle への変換が試行されたときにアクティブ化されます。
ms.date: 03/30/2017
helpviewer_keywords:
- MDAs (managed debugging assistants), invalid cookies
- cookies, invalid
- managed debugging assistants (MDAs), invalid cookies
- InvalidGCHandleCookie MDA
- invalid cookies
ms.assetid: 613ad742-3c11-401d-a6b3-893ceb8de4f8
ms.openlocfilehash: 1063b7be902d3063717b6639564d819ef3292c0e
ms.sourcegitcommit: 0edbeb66d71b8df10fcb374cfca4d731b58ccdb2
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2020
ms.locfileid: "86051299"
---
# <a name="invalidgchandlecookie-mda"></a>invalidGCHandleCookie MDA
`invalidGCHandleCookie` マネージド デバッグ アシスタント (MDA) は、無効な <xref:System.IntPtr> Cookie から <xref:System.Runtime.InteropServices.GCHandle> への変換が試行されたときにアクティブ化されます。  
  
## <a name="symptoms"></a>現象  
 <xref:System.Runtime.InteropServices.GCHandle> の使用または <xref:System.IntPtr> からの取得を試みているときのアクセス違反やメモリ破損などの定義されていない動作。  
  
## <a name="cause"></a>原因  
 Cookie が <xref:System.Runtime.InteropServices.GCHandle> から最初に作成されていないために無効になっている可能性があります。既に解放されている <xref:System.Runtime.InteropServices.GCHandle> が異なるアプリケーション ドメイン内で <xref:System.Runtime.InteropServices.GCHandle> の Cookie になっているか、<xref:System.Runtime.InteropServices.GCHandle> としてネイティブ コードにマーシャリングされても、<xref:System.IntPtr> として CLR に再び渡され、キャストが試行されたことを表します。  
  
## <a name="resolution"></a>解決方法  
 <xref:System.Runtime.InteropServices.GCHandle> の有効な <xref:System.IntPtr> Cookie を指定します。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 この MDA が有効になっているときには、返される Cookie の値が MDA が有効になっていないときに返される値と異なるので、デバッガはルートをオブジェクトまでトレースできなくなります。  
  
## <a name="output"></a>出力  
 無効な <xref:System.IntPtr> Cookie 値が報告されます。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <invalidGCHandleCookie />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Runtime.InteropServices.GCHandle.FromIntPtr%2A>
- <xref:System.Runtime.InteropServices.GCHandle>
- [マネージド デバッグ アシスタントによるエラーの診断](diagnosing-errors-with-managed-debugging-assistants.md)
