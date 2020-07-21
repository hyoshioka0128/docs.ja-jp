---
title: Single コンカレンシー モードでメッセージを順番に処理する
ms.date: 03/30/2017
ms.assetid: a90f5662-a796-46cd-ae33-30a4072838af
ms.openlocfilehash: baba75fe398d974f989acfda7ef7366986f6813b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598737"
---
# <a name="ordered-processing-of-messages-in-single-concurrency-mode"></a>Single コンカレンシー モードでメッセージを順番に処理する
基になるチャネルがセッションフルの場合を除き、WCF はメッセージの処理順序について一切保証しません。  たとえば、セッションフルチャネルではなく MsmqInputChannel を使用する WCF サービスでは、メッセージを順番に処理することができません。 場合によっては、開発者が注文処理の動作を必要としても、セッションを使用しないようにすることがあります。 このトピックでは、サービスが Single コンカレンシー モードで実行されている場合にこの動作を構成する方法について説明します。  
  
## <a name="in-order-message-processing"></a>順番に従ったメッセージの処理  
 <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A> という名前の新しい属性が <xref:System.ServiceModel.ServiceBehaviorAttribute> に追加されました。 <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A> を true に設定し、<xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> を <xref:System.ServiceModel.ConcurrencyMode.Single> に設定すると、サービスに送信されたメッセージは順番に処理されます。 次のコードは、これらの属性の設定方法を示しています。  
  
```csharp
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Single, EnsureOrderedDispatch = true )]  
    class Service : IService  
    {  
         // ...  
    }  
```  
  
 <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> をその他の値に設定すると、<xref:System.InvalidOperationException> がスローされます。  
  
## <a name="see-also"></a>関連項目

- [セッション、インスタンス化、およびコンカレンシー](sessions-instancing-and-concurrency.md)
- [コンカレンシー](../samples/concurrency.md)
