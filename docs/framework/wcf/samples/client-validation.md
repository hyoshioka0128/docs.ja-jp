---
title: クライアント検証
ms.date: 03/30/2017
ms.assetid: f0c1f805-1a81-4d0d-a112-bf5e2e87a631
ms.openlocfilehash: dce11ec2e3ef552c0c53e1faf89a12bc13b66ae0
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84585325"
---
# <a name="client-validation"></a>クライアント検証
サービスは頻繁にメタデータを公開し、クライアント プロキシの型を自動的に生成して構成できるようにします。 サービスが信頼できない場合、クライアント アプリケーションでは、セキュリティ、トランザクション、サービス コントラクトの型などに関して、メタデータがクライアント アプリケーションのポリシーに合致しているかどうか検証する必要があります。 次のサンプルでは、サービス エンドポイントを検証するクライアント エンドポイントの動作を記述して、サービス エンドポイントを安全に使用できることを確認する方法を示します。  
  
 サービスは 4 つのサービス エンドポイントを公開します。 1 つ目は WSDualHttpBinding を使用するエンドポイント、2 つ目は NTLM 認証を使用するエンドポイント、3 つ目はトランザクション フローを有効にするエンドポイント、4 つ目は証明書ベースの認証を使用するエンドポイントです。  
  
 クライアントは <xref:System.ServiceModel.Description.MetadataResolver> クラスを使用してサービスのメタデータを取得します。 クライアントは検証動作を使用して、二重バインディング、NTLM 認証、およびトランザクション フローを禁止するポリシーを適用します。 <xref:System.ServiceModel.Description.ServiceEndpoint>クライアントアプリケーションは、サービスのメタデータからインポートされたインスタンスごとに、エンドポイント `InternetClientValidatorBehavior` <xref:System.ServiceModel.Description.ServiceEndpoint> に接続するために Windows Communication Foundation (WCF) クライアントを使用する前に、エンドポイント動作のインスタンスをに追加します。 動作の `Validate` メソッドはサービスで操作が呼び出される前に実行され、`InvalidOperationExceptions` をスローすることによってクライアントのポリシーを適用します。  
  
### <a name="to-build-the-sample"></a>サンプルをビルドするには  
  
1. ソリューションをビルドするには、「 [Windows Communication Foundation サンプルのビルド](building-the-samples.md)」の手順に従います。  
  
### <a name="to-run-the-sample-on-the-same-computer"></a>サンプルを同じコンピューターで実行するには  
  
1. 管理者特権で Visual Studio の開発者コマンドプロンプトを開き、サンプルのインストールフォルダーから Setup.exe を実行します。 これにより、サンプルの実行に必要なすべての証明書がインストールされます。  
  
2. サービス アプリケーションを \service\bin\Debug で実行します。  
  
3. クライアント アプリケーションを \client\bin\Debug で実行します。 クライアント アクティビティがクライアントのコンソール アプリケーションに表示されます。  
  
4. クライアントとサービスが通信できない場合は、「 [WCF サンプルのトラブルシューティングのヒント](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))」を参照してください。  
  
5. サンプルの使用が終わったら、Cleanup.bat を実行して証明書を削除してください。 他のセキュリティ サンプルでも同じ証明書を使用します。  
  
### <a name="to-run-the-sample-across-computers"></a>サンプルを複数のコンピューターで実行するには  
  
1. サーバーで、[Visual Studio の開発者コマンドプロンプトに管理者特権で実行する] で、「」と入力 `setup.bat service` します。 引数を指定してを実行する `setup.bat` `service` と、コンピューターの完全修飾ドメイン名を使用してサービス証明書が作成され、service .cer という名前のファイルにエクスポートされます。  
  
2. サーバーで、App.config を編集して新しい証明書の名前を反映します。 つまり、 `findValue` 要素の属性を [\<serviceCertificate>](../../configure-apps/file-schema/wcf/servicecertificate-of-clientcredentials-element.md) コンピューターの完全修飾ドメイン名に変更します。  
  
3. Service.cer ファイルを、サービス ディレクトリからクライアント コンピューターのクライアント ディレクトリにコピーします。  
  
4. クライアントで、管理者特権を使用して Visual Studio の開発者コマンドプロンプトを開き、「」と入力し `setup.bat client` ます。 引数を指定してを実行する `setup.bat` `client` と、Client.com という名前のクライアント証明書が作成され、クライアント証明書がクライアント .cer という名前のファイルにエクスポートされます。  
  
5. client.cs ファイルで、MEX エンドポイントと、既定のサーバー証明書を設定するための `findValue` のアドレス値を、サービスの新しいアドレスに合わせて変更します。 そのためには、localhost をサーバーの完全修飾ドメイン名に置き換えます。 Rebuild。  
  
6. Client.cer ファイルを、クライアント ディレクトリからサーバーのサービス ディレクトリにコピーします。  
  
7. クライアントで、管理者特権で開かれた Visual Studio の開発者コマンドプロンプトで Importservicecert.bat を実行します。 これにより、サービス証明書が Service.cer ファイルから CurrentUser - TrustedPeople ストアにインポートされます。  
  
8. サーバーで、管理者特権で開かれた Visual Studio の開発者コマンドプロンプトで Importclientcert.bat を実行します。 これにより、クライアント証明書が Client.cer ファイルから LocalMachine - TrustedPeople ストアにインポートされます。  
  
9. サービス コンピューターの Visual Studio でサービス プロジェクトをビルドし、service.exe を実行します。  
  
10. クライアント コンピューターで、client.exe を実行します。  
  
    1. クライアントとサービスが通信できない場合は、「 [WCF サンプルのトラブルシューティングのヒント](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms751511(v=vs.90))」を参照してください。  
  
### <a name="to-clean-up-after-the-sample"></a>サンプルの実行後にクリーンアップするには  
  
- サンプルの実行が終わったら、サンプル フォルダーにある Cleanup.bat を実行します。  
  
    > [!NOTE]
    > このサンプルを複数のコンピューターで実行している場合、このスクリプトはサービス証明書をクライアントから削除しません。 コンピューター間で証明書を使用する WCF サンプルを実行している場合は、CurrentUser-TrustedPeople ストアにインストールされているサービス証明書を必ずオフにしてください。 削除するには、コマンド `certmgr -del -r CurrentUser -s TrustedPeople -c -n <Fully Qualified Server Machine Name>. For example: certmgr -del -r CurrentUser -s TrustedPeople -c -n server1.contoso.com` を実行します。  
  
## <a name="see-also"></a>関連項目

- [メタデータを使用する](../feature-details/using-metadata.md)
