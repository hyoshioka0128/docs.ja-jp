---
title: 接続文字列と構成ファイル
description: セキュリティとメンテナンスのためのベスト プラクティスとして、ADO.NET アプリケーションの接続文字列をアプリケーション構成ファイルに格納する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 37df2641-661e-407a-a3fb-7bf9540f01e8
ms.openlocfilehash: 572c5be1bd639e8d4b38935f5be49782f0b0316e
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287039"
---
# <a name="connection-strings-and-configuration-files"></a>接続文字列と構成ファイル

接続文字列をアプリケーションのコードに組み込むと、セキュリティ上の脆弱性やメンテナンスの問題を引き起こす可能性があります。 アプリケーションのソース コード内にコンパイルされた暗号化されていない接続文字列は、[Ildasm.exe (IL 逆アセンブラー)](../../tools/ildasm-exe-il-disassembler.md) ツールを使用して参照することができます。 さらに、接続文字列が変わるたびにアプリケーションを再コンパイルする必要性が生じます。 そのため、接続文字列はアプリケーション構成ファイルに保存することをお勧めします。  
  
## <a name="working-with-application-configuration-files"></a>アプリケーション構成ファイルの使用  
 アプリケーション構成ファイルには、特定のアプリケーションに固有の設定が格納されます。 たとえば、ASP.NET アプリケーションには少なくとも 1 つの **web.config** ファイルが存在するほか、Windows アプリケーションにも必要に応じて **app.config** ファイルを割り当てることができます。 構成ファイルの名前と場所はアプリケーションのホストによって異なりますが、どの構成ファイルにも共通の要素があります。  
  
### <a name="the-connectionstrings-section"></a>connectionStrings セクション  
 接続文字列は、アプリケーション構成ファイルの**connectionStrings** 要素の **configuration** セクションにキーと値のペアとして格納できます。 子要素には、**add**、**clear**、および **remove** が存在します。  
  
 次の構成ファイル フラグメントは、接続文字列を格納するためのスキーマと構文の例を示しています。 **name** 属性は、実行時に取得する接続文字列を一意に識別するための名前です。 **providerName** は、machine.config ファイルに登録された .NET Framework データ プロバイダーの不変名です。  
  
```xml  
<?xml version='1.0' encoding='utf-8'?>  
  <configuration>  
    <connectionStrings>  
      <clear />  
      <add name="Name"
       providerName="System.Data.ProviderName"
       connectionString="Valid Connection String;" />  
    </connectionStrings>  
  </configuration>  
```  
  
> [!NOTE]
> 構成ファイルに接続文字列の一部を保存しておき、<xref:System.Data.Common.DbConnectionStringBuilder> クラスを使用して実行時に補完できます。 接続文字列の要素を事前に知ることができない場合や、機密情報を構成ファイルに保存したくない場合には有効な手段です。 詳細については、「[接続文字列ビルダー](connection-string-builders.md)」をご覧ください。  
  
### <a name="using-external-configuration-files"></a>外部構成ファイルの使用  
 外部構成ファイルとは、単一のセクションから成る、構成ファイルのフラグメントを含んだ独立したファイルを言います。 外部構成ファイルは、メインの構成ファイルによって参照されます。 **connectionStrings** セクションを物理的に分かれたファイルに保存できるため、アプリケーションの配置後に接続文字列を編集する場合に有効な手段です。 たとえば、構成ファイルに修正が加えられた場合、ASP.NET の標準的な動作ではアプリケーション ドメインが再起動され、その結果、状態情報が失われてしまいます。 しかし、外部構成ファイルに対する修正であればアプリケーションの再起動は伴いません。 外部構成ファイルは ASP.NET だけでなく、Windows アプリケーションでも使用できます。 また、ファイルのアクセス セキュリティや権限を使用して、外部構成ファイルへのアクセスを制限することもできます。 実行時における外部構成ファイルの使用は透過的であり、特殊なコーディングも不要です。  
  
 外部構成ファイルに接続文字列を保存するには、**connectionStrings** セクションだけを含んだファイルを別途作成します。 それ以外の要素、セクション、または属性は含めないでください。 外部構成ファイルの構文の例を次に示します。  
  
```xml  
<connectionStrings>  
  <add name="Name"
   providerName="System.Data.ProviderName"
   connectionString="Valid Connection String;" />  
</connectionStrings>  
```  
  
 外部ファイルの完全修飾名および場所は、メインのアプリケーション構成ファイルの **configSource** 属性で指定します。 この例では、`connections.config` という名前の外部構成ファイルを参照しています。  
  
```xml  
<?xml version='1.0' encoding='utf-8'?>  
<configuration>  
    <connectionStrings configSource="connections.config"/>  
</configuration>  
```  
  
