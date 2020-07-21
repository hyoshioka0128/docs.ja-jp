---
title: '方法: メッセージング アクティビティを使用してワークフロー サービスを作成する'
ms.date: 03/30/2017
ms.assetid: 53d094e2-6901-4aa1-88b8-024b27ccf78b
ms.openlocfilehash: b4991fc9f8a6c45cae3943f1506247c42ed2b30b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597125"
---
# <a name="how-to-create-a-workflow-service-with-messaging-activities"></a>方法: メッセージング アクティビティを使用してワークフロー サービスを作成する
このトピックでは、メッセージング アクティビティを使用して単純なワークフロー サービスを作成する方法について説明します。 ここでは、メッセージング アクティビティだけで構成されるサービスのワークフロー サービスを作成する機構に重点を置きます。 実際のサービスでは、ワークフローに他の多くのアクティビティが含まれます。 このサービスは、文字列を取得して、それを呼び出し元に返す、Echo という 1 つの操作を実装します。 このトピックは、一連の 2 つのトピックの最初のものです。 次のトピック「[方法: ワークフローアプリケーションからサービスにアクセス](how-to-access-a-service-from-a-workflow-application.md)する」では、このトピックで作成したサービスを呼び出すことができるワークフローアプリケーションを作成する方法について説明します。  
  
### <a name="to-create-a-workflow-service-project"></a>ワークフロー サービス プロジェクトを作成するには  
  
1. Visual Studio 2012 を起動します。  
  
2. [**ファイル**] メニューの [**新規作成**] をポイントし、[**プロジェクト**] をクリックして [**新しいプロジェクト] ダイアログ**を表示します。 プロジェクトの種類の一覧から、インストールされているテンプレートと**WCF ワークフローサービスアプリケーション**の一覧から [**ワークフロー** ] を選択します。 次の図に示すように、プロジェクトにという名前 `MyWFService` を付け、既定の場所を使用します。  
  
     [ **OK** ] ボタンをクリックして、[**新しいプロジェクト] ダイアログボックス**を閉じます。  
  
3. プロジェクトが作成されると、次の図に示すように、Service1.xamlx ファイルがデザイナーで開かれます。  
  
     ![スクリーンショットは、デザイナーで開かれている Service1 .xamlx ファイルを示しています。](./media/how-to-create-a-workflow-service-with-messaging-activities/default-workflow-service.jpg)  
  
     [**シーケンシャルサービス**] というラベルの付いたアクティビティを右クリックし、[**削除**] を選択します。  
  
### <a name="to-implement-the-workflow-service"></a>ワークフロー サービスを実装するには  
  
1. 画面の左側にある [**ツールボックス**] タブを選択してツールボックスを表示し、プッシュピンをクリックしてウィンドウを開いたままにします。 次の図に示すように、[ツールボックス] の [**メッセージング**] セクションを展開して、メッセージングアクティビティとメッセージングアクティビティテンプレートを表示します。  
  
     ![メッセージングセクションが展開されたツールボックスを示すスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/toolbox-messaging-section.jpg)  
  
2. **Receiveandsendreply**テンプレートをワークフローデザイナーにドラッグアンドドロップします。 これに <xref:System.Activities.Statements.Sequence> より、次の図に示すように、 **Receive**アクティビティの後にアクティビティが作成さ <xref:System.ServiceModel.Activities.SendReply> れます。  
  
     ![ReceiveAndSendReply テンプレートを示すスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/receiveandsendreply-template.jpg)  
  
     <xref:System.ServiceModel.Activities.SendReply> アクティビティの <xref:System.ServiceModel.Activities.SendReply.Request%2A> プロパティは `Receive` に設定されています。これは、<xref:System.ServiceModel.Activities.Receive> アクティビティが応答する <xref:System.ServiceModel.Activities.SendReply> アクティビティの名前です。  
  
3. アクティビティの <xref:System.ServiceModel.Activities.Receive> 種類で、 `Echo` **OperationName**という名前のテキストボックスに入力します。 これにより、サービスが実装する操作の名前が定義されます。  
  
     ![操作名を指定する場所を示すスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/define-operation-name.jpg)  
  
4. アクティビティを選択した状態で、 <xref:System.ServiceModel.Activities.Receive> まだ開いていない場合は [**表示**] メニューの [**プロパティウィンドウ]** をクリックして、[プロパティ] ウィンドウを開きます。 [**プロパティ] ウィンドウ**で、次の図に示すように、 **CanCreateInstance**が表示されるまで下にスクロールし、チェックボックスをオンにします。 この設定によって、ワークフロー サービス ホストはメッセージが受信されると (必要に応じて) サービスの新しいインスタンスを作成できるようになります。  
  
     ![CanCreateInstance プロパティを示すスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/cancreateinstance-property.jpg)  
  
