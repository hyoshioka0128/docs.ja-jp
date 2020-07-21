---
title: サービスおよびクライアントのセキュリティ保護
ms.date: 03/30/2017
helpviewer_keywords:
- message security [WCF]
ms.assetid: e681f3bd-0c09-4a58-b0e4-0ecbdf1aa6c7
ms.openlocfilehash: db0a0dcfbe04a7b7dbfabfed59f9b8637d0a2797
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84586209"
---
# <a name="securing-services-and-clients"></a>サービスおよびクライアントのセキュリティ保護
このセクションの情報は、Windows Communication Foundation (WCF) でのセキュリティのプログラミングに焦点を当てています。 一般に、これには、システムが提供する適切なバインディングを選択すること、セキュリティ要素のプロパティを適切に設定すること、サービス側/クライアント側で使う資格情報の検索方法にまつわる、サービスの動作に関するプロパティを適切に設定することなどが含まれます。 これらの手法は、[一般的なセキュリティシナリオ](common-security-scenarios.md)に示すように、ほとんどのシナリオでほとんどのユーザーのセキュリティ要件に対応しています。 シナリオにより多くの機能が必要な場合は、まず「[カスタムバインドを使用したセキュリティ機能](security-capabilities-with-custom-bindings.md)」を参照してください。ソリューションが明らかでない場合は、「[セキュリティの拡張](../extending/extending-security.md)」を参照してください。 豊富な信頼性情報を使用するシステムを作成 (または相互運用) する場合は、「[承認](authorization-in-wcf.md)」のトピックを参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [WCF セキュリティのプログラミング](programming-wcf-security.md)  
 メッセージを保護するために使うプログラミング モデルの概要  
  
 [トランスポート セキュリティの概要](transport-security-overview.md)  
 トランスポート層を介してやり取りするメッセージを保護する方法の概要  
  
 [メッセージのセキュリティ](message-security-in-wcf.md)  
 Windows Communication Foundation (WCF) でメッセージレベルのセキュリティを使用する理由の概要を示します。  
  
 [セキュリティで保護されたセッション](secure-sessions.md)  
 WCF セッションをセキュリティで保護する場合に必要な考慮事項について説明します。  
  
 [証明書の使用](working-with-certificates.md)  
 X.509 証明書を使用する際に必要となる主なタスクの解説  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel>  
  
 <xref:System.ServiceModel.Channels>  
  
 <xref:System.ServiceModel.Security>  
  
## <a name="related-sections"></a>関連項目  
 [セキュリティの概念](security-concepts.md)  
  
 [セキュリティの拡張](../extending/extending-security.md)  
  
 [一般的なセキュリティ シナリオ](common-security-scenarios.md)  
  
 [バインディングとセキュリティ](bindings-and-security.md)  
  
 [カスタム バインディングを使用したセキュリティ機能](security-capabilities-with-custom-bindings.md)  
  
 [セキュリティの拡張](../extending/extending-security.md)  
  
 [承認](authorization-in-wcf.md)  
  
## <a name="see-also"></a>関連項目

- [基本的な WCF プログラミング](../basic-wcf-programming.md)
- [Windows Server AppFabric のセキュリティ モデル](https://docs.microsoft.com/previous-versions/appfabric/ee677202(v=azure.10))
