---
title: '方法: MMC スナップインを使用して証明書を表示する'
description: セキュリティで保護された WCF クライアントまたはサービスでは、資格情報として証明書を使用できます。 MMC プラグインを使用して確認できる証明書ストアの種類について説明します。
ms.date: 02/25/2019
helpviewer_keywords:
- certificates [WCF], viewing with the MMC snap-in
ms.assetid: 2b8782aa-ebb4-4ee7-974b-90299e356dc5
ms.openlocfilehash: e63034e48ae836f67f89b454829f7196c94610cd
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246676"
---
# <a name="how-to-view-certificates-with-the-mmc-snap-in"></a>方法: MMC スナップインを使用して証明書を表示する
セキュリティで保護されたクライアントまたはサービスを作成する場合は、資格情報として[証明書](working-with-certificates.md)を使用できます。 たとえば、一般的な資格情報の種類は、x.509 証明書です。この証明書は、メソッドを使用して作成します <xref:System.ServiceModel.Security.X509CertificateInitiatorClientCredential.SetCertificate%2A?displayProperty=nameWithType> 。

Windows システムの Microsoft 管理コンソール (MMC) を使用して確認できる証明書ストアには、次の3種類があります。

- [ローカルコンピューター]: ストアはデバイスに対してローカルで、デバイス上のすべてのユーザーに対してグローバルです。

- 現在のユーザー: ストアは、デバイス上の現在のユーザーアカウントに対してローカルです。

- サービスアカウント: ストアは、デバイス上の特定のサービスに対してローカルです。

## <a name="view-certificates-in-the-mmc-snap-in"></a>MMC スナップインで証明書を表示する

次の手順では、ローカルデバイス上のストアを調べて、適切な証明書を検索する方法を示します。
  
1. [**スタート**] メニューから [**実行**] を選択し、「 *mmc*」と入力します。

    MMC が表示されます。
  
2. [**ファイル**] メニューの [**スナップインの追加と削除**] を選択します。

    [**スナップインの追加と削除**] ウィンドウが表示されます。
  
3. [**利用できるスナップ**イン] の一覧から [**証明書**] を選択し、[**追加**] を選択します。  

    ![証明書スナップインの追加](./media/mmc-add-certificate-snap-in.png)
  
4. [**証明書スナップ**イン] ウィンドウで、[**コンピューターアカウント**] を選択し、[**次へ**] を選択します。
  
    必要に応じて、特定のサービスの現在のユーザーまたは**サービスアカウント**の **[ユーザーアカウント**] を選択できます。

    > [!NOTE]
    > デバイスの管理者でない場合は、自分のユーザーアカウントの証明書のみを管理できます。
  
5. **[コンピューターの選択**] ウィンドウで、[**ローカルコンピューター** ] を選択したままにして、[**完了**] を選択します。  
  
6. [スナップインの**追加と削除**] ウィンドウで、[ **OK]** を選択します。  
  
    ![証明書スナップインの追加](./media/mmc-certificate-snap-in-selected.png)

7. 省略可能: [**ファイル**] メニューの [**保存**] または [**名前を付けて保存**] を選択すると、後で使用するために MMC コンソールファイルが保存されます。  

8. MMC スナップインで証明書を表示するには、左側のウィンドウで [**コンソールルート**] を選択し、[**証明書 (ローカルコンピューター)**] を展開します。

    証明書の種類ごとにディレクトリの一覧が表示されます。 各証明書ディレクトリから、証明書の表示、エクスポート、インポート、および削除を行うことができます。

## <a name="view-certificates-with-the-certificate-manager-tool"></a>証明書マネージャーツールを使用して証明書を表示する

証明書マネージャーツールを使用して、証明書の表示、エクスポート、インポート、および削除を行うこともできます。

### <a name="to-view-certificates-for-the-local-device"></a>ローカルデバイスの証明書を表示するには

1. [**スタート**] メニューから [**実行**] を選択し、「 *certlm .msc*」と入力します。

    ローカルデバイスの証明書マネージャーツールが表示されます。
  
2. 証明書を表示するには、左側のウィンドウの [**証明書-ローカルコンピューター** ] で、表示する証明書の種類のディレクトリを展開します。

### <a name="to-view-certificates-for-the-current-user"></a>現在のユーザーの証明書を表示するには

1. **[スタート]** メニューから **[ファイル名を指定して実行]** メニューを選択し、「*certmgr.msc*」と入力します。

    現在のユーザーの証明書マネージャー ツールが表示されます。
  
2. 証明書を表示するには、左側のウィンドウの [**証明書-現在のユーザー** ] で、表示する証明書の種類のディレクトリを展開します。

## <a name="see-also"></a>関連項目

- [証明書の使用](working-with-certificates.md)
- [方法: 開発時に使用する一時的な証明書を作成する](how-to-create-temporary-certificates-for-use-during-development.md)
- [方法: 証明書の拇印を取得する](how-to-retrieve-the-thumbprint-of-a-certificate.md)
