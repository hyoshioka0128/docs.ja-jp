---
title: '方法 : 署名の検証に使用する証明機関の証明書チェーンを指定する (WCF)'
ms.date: 03/30/2017
helpviewer_keywords:
- certificates [WCF], specifying the certificate authority certificate chain
- certificates [WCF], verifying signatures
ms.assetid: 7c719355-aa41-4567-80d0-5115a8cf73fd
ms.openlocfilehash: 103d68d4ccb4cc243d28037260c1f9f380485ff6
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600310"
---
# <a name="how-to-specify-the-certificate-authority-certificate-chain-used-to-verify-signatures-wcf"></a>方法 : 署名の検証に使用する証明機関の証明書チェーンを指定する (WCF)
Windows Communication Foundation (WCF) は、x.509 証明書を使用して署名された SOAP メッセージを受信すると、x.509 証明書が信頼された証明機関によって発行されたことを確認します。 これは、証明書ストアを検索し、その証明機関の証明書が信頼された証明書として指定されているかどうかを確認することによって行われます。 WCF がこの判断を行うためには、証明機関の証明書チェーンが正しい証明書ストアにインストールされている必要があります。  
  
### <a name="to-install-a-certification-authority-certificate-chain"></a>証明機関証明書チェーンをインストールするには  
  
- SOAP メッセージの受信者によって発行された x.509 証明書を信頼する証明機関ごとに、証明機関の証明書チェーンを、WCF が x.509 証明書を取得するように構成されている証明書ストアにインストールします。  
  
     たとえば、SOAP メッセージの受信者が Microsoft によって発行された x.509 証明書を信頼する場合、WCF が x.509 証明書を検索するように設定されている証明書ストアに、Microsoft の証明機関証明書チェーンをインストールする必要があります。 WCF が x.509 証明書を検索する証明書ストアは、コードまたは構成で指定できます。 たとえば、これは、メソッドを使用してコードで指定することも、を含むいくつかの方法で構成することもでき <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) ます。  
  
     Windows には、信頼された証明機関の既定の証明書チェーンのセットが用意されているため、一部の CA については証明書チェーンをインストールする必要はありません。  
  
    1. 証明機関証明書チェーンをエクスポートします。  
  
         正確なエクスポート方法は、証明機関によって異なります。 証明機関が Microsoft 証明書サービスを実行している場合は、[ **ca 証明書、証明書チェーン、または CRL をダウンロードする**] を選択し、[ **ca 証明書のダウンロード**] を選択します。  
  
    2. 証明機関証明書チェーンをインポートします。  
  
         Microsoft 管理コンソール (MMC: Microsoft Management Console) で、証明書スナップインを開きます。 WCF が x.509 証明書を取得するように構成されている証明書ストアについて、[**信頼されたルート****証明機関**] フォルダーを選択します。 [**信頼されたルート証明機関**] フォルダーの下で、[**証明書**] フォルダーを右クリックし、[**すべてのタスク**] をポイントして、[**インポート**] をクリックします。 手順 a. でエクスポートしたファイルを指定します。  
  
         MMC で証明書スナップインを使用する方法の詳細については、「[方法: Mmc スナップインを使用して証明書を表示する](how-to-view-certificates-with-the-mmc-snap-in.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [証明書の使用](working-with-certificates.md)
