---
title: 信頼できるセッション
ms.date: 03/30/2017
f1_keywords:
- Windows Communication Foundation, sessions and instances
- WCF, sessions and instances
- sessions and instances [WCF]
helpviewer_keywords:
- instances [WCF]
- sessions [WCF]
ms.assetid: 143951b3-3aa0-4540-b4b7-d33e77e874a1
ms.openlocfilehash: 910ad952192243c6aa8a79417ad711d8c2a4ba2e
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84590541"
---
# <a name="reliable-sessions"></a>信頼できるセッション

このセクションでは、Windows Communication Foundation (WCF) の信頼できるセッションについて説明します。これは、どのように使用されるか、どのように使用されるか、どのようなバインディング構成がサポートしているか、およびベストプラクティスに関するヒントについて説明します。 このセクションの重要なポイントと関連するトピックの詳細について、次の表にまとめます。

Reliable session WCF は、エンドポイント間で送信されるメッセージが SOAP またはトランスポート中継局間で転送されることを保証する機能を提供します。また、必要に応じて、送信された順序で1回だけ配信されます。

WCF アプリケーションで信頼できるセッションを使用するには、既定で、またはオプションとして、信頼できるセッションをサポートするシステム指定のバインディングのいずれかを使用するか、またはセッションをサポートする独自のカスタムバインドを作成します。

## <a name="in-this-section"></a>このセクションの内容

[信頼できるセッションの概要](reliable-sessions-overview.md)信頼できるセッション、使用するタイミング、信頼できるセッションをサポートするさまざまなバインディング、および動作のしくみについて説明します。

[方法: 信頼できるセッション内でメッセージを交換](how-to-exchange-messages-within-a-reliable-session.md)する構成で指定されたカスタムバインディングを使用して、HTTP 経由で信頼できるセッションを作成する方法について説明します。

[方法: 信頼できるセッション内のメッセージをセキュリティで保護する](how-to-secure-messages-within-reliable-sessions.md)信頼できるセッションをセキュリティで保護する方法について説明します。

[方法: HTTPS を使用してカスタムの信頼できるセッションバインディングを作成](how-to-create-a-custom-reliable-session-binding-with-https.md)するHTTPS を介して信頼できるセッションを作成する方法について説明します。

[信頼できるセッションのベストプラクティス](best-practices-for-reliable-sessions.md)信頼できるセッションの使用に関連するベストプラクティスについて説明します。

## <a name="reference"></a>関連項目

<xref:System.ServiceModel.ReliableSession>

## <a name="see-also"></a>関連項目

- [キューと信頼できるセッション](queues-and-reliable-sessions.md)
- [セッション、インスタンス化、およびコンカレンシー](sessions-instancing-and-concurrency.md)
