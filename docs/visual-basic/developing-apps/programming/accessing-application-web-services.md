---
title: アプリケーションの Web サービスへのアクセス
ms.date: 07/20/2015
helpviewer_keywords:
- Web services [Visual Basic], My.WebServices object
- My.WebServices object
- applications [Visual Basic], Web services
ms.assetid: 8ad5405b-e771-42b1-82d3-ce97af2cea9e
ms.openlocfilehash: cf9a0c9840b9228b59af9959cf3a4efb9a1d1ea0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410193"
---
# <a name="accessing-application-web-services-visual-basic"></a>アプリケーションの Web サービスへのアクセス (Visual Basic)

`My.WebServices` オブジェクトは、現在のプロジェクトにより参照されている各 Web サービスのインスタンスを提供します。 各インスタンスは要求に応じてインスタンス化されます。 これらの Web サービスには `My.WebServices` オブジェクトのプロパティを介してアクセスできます。 プロパティの名前は、プロパティがアクセスする Web サービスの名前と同じになります。 <xref:System.Web.Services.Protocols.SoapHttpClientProtocol> から継承されたクラスはすべて Web サービスです。

## <a name="tasks"></a>処理手順

次の表は、アプリケーションにより参照される Web サービスにアクセスする方法を一覧にしたものです。

|ターゲット|参照先|
|---|---|
|Web サービスを呼び出す|[My.WebServices オブジェクト](../../language-reference/objects/my-webservices-object.md)|
|Web サービスを非同期で呼び出し、完了時にイベントを処理する|[方法 : Web サービスを非同期で呼び出す](how-to-call-a-web-service-asynchronously.md)|

## <a name="see-also"></a>参照

- [My.WebServices オブジェクト](../../language-reference/objects/my-webservices-object.md)