## <a name="retrieving-connection-strings-at-run-time"></a>接続文字列の実行時の取得  
 .NET Framework 2.0 では、<xref:System.Configuration> 名前空間に新しいクラスが導入され、実行時に簡単に構成ファイルから接続文字列を取得できるようになりました。 プログラムから名前またはプロバイダー名を使用して接続文字列を取得できます。  
  
> [!NOTE]
> **connectionStrings** セクションは、**machine.config** ファイルにも存在します。このセクションには、Visual Studio によって使用される接続文字列が格納されます。 Windows アプリケーションの **app.config** ファイルからプロバイダー名で接続文字列を取得した場合、まず **machine.config** 内の接続文字列が読み込まれ、その後、**app.config** のエントリが読み込まれます。**connectionStrings** 要素の直後に **clear** を追加すると、継承されたすべての参照がメモリ内のデータ構造から削除され、ローカルの **app.config** ファイルに定義されている接続文字列だけが考慮されます。  
  
### <a name="working-with-the-configuration-classes"></a>構成クラスの使用  
 .NET Framework 2.0 以降では、ローカル コンピューター上の構成ファイルで作業するときに、非推奨とされた <xref:System.Configuration.ConfigurationManager> に代わって <xref:System.Configuration.ConfigurationSettings> を使用します。 ASP.NET 構成ファイルでの作業では、<xref:System.Web.Configuration.WebConfigurationManager> を使用します。 Web サーバー上の構成ファイルを扱うことを目的に設計され、**system.web** など、構成ファイルのセクションにプログラムからアクセスできます。  
  
