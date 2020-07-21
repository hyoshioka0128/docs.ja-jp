---
title: Internet Explorer と WCF で実行されるサービス証明書の検証の相違点
ms.date: 03/30/2017
helpviewer_keywords:
- service certificate validation [WCF]
- certificates [WCF], service certificate validation
ms.assetid: 9dffcab2-70a9-40f0-99fd-d3a0b296028f
ms.openlocfilehash: 151075f2894b895ab90418748df9face3aa70252
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599192"
---
# <a name="differences-between-service-certificate-validation-done-by-internet-explorer-and-wcf"></a>Internet Explorer と WCF で実行されるサービス証明書の検証の相違点
HTTPS の使用時に Internet Explorer と Windows Communication Foundation (WCF) がサービス証明書を検証する方法が異なるため、WCF クライアントがサービスエンドポイントにメッセージを正常に送信できる場合でも、Internet Explorer がサービスのヘルプページまたは Web サービス記述言語 (WSDL) にアクセスできない可能性があります。 これは、Internet Explorer によって、サービス証明書の `ServerAuthentication` 拡張使用フラグにオブジェクト識別子 (OID) があるかどうかが確認されるのに対し、WCF ではこのような制約は適用されないためです。 Internet Explorer がサービスのヘルプページまたはサービスの WSDL にアクセスできない場合は、 [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を使用してサービスメタデータにアクセスします。  
  
## <a name="see-also"></a>関連項目

- [HTTPS、SSL Over TCP、SOAP セキュリティ間における証明書検証方法の相違点](cert-val-diff-https-ssl-over-tcp-and-soap.md)
- [方法: メタデータの取得および準拠サービスの実装をする](how-to-retrieve-metadata-and-implement-a-compliant-service.md)
