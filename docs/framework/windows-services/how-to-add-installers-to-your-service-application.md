---
title: '方法: サービス アプリケーションにインストーラーを追加する'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, deploying
- installation components, adding to services
- installers, adding to services
- Windows Service applications, adding installers
- services, adding installers
- ServiceInstaller class, adding installers to services
- ServiceProcessInstaller class, adding installers to services
ms.assetid: 8b698e9a-b88e-4f44-ae45-e0c5ea0ae5a8
author: ghogen
ms.openlocfilehash: 99e2376c50f0b47cc21002b2926818707188805e
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053649"
---
# <a name="how-to-add-installers-to-your-service-application"></a>方法: サービス アプリケーションにインストーラーを追加する
Visual Studio には、サービス アプリケーションに関連付けられているリソースをインストールできるインストール コンポーネントが付属しています。 インストール コンポーネントは、個々のサービスをインストール先のシステムに登録し、サービス コントロール マネージャーにサービスが存在することを認識させます。 サービス アプリケーションを操作するときは、[プロパティ] ウィンドウでリンクを選択して、適切なインストーラーをプロジェクトに自動的に追加することができます。  
  
> [!NOTE]
> サービスに対するプロパティの値は、サービス クラスからインストーラー クラスにコピーされます。 サービス クラスでプロパティの値を更新した場合、インストーラーでは自動的には更新されません。  
  
 インストーラーをプロジェクトに追加すると、新しいクラス (既定の名前は `ProjectInstaller`) がプロジェクトに作成され、その中に適切なインストール コンポーネントのインスタンスが作成されます。 このクラスは、プロジェクトで必要なすべてのインストール コンポーネントの中心的な場所として機能します。 たとえば、2 番目のサービスをアプリケーションに追加し、[インストーラーの追加] リンクをクリックしても、2 番目のインストーラー クラスは作成されません。代わりに、2 番目のサービスに必要な追加のインストール コンポーネントは、既存のクラスに追加されます。  
  
 サービスが正しくインストールされるようにするために、インストーラー内で特殊なコーディングを行う必要はありません。 ただし、インストール プロセスに特別な機能を追加する必要がある場合は、インストーラーの内容の変更が必要になることがあります。  
  
> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio IDE のカスタマイズ](/visualstudio/ide/personalizing-the-visual-studio-ide)」を参照してください。  
  
### <a name="to-add-installers-to-your-service-application"></a>サービス アプリケーションにインストーラーを追加するには  
  
1. **ソリューション エクスプローラー**で、インストール コンポーネントを追加するサービスの **[デザイン]** ビューにアクセスします。  
  
2. デザイナーの背景をクリックして、サービスの内容ではなくサービス自体を選択します。  
  
3. デザイナーにフォーカスを置いた状態で右クリックし、 **[インストーラーの追加]** をクリックします。  
  
     新しいクラス `ProjectInstaller`、および 2 つのインストール コンポーネント <xref:System.ServiceProcess.ServiceProcessInstaller> と <xref:System.ServiceProcess.ServiceInstaller> がプロジェクトに追加され、サービスのプロパティ値がコンポーネントにコピーされます。  
  
4. <xref:System.ServiceProcess.ServiceInstaller> コンポーネントをクリックし、<xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> プロパティが、サービス自体の <xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> プロパティと同じ値に設定されていることを確認します。  
  
5. サービスの開始方法を決定するには、<xref:System.ServiceProcess.ServiceInstaller> コンポーネントをクリックし、<xref:System.ServiceProcess.ServiceInstaller.StartType%2A> プロパティを適切な値に設定します。  
  
    |[値]|結果|  
    |-----------|------------|  
    |<xref:System.ServiceProcess.ServiceStartMode.Manual>|インストールの後、サービスを手動で開始する必要があります。 詳細については、[サービスを開始する](how-to-start-services.md)」を参照してください。|  
    |<xref:System.ServiceProcess.ServiceStartMode.Automatic>|サービスは、コンピューターが再起動されるたびに、自動的に開始します。|  
    |<xref:System.ServiceProcess.ServiceStartMode.Disabled>|サービスは開始できません。|  
  
6. サービスが実行するセキュリティ コンテキストを決定するには、<xref:System.ServiceProcess.ServiceProcessInstaller> コンポーネントをクリックし、適切なプロパティ値を設定します。 詳細については、[サービスのセキュリティ コンテキストを指定する](how-to-specify-the-security-context-for-services.md)」を参照してください。  
  
7. カスタム処理を実行する必要があるメソッドをオーバーライドします。  
  
8. プロジェクトの追加サービスごとに、手順 1 から 7 を実行します。  
  
    > [!NOTE]
    > プロジェクトの追加サービスごとに、新しい <xref:System.ServiceProcess.ServiceInstaller> コンポーネントをプロジェクトの `ProjectInstaller` クラスに追加する必要があります。 手順 3 で追加した <xref:System.ServiceProcess.ServiceProcessInstaller> コンポーネントは、プロジェクト内のすべての個別サービス インストーラーで動作します。  
  
## <a name="see-also"></a>関連項目

- [Windows サービス アプリケーションの概要](introduction-to-windows-service-applications.md)
- [方法: サービスをインストールおよびアンインストールする](how-to-install-and-uninstall-services.md)
- [方法: サービスを開始する](how-to-start-services.md)
- [方法: サービスのセキュリティ コンテキストを指定する](how-to-specify-the-security-context-for-services.md)
