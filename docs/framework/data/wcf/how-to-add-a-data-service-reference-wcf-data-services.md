---
title: '方法: データ サービス参照を追加する (WCF Data Services)'
ms.date: 08/24/2018
helpviewer_keywords:
- WCF Data Services, configuring
ms.assetid: 62c6f318-3ee1-433a-b7a3-efa234c3034c
ms.openlocfilehash: 42d89cf87b5fe9bbdb229f10cd6a0e340d4c08fd
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70790740"
---
# <a name="how-to-add-a-data-service-reference-wcf-data-services"></a>方法: データ サービス参照を追加する (WCF Data Services)

Visual Studio の **[サービス参照の追加]** ダイアログを使用して、WCF Data Services への参照を追加できます。 参照をデータ サービスに追加すると、Visual Studio で開発したクライアント アプリケーションのデータ サービスに容易にアクセスできます。 この手順を完了すると、データ サービスから取得されたメタデータに基づいてデータ クラスが生成されます。 詳しくは、「[データ サービス クライアント ライブラリの生成](generating-the-data-service-client-library-wcf-data-services.md)」をご覧ください。

## <a name="add-a-data-service-reference"></a>データ サービスの参照を追加する

1. (オプション) データ サービスがソリューションの一部ではなく、実行していない場合は、データ サービスを開始して、データ サービスの URI を記録します。

2. Visual Studio の**ソリューション エクスプローラー**で、クライアント プロジェクトを右クリックして、 **[追加]**  >  **[サービス参照]** を選択します。

3. データ サービスが現在のソリューションの一部である場合は、 **[探索]** をクリックします。

     \- または -

     **[アドレス]** ボックスにデータ サービスのベース URL (`http://localhost:1234/Northwind.svc` など) を入力して **[移動]** をクリックします。

4. **[OK]** を選択します。

     データ サービス リソースにアクセスして操作できるデータ クラスが含まれる新しいコード ファイルが、プロジェクトに追加されます。

## <a name="see-also"></a>関連項目

- [クイック スタート](quickstart-wcf-data-services.md)