5. アクティビティを選択し、 <xref:System.Activities.Statements.Sequence> デザイナーの左下隅にある [**変数**] ボタンをクリックします。 これにより、変数エディターが開かれます。 [**変数の作成**] リンクをクリックして、操作に送信される文字列を格納する変数を追加します。 次の図に示すように、変数にという名前 `msg` を付け、その**変数**の型を String に設定します。  
  
     ![変数を追加する方法を示すスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/add-variable-msg-string.jpg)  
  
     [**変数**] ボタンをもう一度クリックして、変数エディターを閉じます。  
  
6. [定義] をクリックし**ます**。 [コンテンツ定義] ダイアログボックスを表示するには、アクティビティの [**コンテンツ**] テキストボックス内のリンクを選択し <xref:System.ServiceModel.Activities.Receive> ます。 **Content Definition** [**パラメーター** ] オプションボタンを選択し、[**新しいパラメーターの追加**] リンクをクリックし、[名前] テキストボックスに「」と入力し `inMsg` **name**ます。次の図に示すように、[**型**] ボックスで [**文字列**] を選択し、[ `msg` **割り当て先**] テキストボックスに「」と入力します。  
  
     ![パラメーターの内容の追加を示すスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/adding-parameters-content.jpg)  
  
     これにより、Receive アクティビティが文字列パラメーターを受け取り、そのデータが `msg` 変数にバインドされるように指定されます。 [ **OK** ] をクリックして、[**コンテンツ定義**] ダイアログを閉じます。  
  
7. アクティビティの [**コンテンツ**] ボックスの [**定義...** ] リンクをクリックして <xref:System.ServiceModel.Activities.SendReply> 、[**コンテンツ定義**] ダイアログを表示します。 [**パラメーター** ] オプションボタンを選択し、[**新しいパラメーターの追加**] リンクをクリックします。次の図に示すように、[名前] ボックスに「」と入力し、[ `outMsg` **型**] ドロップダウンリストボックスで [**文字列**] を選択し、[ **name** `msg` **値**] テキストボックスに「」と入力します。  
  
     ![OutMsg パラメーターを追加する方法を示すスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/outmsg-parameters-content.jpg)  
  
     これにより、<xref:System.ServiceModel.Activities.SendReply> アクティビティがメッセージまたはメッセージ コントラクト型を送信し、そのデータが `msg` 変数にバインドされるように指定されます。 これは <xref:System.ServiceModel.Activities.SendReply> アクティビティであるため、`msg` のデータは、アクティビティがクライアントに送り返すメッセージの設定に使用されます。 [ **OK** ] をクリックして、[**コンテンツ定義**] ダイアログを閉じます。  
  
8. [**ビルド**] メニューの [**ソリューションのビルド**] をクリックして、ソリューションを保存してビルドします。  
  
## <a name="configure-the-workflow-service-project"></a>ワークフロー サービス プロジェクトの構成  
 ワークフロー サービスは完成しました。 ここでは、ホストと実行を容易にするように、ワークフロー サービス ソリューションを構成する方法について説明します。 このソリューションでは、ASP.NET 開発サーバーを使用してサービスをホストします。  
  
#### <a name="to-set-project-start-up-options"></a>プロジェクトのスタートアップ オプションを設定するには  
  
1. **ソリューションエクスプローラー**で、[ **myのサービス**] を右クリックし、[**プロパティ**] をクリックして、[**プロジェクトのプロパティ**] ダイアログボックスを表示します。  
  
2. [ **Web** ] タブを選択し、[**開始動作**] で [**特定のページ**] を選択し、 `Service1.xamlx` 次の図に示すように、テキストボックスに「」と入力します。  
  
     ![[プロジェクトのプロパティ] ダイアログボックスが表示されるスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/project-properties-dialog.jpg)  
  
     これにより、ASP.NET 開発サーバーの Service1.xamlx で定義されたサービスがホストされます。  
  
3. Ctrl キーを押しながら F5 キーを押して、サービスを起動します。 次の図に示すように、ASP.NET 開発サーバーのアイコンが、デスクトップの右下側に表示されます。  
  
     ![ASP.NET Developer サーバーアイコンを示すスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/asp-net-dev-server-icon.jpg)  
  
     また、Internet Explorer に、サービスの WCF サービス ヘルプ ページが表示されます。  
  
     ![WCF サービスのヘルプページを示すスクリーンショット。](./media/how-to-create-a-workflow-service-with-messaging-activities/wcf-service-help-page.jpg)  
  
4. 「[方法: ワークフローアプリケーションからサービスにアクセス](how-to-access-a-service-from-a-workflow-application.md)する」のトピックに進み、このサービスを呼び出すワークフロークライアントを作成します。  
  
## <a name="see-also"></a>関連項目

- [ワークフロー サービス](workflow-services.md)
- [ワークフロー サービスのホストの概要](hosting-workflow-services-overview.md)
- [メッセージング アクティビティ](messaging-activities.md)
