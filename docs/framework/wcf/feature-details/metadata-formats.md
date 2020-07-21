---
title: メタデータ形式
ms.date: 03/30/2017
ms.assetid: baad1e68-28fc-4a6a-8a43-75e47e7fa871
ms.openlocfilehash: a74a57843beaba09b969678a34cad3ad8bed7050
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598841"
---
# <a name="metadata-formats"></a>メタデータ形式
Windows Communication Foundation (WCF) は、次の表のメタデータ形式をサポートしています。  
  
## <a name="metadata-specifications-and-usage"></a>メタデータの仕様と用途  
  
|プロトコル|仕様と用途|  
|--------------|-----------------------------|  
|WSDL 1.1|[Web Services Description Language (WSDL) 1.1](https://www.w3.org/TR/wsdl/)<br /><br /> WCF では、Web サービス記述言語 (WSDL) を使用してサービスを記述します。|  
|XML スキーマ|[Xml スキーマパート 2: データ型 Second エディション](https://www.w3.org/TR/2004/REC-xmlschema-2-20041028/)と[XML スキーマパート 1: 2 番目のエディション](https://www.w3.org/TR/2004/REC-xmlschema-1-20041028/)<br /><br /> WCF では、XML スキーマを使用して、メッセージで使用されるデータ型を記述します。|  
|WS-Policy|[Web Services Policy 1.2 - Framework (WS-Policy)](https://www.w3.org/Submission/WS-Policy/)<br /><br /> [Web Services Policy 1.5 - Framework](https://www.w3.org/TR/ws-policy/)<br /><br /> WCF では、ドメイン固有のアサーションと共に WS-POLICY 1.2 または1.5 仕様を使用して、サービスの要件と機能を記述します。|  
|WS-PolicyAttachments|[Web Services Policy 1.2 - Attachment (WS-PolicyAttachment)](https://www.w3.org/Submission/WS-PolicyAttachment/)<br /><br /> WCF では、WS-POLICY 添付ファイルを実装して、WSDL 内のさまざまなスコープでポリシー式をアタッチします。|  
|WS-Metadata Exchange|[Web Services Metadata Exchange (WS-MetadataExchange) version 1.1](https://specs.xmlsoap.org/ws/2004/09/mex/WS-MetadataExchange.pdf)<br /><br /> WCF では、XML スキーマ、WSDL、および WS-POLICY を取得するために、Ws-metadataexchange が実装されています。|  
|WS Addressing Binding for WSDL|[Web Services Addressing 1.0 - WSDL Binding](https://www.w3.org/TR/ws-addr-wsdl/)<br /><br /> WCF では、wsdl でアドレス指定情報をアタッチするために、WS-ADDRESSING Binding for WSDL が実装されています。|  
  
## <a name="see-also"></a>関連項目

- [システム標準の相互運用性バインディングがサポートしている Web サービス プロトコル](web-services-protocols-supported-by-system-provided-interoperability-bindings.md)
- [WSDL とポリシー](wsdl-and-policy.md)
