---
title: '方法: 証明書のサムプリントを取得する'
description: X.509 証明書で検出されたクレームを指定する方法について説明します。これは、認証に証明書を使用する WCF アプリケーションを開発する場合に必要です。
ms.date: 03/30/2017
helpviewer_keywords:
- certificates [WCF], retrieving thumbprint
ms.assetid: da3101aa-78cd-4c34-9652-d1f24777eeab
ms.openlocfilehash: 87c696323af442021af267f0d8c523418e2234f7
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246780"
---
# <a name="how-to-retrieve-the-thumbprint-of-a-certificate"></a>方法: 証明書のサムプリントを取得する
認証に x.509 証明書を使用する Windows Communication Foundation (WCF) アプリケーションを作成する場合、多くの場合、証明書で検出されたクレームを指定する必要があります。 たとえば、 <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint> メソッドで <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A> 列挙体を使用する場合は、拇印クレームを指定する必要があります。 クレーム値を検索するには 2 つの手順を実行する必要があります。 まず、証明書用の Microsoft 管理コンソール (MMC) スナップインを開きます (「[方法: MMC スナップインを使用して証明書を表示する](how-to-view-certificates-with-the-mmc-snap-in.md)」を参照してください)。次に、ここで説明するように、適切な証明書を検索し、その拇印 (またはその他の要求値) をコピーします。  
  
 サービス認証で証明書を使用する場合は、 **[Issued To]** 列 (コンソールの 1 番目の列) の値に注意することが重要です。 トランスポート セキュリティとして SSL (Secure Sockets Layer) を使用する場合、実行される最初のチェックの 1 つで、サービスのベース アドレス URI (Uniform Resource Identifier) が **[Issued To]** の値と比較されます。 値は一致する必要があります。一致しない場合は、認証が停止します。  
  
 Powershell の新しい-SelfSignedCertificate コマンドレットを使用して、開発中にのみ使用する一時的な証明書を作成することもできます。 ただし、既定では、このような証明書は証明機関によって発行されず、運用目的では使用できません。 詳細については、「[方法: 開発時に使用する一時的な証明書を作成する](how-to-create-temporary-certificates-for-use-during-development.md)」を参照してください。  
  
### <a name="to-retrieve-a-certificates-thumbprint"></a>証明書の拇印を取得するには  
  
1. 証明書用の Microsoft 管理コンソール (MMC) スナップインを開きます (「 [How to: View Certificates with the MMC Snap-in](how-to-view-certificates-with-the-mmc-snap-in.md)」を参照)。  
  
2. **[Console Root]** ウィンドウの左ペインで、 **[Certificates (Local Computer)]** をクリックします。  
  
3. **[Personal]** フォルダーをクリックして展開します。  
  
4. **[Certificates]** フォルダーをクリックして展開します。  
  
5. 証明書リストの **[Intended Purposes]** 見出しを確認します。 目的として **[Client Authentication]** が表示されている証明書を検索します。  
  
6. 証明書をダブルクリックする  
  
7. **[Certificate]** ダイアログ ボックスの **[Details]** タブをクリックします。  
  
8. フィールド リストをスクロールし、 **[Thumbprint]** をクリックします。  
  
9. ボックスから 16 進文字をコピーします。 この拇印を `X509FindType`のコードで使用する場合は、16 進文字の間のスペースを削除します。 たとえば、拇印 "a9 09 50 2d d8 2a e4 14 33 e6 f8 38 86 b0 0d 42 77 a3 2a 7b" は、コード内で "a909502dd82ae41433e6f83886b00d4277a32a7b" として指定する必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Security.Cryptography.X509Certificates.X509FindType.FindByThumbprint>
- <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A>
- [方法: SSL 証明書を使用してポートを構成する](how-to-configure-a-port-with-an-ssl-certificate.md)
- [方法: MMC スナップインを使用して証明書を参照する](how-to-view-certificates-with-the-mmc-snap-in.md)
- [方法: 開発中に使用する一時的な証明書を作成する](how-to-create-temporary-certificates-for-use-during-development.md)
