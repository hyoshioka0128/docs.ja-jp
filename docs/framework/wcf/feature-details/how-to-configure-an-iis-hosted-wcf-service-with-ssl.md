---
title: '方法: IIS でホストされる WCF サービスに SSL を構成する'
description: Iis でホストされる WCF サービスで HTTP トランスポートセキュリティを使用するように設定する方法について説明します。これには、IIS に登録されている証明書が必要です。
ms.date: 03/30/2017
ms.assetid: df2fe31f-a4bb-4024-92ca-b74ba055e038
ms.openlocfilehash: 8dc4692863d93e407a122c0ba93ae38323b8b213
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85245259"
---
# <a name="how-to-configure-an-iis-hosted-wcf-service-with-ssl"></a>方法: IIS でホストされる WCF サービスに SSL を構成する
ここでは、HTTP トランスポート セキュリティを使用するように IIS でホストされる WCF サービスをセットアップする方法について説明します。 HTTP トランスポート セキュリティを使用するには、SSL 証明書が IIS に登録されている必要があります。 SSL 証明書がない場合は、IIS を使用してテスト証明書を生成できます。 次に、Web サイトに SSL バインディングを追加し、Web サイトの認証プロパティを構成する必要があります。 最後に、HTTPS を使用するように WCF サービスを構成する必要があります。  
  
### <a name="creating-a-self-signed-certificate"></a>自己署名証明書の作成  
  
1. インターネット インフォメーション サービス マネージャー (inetmgr.exe) を開き、左側のツリー ビューでコンピューター名を選択します。 画面の右側で [サーバー証明書] を選択します。  
  
     ![IIS マネージャー ホーム画面](media/mg-inetmgrhome.jpg "mg_INetMgrHome")  
  
2. [サーバー証明書] ウィンドウで、[**自己署名証明書の作成...** ] をクリックします。 リンクをクリックします。  
  
     ![IIS での自己&#45;署名入り証明書の作成](media/mg-createselfsignedcert.jpg "mg_CreateSelfSignedCert")  
  
3. 自己署名証明書のフレンドリ名を入力し、[ **OK]** をクリックします。  
  
     ![自己&#45;署名入り証明書の作成ダイアログ](media/mg-mycert.jpg "mg_MyCert")  
  
     新しく作成された自己署名証明書の詳細が [**サーバー証明書**] ウィンドウに表示されるようになりました。  
  
     ![[サーバー証明書] ウィンドウ](media/mg-servercertificatewindow.jpg "mg_ServerCertificateWindow")  
  
     生成された証明書が、信頼されたルート証明機関ストアにインストールされます。  
  
### <a name="add-ssl-binding"></a>SSL バインドの追加  
  
1. 引き続きインターネットインフォメーションサービスマネージャーで、[**サイト**] フォルダーを展開し、画面の左側にあるツリービューの [**既定の Web サイト**] フォルダーを展開します。  
  
2. [**バインド...** ] をクリックします。 ウィンドウの右上隅にある [**アクション**] セクションのリンク。  
  
     ![SSL バインディングの追加](media/mg-addsslbinding.jpg "mg_AddSSLBinding")  
  
3. [サイトバインド] ウィンドウで、[**追加**] ボタンをクリックします。  
  
     ![[サイト バインド] ダイアログ](media/mg-sitebindingsdialog.jpg "mg_SiteBindingsDialog")  
  
4. [**サイトバインドの追加**] ダイアログで、[種類] に [https] を、先ほど作成した自己署名証明書のフレンドリ名を選択します。  
  
     ![サイト バインディングの例](media/mg-mycertbinding.jpg "mg_MyCertBinding")  
  
### <a name="configure-virtual-directory-for-ssl"></a>SSL の仮想ディレクトリの構成  
  
1. インターネット インフォメーション サービス マネージャーで、WCF のセキュリティで保護されたサービスが含まれている仮想ディレクトリを選択します。  
  
2. ウィンドウの中央のウィンドウで、[IIS] セクションの [ **SSL 設定**] を選択します。  
  
     ![仮想ディレクトリの SSL 設定](media/mg-sslsettingsforvdir.jpg "mg_SSLSettingsForVDir")  
  
3. [SSL 設定] ウィンドウで、[ **Ssl が必要**] チェックボックスをオンにし、画面の右側の [**アクション**] セクションの [**適用**] リンクをクリックします。  
  
     ![仮想ディレクトリの SSL 設定](media/mg-vdirsslsettings.JPG "mg_VDirSSLSettings")  
  
### <a name="configure-wcf-service-for-http-transport-security"></a>HTTP トランスポート セキュリティのための WCF サービスの構成  
  
1. WCF サービスの Web.config で、次の XML に示すように、トランスポート セキュリティを使用するよう HTTP バインドを構成します。  
  
    ```xml  
    <bindings>  
          <basicHttpBinding>  
            <binding name="secureHttpBinding">  
              <security mode="Transport">  
                <transport clientCredentialType="None"/>  
              </security>  
            </binding>  
          </basicHttpBinding>  
    </bindings>  
    ```  
  
2. 次の XML に示すように、サービスとサービス エンドポイントを指定します。  
  
    ```xml  
    <services>  
          <service name="MySecureWCFService.Service1">  
            <endpoint address=""  
                      binding="basicHttpBinding"  
                      bindingConfiguration="secureHttpBinding"  
                      contract="MySecureWCFService.IService1"/>  
  
            <endpoint address="mex"  
                      binding="mexHttpsBinding"  
                      contract="IMetadataExchange" />  
          </service>  
    </services>  
    ```  
  
## <a name="example"></a>例  
 次は、HTTP トランスポート セキュリティを使用した WCF サービスの web.config ファイルの詳細な例です。  
  
```xml  
<?xml version="1.0"?>  
<configuration>  
  
  <system.web>  
    <compilation debug="true" targetFramework="4.0" />  
  </system.web>  
  <system.serviceModel>  
    <services>  
      <service name="MySecureWCFService.Service1">  
        <endpoint address=""  
                  binding="basicHttpBinding"  
                  bindingConfiguration="secureHttpBinding"  
                  contract="MySecureWCFService.IService1"/>  
  
        <endpoint address="mex"  
                  binding="mexHttpsBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
    <bindings>  
      <basicHttpBinding>  
        <binding name="secureHttpBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="None"/>  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior>  
          <!-- To avoid disclosing metadata information, set the value below to false and remove the metadata endpoint above before deployment -->  
          <serviceMetadata httpsGetEnabled="true"/>  
          <!-- To receive exception details in faults for debugging purposes, set the value below to true.  Set to false before deployment to avoid disclosing exception information -->  
          <serviceDebug includeExceptionDetailInFaults="false"/>  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <serviceHostingEnvironment multipleSiteBindingsEnabled="true" />  
  </system.serviceModel>  
  <system.webServer>  
    <modules runAllManagedModulesForAllRequests="true"/>  
  </system.webServer>  
  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [インターネット インフォメーション サービスでのホスティング](hosting-in-internet-information-services.md)
- [インターネット インフォメーション サービスのホスティング手順](../samples/internet-information-service-hosting-instructions.md)
- [インターネット インフォメーション サービス ホスティングのベスト プラクティス](internet-information-services-hosting-best-practices.md)
- [インライン コードを使用した IIS ホスティング](../samples/iis-hosting-using-inline-code.md)
