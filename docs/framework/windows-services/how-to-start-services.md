---
title: '方法: サービスを開始する'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, starting
- services, starting
ms.assetid: 9ea77955-2d96-4c3d-913c-14db7604cdad
author: ghogen
ms.openlocfilehash: 75fd3aba88bdffbe536ad5dab14996913d0a9d22
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053570"
---
# <a name="how-to-start-services"></a>方法: サービスを開始する

サービスをインストールした後で、サービスを起動します。 起動することで、サービス クラスの <xref:System.ServiceProcess.ServiceBase.OnStart%2A> メソッドが呼び出されます。 通常、<xref:System.ServiceProcess.ServiceBase.OnStart%2A> メソッドにはサービスが本来行う処理を定義します。 サービスの起動後は、手動で一時停止または停止するまで、アクティブの状態を維持します。

サービスを自動で起動するか手動で起動するかを設定できます。 自動的に起動するサービスは、そのサービスがインストールされているコンピューターを再起動したとき、または初めて電源を入れたときに起動します。 手動で起動するサービスは、ユーザーが起動する必要があります。

> [!NOTE]
> 既定では、Visual Studio で作成されたサービスは手動で起動するように設定されます。

サービスを手動で起動するには、**サーバー エクスプローラー**または**サービス コントロール マネージャー**を使用します。<xref:System.ServiceProcess.ServiceController> コンポーネントを使ってコードによって起動することもできます。

<xref:System.ServiceProcess.ServiceInstaller.StartType%2A> クラスの <xref:System.ServiceProcess.ServiceInstaller> プロパティを設定し、サービスを手動で起動するか自動で起動するかを指定します。

### <a name="to-specify-how-a-service-should-start"></a>サービスの起動方法を指定するには

1. サービスの作成後、必要なインストーラーを追加します。 詳細については、[サービス アプリケーションにインストーラーを追加する](how-to-add-installers-to-your-service-application.md)」をご覧ください。

2. デザイナーで、対象となるサービスのインストーラーをクリックします。

3. **[プロパティ]** ウィンドウで、<xref:System.ServiceProcess.ServiceInstaller.StartType%2A> プロパティに次のいずれかの値を設定します。

    |サービスを起動するタイミング|設定値|
    |----------------------------------|--------------------|
    |コンピューターを再起動したとき。|**自動**|
    |明示的なユーザー アクションによってサービスを開始するとき。|**手動**|

    > [!TIP]
    > サービスが起動しないようにするには、<xref:System.ServiceProcess.ServiceInstaller.StartType%2A> プロパティを **[無効]** に設定します。 サーバーを数回再起動することが見込まれる場合は、サービスを自動的に起動しないように設定することで、再起動の時間を短縮できます。

    > [!NOTE]
    > 以上のプロパティやその他のプロパティの設定は、サービスのインストール後に変更できます。

    <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> プロパティが **[手動]** に設定されているサービスを起動するには、**サーバー エクスプローラー**または **Windows サービス コントロール マネージャー**を使います。また、コードで起動することもできます。 起動方法によっては、**サービス コントロール マネージャー**のコンテキストではサービスを起動しません。**サーバー エクスプローラー**によるサービスの起動とコードによるサービスの起動の場合は、実際にはコントローラーを操作しています。

### <a name="to-manually-start-a-service-from-server-explorer"></a>サーバー エクスプローラーでサービスを手動起動するには

1. サーバーが**サーバー エクスプローラー**の一覧にない場合は追加します。 詳細については、「方法:サーバー エクスプローラー/データベース エクスプローラーにアクセスして初期化する」を参照してください。

2. **[サービス]** ノードを展開し、開始するサービスを検索します。

3. サービス名を右クリックし、 **[開始]** をクリックします。

### <a name="to-manually-start-a-service-from-services-control-manager"></a>サービス制御マネージャーでサービスを手動起動するには

1. **サービス コントロール マネージャー**を次のいずれかの方法で開きます。

    - Windows XP および Windows 2000 Professional のデスクトップで、 **[マイ コンピューター]** を右クリックし、 **[管理]** をクリックします。 表示されるダイアログ ボックスで、 **[サービスとアプリケーション]** ノードを展開します。

      \- または

    - Windows Server 2003 および Windows 2000 Server では、 **[スタート]** メニューの **[プログラム]** をポイントし、 **[管理ツール]** をポイントして、 **[サービス]** をクリックします。

      > [!NOTE]
      > Windows NT Version 4.0 では、 **[コントロール パネル]** でこのダイアログ ボックスを開くことができます。

    ウィンドウの **[サービス]** セクションに、サービスが一覧表示されます。

2. 一覧で目的のサービスを右クリックし、 **[開始]** をクリックします。

### <a name="to-manually-start-a-service-from-code"></a>コードでサービスを手動起動するには

1. <xref:System.ServiceProcess.ServiceController> クラスのインスタンスを作成し、管理対象となるサービスと対話するように設定します。

2. <xref:System.ServiceProcess.ServiceController.Start%2A> メソッドを呼び出してサービスを起動します。

## <a name="see-also"></a>関連項目

- [Windows サービス アプリケーションの概要](introduction-to-windows-service-applications.md)
- [方法: Windows サービスを作成する](how-to-create-windows-services.md)
- [方法: サービス アプリケーションにインストーラーを追加する](how-to-add-installers-to-your-service-application.md)