> [!NOTE]
> 実行時に構成ファイルにアクセスするには、呼び出し元に権限を付与する必要があります。必要な権限は、アプリケーションの種類、構成ファイル、格納場所などによって異なります。 詳細については、「[構成クラスの使用](https://docs.microsoft.com/previous-versions/aspnet/ms228063(v=vs.100))」、および ASP.NET アプリケーションには、「<xref:System.Web.Configuration.WebConfigurationManager>」および Windows アプリケーションには、「<xref:System.Configuration.ConfigurationManager>」を参照してください。  
  
 <xref:System.Configuration.ConnectionStringSettingsCollection> を使用すると、アプリケーション構成ファイルから接続文字列を取得できます。 このコレクションには、それぞれが **connectionStrings** セクションの単一のエントリを表す一連の <xref:System.Configuration.ConnectionStringSettings> オブジェクトが格納されます。 個々のプロパティは接続文字列の属性にマップされており、名前またはプロバイダー名を指定することによって接続文字列を取得できます。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:System.Configuration.ConnectionStringSettings.Name%2A>|接続文字列の名前。 **name** 属性にマップされています。|  
|<xref:System.Configuration.ConnectionStringSettings.ProviderName%2A>|プロバイダーの完全修飾名。 **providerName** 属性にマップされています。|  
|<xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A>|接続文字列。 **connectionString** 属性にマップされています。|  
  
### <a name="example-listing-all-connection-strings"></a>例:すべての接続文字列を一覧表示する  
 この例では、<xref:System.Configuration.ConnectionStringSettingsCollection> を反復処理しながら、<xref:System.Configuration.ConnectionStringSettings.Name%2A?displayProperty=nameWithType>、<xref:System.Configuration.ConnectionStringSettings.ProviderName%2A?displayProperty=nameWithType>、<xref:System.Configuration.ConnectionStringSettings.ConnectionString%2A?displayProperty=nameWithType> の各プロパティをコンソール ウィンドウに表示します。  
  
> [!NOTE]
> プロジェクトの種類によっては System.Configuration.dll がインクルードされていない場合があります。構成クラスを使用する場合は、必要に応じて参照設定するようにしてください。 特定のアプリケーションの構成ファイルの名前と場所は、アプリケーションの種類やホストしているプロセスによって異なります。  
  
 [!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfig#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfig/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringSettings.RetrieveFromConfig#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfig/VB/source.vb#1)]  
  
### <a name="example-retrieving-a-connection-string-by-name"></a>例:接続文字列を名前で取得する  
 次の例では、接続文字列の名前を指定することによって、接続文字列を構成ファイルから取得する方法を説明します。 このコードでは、指定された入力パラメーターと <xref:System.Configuration.ConnectionStringSettings> の名前とを照合することによって、<xref:System.Configuration.ConfigurationManager.ConnectionStrings%2A> オブジェクトを作成します。 一致する名前が見つからなかった場合は `null` (Visual Basic の場合は `Nothing`) が返されます。  
  
 [!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfigByName#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByName/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringSettings.RetrieveFromConfigByName#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByName/VB/source.vb#1)]  
  
### <a name="example-retrieving-a-connection-string-by-provider-name"></a>例:プロバイダー名による接続文字列の取得  
 次の例では、プロバイダーの不変名を *System.Data.ProviderName* の形式で指定することによって接続文字列を取得する方法を説明します。 このコードでは、<xref:System.Configuration.ConnectionStringSettingsCollection> を反復処理し、最初に見つかった <xref:System.Configuration.ConnectionStringSettings.ProviderName%2A> の接続文字列を返します。 プロバイダー名が見つからなかった場合は `null` (Visual Basic の場合は `Nothing`) が返されます。  
  
 [!code-csharp[DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringSettings.RetrieveFromConfigByProvider/VB/source.vb#1)]  
  
## <a name="encrypting-configuration-file-sections-using-protected-configuration"></a>保護構成を使った構成ファイル セクションの暗号化  
 ASP.NET 2.0 では、*保護構成*と呼ばれる、構成ファイルの機密情報を暗号化するための新しい機能が導入されました。 保護構成は、主に ASP.NET を想定して設計されたものですが、Windows アプリケーションの構成ファイル セクションを暗号化する目的でも使用できます。 保護構成機能の詳細については、「[保護された構成を使用した構成情報の暗号化](https://docs.microsoft.com/previous-versions/aspnet/53tyfkaw(v=vs.100))」を参照してください。  
  
 次の構成ファイル フラグメントは、暗号化後の **connectionStrings** セクションを示しています。 **configProtectionProvider** には、接続文字列の暗号化と復号化に使用される、保護構成プロバイダーが指定されています。 **EncryptedData** セクションには暗号文が格納されています。  
  
```xml  
<connectionStrings configProtectionProvider="DataProtectionConfigurationProvider">  
  <EncryptedData>  
    <CipherData>  
      <CipherValue>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAH2... </CipherValue>  
    </CipherData>  
  </EncryptedData>  
</connectionStrings>  
```  
  
 暗号化された接続文字列は実行時に取得されることになります。このとき、.NET Framework は、指定されたプロバイダーを使用して **CipherValue** を復号化し、アプリケーションに利用可能な接続文字列を提供します。 復号化のプロセスを管理するためのコードを自分で作成する必要はありません。  
  
### <a name="protected-configuration-providers"></a>保護構成プロバイダー  
 保護構成プロバイダーは、ローカル コンピューターの **machine.config** ファイルの **configProtectedData** セクションに登録されます。次のフラグメントを見ると、.NET Framework が備えている 2 つの保護構成プロバイダーが指定されていることがわかります。 ここでは、読みやすくするために一部の値を省略しています。  
  
```xml  
<configProtectedData defaultProvider="RsaProtectedConfigurationProvider">  
  <providers>  
    <add name="RsaProtectedConfigurationProvider"
      type="System.Configuration.RsaProtectedConfigurationProvider" />  
    <add name="DataProtectionConfigurationProvider"
      type="System.Configuration.DpapiProtectedConfigurationProvider" />  
  </providers>  
</configProtectedData>  
```  
  
 別の保護構成プロバイダーが必要な場合は、それを **machine.config** ファイルに追加することによって構成できます。 また、<xref:System.Configuration.ProtectedConfigurationProvider> 抽象基本クラスを継承することで、保護構成プロバイダーを独自に作成することもできます。 次の表は、.NET Framework に含まれている 2 つの構成プロバイダーを示しています。  
  
|プロバイダー|説明|  
|--------------|-----------------|  
|<xref:System.Configuration.RsaProtectedConfigurationProvider>|データの暗号化と復号化には、RSA 暗号化アルゴリズムが使用されます。 RSA アルゴリズムは、公開キー暗号化だけでなく、デジタル署名にも使用されます。 "公開キー" として知られているほか、2 つの異なるキーが使用されることから非対称暗号化と呼ばれる場合もあります。 [ASP.NET IIS 登録ツール (Aspnet_regiis.exe)](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/k6h9cz8h(v=vs.90)) を使用すると、Web.config ファイルのセクションを暗号化したり、暗号化キーを管理したりすることができます。 構成ファイルは、その処理時に ASP.NET によって復号化されます。 ASP.NET アプリケーションの ID には、セクションの暗号化と復号化に使用される暗号化キーへの読み取りアクセスが必要です。|  
|<xref:System.Configuration.DpapiProtectedConfigurationProvider>|構成セクションの暗号化に Windows Data Protection API (DPAPI) が使用されます。 この API には、Windows の組み込み暗号化サービスが使用され、コンピューター単位またはユーザー アカウント単位の保護を構成できます。 コンピューター単位の保護は、同じサーバー上の複数のアプリケーションで情報を共有する必要がある場合に使用します。 共有ホスティング環境など、特定のユーザー ID で実行されるサービスには、ユーザー アカウント単位の保護を使用できます。 各アプリケーションは、ファイルやデータベースなど、各種リソースへのアクセスが制限された別々の ID で実行されます。|  
  
 どちらのプロバイダーも、強力なデータ暗号化機能を備えています。 ただし、Web ファームなど、複数のサーバーで、同じ構成ファイルを暗号化して使用する場合、データの暗号化に使用される暗号化キーをエクスポートしたり、それを別のサーバーにインポートしたりできるのは、<xref:System.Configuration.RsaProtectedConfigurationProvider> だけです。 詳細については、「[保護された構成 RSA キー コンテナのインポートとエクスポート](https://docs.microsoft.com/previous-versions/aspnet/yxw286t2(v=vs.100))」を参照してください。  
  
### <a name="using-the-configuration-classes"></a>構成クラスの使用  
 <xref:System.Configuration> 名前空間には、構成設定をプログラムから行うためのクラスが存在します。 <xref:System.Configuration.ConfigurationManager> クラスは、コンピューター、アプリケーション、ユーザーの各構成ファイルへのアクセスを提供します。 ASP.NET アプリケーションを作成している場合は、同じ機能を持った <xref:System.Web.Configuration.WebConfigurationManager> クラスを使用します。他にも **\<system.web>** の設定など、ASP.NET アプリケーション固有の設定にもアクセスできます。  
  
> [!NOTE]
> <xref:System.Security.Cryptography> 名前空間には、データの暗号化と復号化に関連した補足的なオプションを提供するクラスが存在します。 これらのクラスは、保護構成では利用できない暗号化サービスが必要な場合に使用します。 これらのクラスは必ずしも純粋なマネージド実装とは限らず、アンマネージド Microsoft CryptoAPI 用のラッパーもあります。 詳細については、「[暗号サービス](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/93bskf9z(v=vs.90))」をご覧ください。  
  
### <a name="appconfig-example"></a>App.config の例  
 ここでは、Windows アプリケーションの **app.config** ファイルにある **connectionStrings** セクションを条件に応じて暗号化したり復号化したりする方法を紹介します。 この例に示したプロシージャは、MyApplication.exe など、アプリケーションの名前を引数として受け取ります。 その後、**app.config** ファイルを暗号化して、その実行可能ファイルと同じフォルダーに MyApplication.exe.config という名前でコピーします。  
  
> [!NOTE]
> 接続文字列は暗号化したときと同じコンピューターでしか復号化できません。  
  
 このコードは、<xref:System.Configuration.ConfigurationManager.OpenExeConfiguration%2A> メソッドを使用して **app.config** ファイルを編集モードで開き、<xref:System.Configuration.ConfigurationManager.GetSection%2A> メソッドを使用して **connectionStrings** セクションを返します。 さらに、<xref:System.Configuration.SectionInformation.IsProtected%2A> プロパティをチェックし、セクションがまだ暗号化されていなければ、<xref:System.Configuration.SectionInformation.ProtectSection%2A> を呼び出して暗号化します。 それ以外の場合は、<xref:System.Configuration.SectionInformation.UnprotectSection%2A> メソッドを呼び出してセクションを復号化します。 最後に、<xref:System.Configuration.Configuration.Save%2A> メソッドで操作を完了し、変更内容を保存します。  
  
> [!NOTE]
> このコードを実行するには、プロジェクトで `System.Configuration.dll` を参照設定する必要があります。  
  
 [!code-csharp[DataWorks ConnectionStrings.Encrypt#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStrings.Encrypt/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStrings.Encrypt#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStrings.Encrypt/VB/source.vb#1)]  
  
### <a name="webconfig-example"></a>Web.config の例  
 この例では、<xref:System.Web.Configuration.WebConfigurationManager.OpenWebConfiguration%2A> の `WebConfigurationManager` メソッドを使用しています。 この場合、チルダを使用して、**Web.config** ファイルの相対パスを指定できる点に注目してください。 このコードを実行するには、`System.Web.Configuration` クラスへの参照が必要です。  
  
 [!code-csharp[DataWorks ConnectionStringsWeb.Encrypt#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks ConnectionStringsWeb.Encrypt/CS/source.cs#1)]
 [!code-vb[DataWorks ConnectionStringsWeb.Encrypt#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks ConnectionStringsWeb.Encrypt/VB/source.vb#1)]  
  
 ASP.NET アプリケーションのセキュリティ保護について詳しくは、「[ASP.NET Web サイトのセキュリティ保護](https://docs.microsoft.com/previous-versions/aspnet/91f66yxt(v=vs.100))」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [接続文字列ビルダー](connection-string-builders.md)
- [接続情報の保護](protecting-connection-information.md)
- [構成クラスの使用](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ms228063(v=vs.90))
- [アプリの構成](../../configure-apps/index.md)
- [ASP.NET Web サイト管理](https://docs.microsoft.com/previous-versions/aspnet/6hy1xzbw(v=vs.100))
- [ADO.NET の概要](ado-net-overview.md)
