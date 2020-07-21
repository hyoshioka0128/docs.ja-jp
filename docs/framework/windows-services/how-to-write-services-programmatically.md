---
title: '方法: プログラムでサービスを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- services, creating
- Windows Service applications, creating
ms.assetid: 3abbb2ec-78d2-41e6-b9f9-6662d4e2cdc7
author: ghogen
ms.openlocfilehash: 5637d569ad5261bff6865af4ab2ed8b7631d2d38
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053556"
---
# <a name="how-to-write-services-programmatically"></a>方法: プログラムでサービスを作成する
Windows サービス プロジェクトのテンプレートを使用しない場合は、継承などの基本要素を設定して独自のサービスを作成できます。 プログラミングによってサービスを作成する場合は、テンプレートでは自動化される手順を手動で行う必要があります。  
  
- サービス クラスが <xref:System.ServiceProcess.ServiceBase> クラスから継承されるように設定します。  
  
- サービス プロジェクトの `Main` メソッドを作成します。このメソッドは、実行するサービスを定義し、それに対して <xref:System.ServiceProcess.ServiceBase.Run%2A> メソッドを呼び出します。  
  
- <xref:System.ServiceProcess.ServiceBase.OnStart%2A> プロシージャと <xref:System.ServiceProcess.ServiceBase.OnStop%2A> プロシージャをオーバーライドし、任意の処理内容を記述します。  
  
### <a name="to-write-a-service-programmatically"></a>プログラミングによってサービスを作成するには  
  
1. 空のプロジェクトを作成し、必要な名前空間への参照を作成するには、次の手順を実行します。  
  
    1. **ソリューション エクスプローラー**で、 **[参照]** ノードを右クリックし、 **[参照の追加]** をクリックします。  
  
    2. **[.NET Framework]** タブで **System.dll** までスクロールして選択し、 **[選択]** をクリックします。  
  
    3. **System.ServiceProcess.dll** までスクロールして選択し、 **[選択]** をクリックします。  
  
    4. **[OK]** をクリックします。  
  
2. クラスを追加し、<xref:System.ServiceProcess.ServiceBase> から継承されるように設定します。  
  
     [!code-csharp[VbRadconService#7](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#7)]
     [!code-vb[VbRadconService#7](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#7)]  
  
3. 次のコードを追加してサービス クラスを設定します。  
  
     [!code-csharp[VbRadconService#8](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#8)]
     [!code-vb[VbRadconService#8](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#8)]  
  
4. クラスの `Main` メソッドを作成し、それを使用してクラスに含まれるサービスを定義します。`userService1` がクラスの名前です。  
  
     [!code-csharp[VbRadconService#9](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#9)]
     [!code-vb[VbRadconService#9](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#9)]  
  
5. <xref:System.ServiceProcess.ServiceBase.OnStart%2A> メソッドをオーバーライドし、サービスの開始時に実行する処理を定義します。  
  
     [!code-csharp[VbRadconService#10](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#10)]
     [!code-vb[VbRadconService#10](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#10)]  
  
6. 他に独自の処理を定義するメソッドがあればそれをオーバーライドし、サービスが行うアクションを記述します。  
  
7. サービス アプリケーションの必要なインストーラーを追加します。 詳細については、[サービス アプリケーションにインストーラーを追加する](how-to-add-installers-to-your-service-application.md)」を参照してください。  
  
8. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックして、プロジェクトを作成します。  
  
    > [!NOTE]
    > F5 キーを押してプロジェクトを実行しないでください。この方法ではサービス プロジェクトを実行できません。  
  
9. セットアップ プロジェクトと、サービスをインストールするカスタム処理を作成します。 例については、「[チュートリアル: コンポーネント デザイナーによる Windows サービス アプリケーションの作成](walkthrough-creating-a-windows-service-application-in-the-component-designer.md)」を参照してください。  
  
10. サービスをインストールします。 詳細については、[サービスをインストールおよびアンインストールする](how-to-install-and-uninstall-services.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Windows サービス アプリケーションの概要](introduction-to-windows-service-applications.md)
- [方法: Windows サービスを作成する](how-to-create-windows-services.md)
- [方法: サービス アプリケーションにインストーラーを追加する](how-to-add-installers-to-your-service-application.md)
- [方法: サービスに関する情報のログを記録する](how-to-log-information-about-services.md)
- [チュートリアル: コンポーネント デザイナーによる Windows サービス アプリケーションの作成](walkthrough-creating-a-windows-service-application-in-the-component-designer.md)
