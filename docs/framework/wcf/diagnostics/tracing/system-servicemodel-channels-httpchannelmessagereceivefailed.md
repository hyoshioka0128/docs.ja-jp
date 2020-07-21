---
title: System.ServiceModel.Channels.HttpChannelMessageReceiveFailed
ms.date: 03/30/2017
ms.assetid: 9eb311da-fdcc-4dd3-9d85-05b3280dfdda
ms.openlocfilehash: e11b376924ee74e5d0d67da0cac59af41655dc44
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594076"
---
# <a name="systemservicemodelchannelshttpchannelmessagereceivefailed"></a>System.ServiceModel.Channels.HttpChannelMessageReceiveFailed
HTTP チャネルを介したメッセージの受信に失敗しました。  
  
## <a name="description"></a>説明  
 このトレースは、警告またはエラーとして出力されます。 どちらの場合であっても、このトレースは、受信 HTTP 要求に対して互換性のあるリスナーが見つからない場合に出力され、HTTP 要求は破棄されます。 これは、要求の HTTP 動詞が HTTP リスナーによって認識されない、または要求が対象としているアドレスでリッスンしているリスナーがないために発生します。 このトレースは、自己ホスト型の場合は警告を出力し、サービスが IIS でホストされている場合はエラーを出力します。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
