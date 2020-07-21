---
title: SendMail カスタム アクティビティ
ms.date: 03/30/2017
ms.assetid: 947a9ae6-379c-43a3-9cd5-87f573a5739f
ms.openlocfilehash: e7cc64e68c3d78b9ee7ec813700e96a52c239141
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182783"
---
# <a name="sendmail-custom-activity"></a>SendMail カスタム アクティビティ
このサンプルでは、<xref:System.Activities.AsyncCodeActivity> から派生するカスタム アクティビティを作成して、SMTP を使用して電子メールを送信し、ワークフロー アプリケーション内で使用する方法を示します。 カスタム アクティビティでは、電子メール<xref:System.Net.Mail.SmtpClient>を非同期的に送信し、認証を使用してメールを送信する機能を使用します。 また、テスト モード、トークン置換、ファイル テンプレート、テスト ドロップ パスなどのエンドユーザーの機能も提供しています。  
  
 次の表で、`SendMail` アクティビティの引数の詳細を説明します。  
  
|名前|Type|説明|  
|-|-|-|  
|Host|String|SMTP サーバー ホストのアドレス。|  
|Port|String|ホストの SMTP サービスのポート。|  
|EnableSsl|[bool]|<xref:System.Net.Mail.SmtpClient> が、接続を暗号化するために SSL (Secure Sockets Layer) を使用するかどうかを指定します。|  
|UserName|String|差出人の <xref:System.Net.Mail.SmtpClient.Credentials%2A> プロパティを認証する資格情報を設定するユーザー名。|  
|Password|String|差出人の <xref:System.Net.Mail.SmtpClient.Credentials%2A> プロパティを認証する資格情報を設定するパスワード。|  
|サブジェクト|<xref:System.Activities.InArgument%601>\<文字列>|メッセージの件名。|  
|Body|<xref:System.Activities.InArgument%601>\<文字列>|メッセージの本文。|  
|[Attachments]|<xref:System.Activities.InArgument%601>\<文字列>|この電子メール メッセージに添付されたデータを格納するために使用される添付ファイルのコレクション。|  
|ソース|<xref:System.Net.Mail.MailAddress>|この電子メール メッセージの差出人アドレスです。|  
|ターゲット|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>>|この電子メール メッセージの受信者を含むアドレス のコレクション。|  
|CC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>>|この電子メール メッセージのカーボン コピー (CC) 受信者を含むアドレス コレクション。|  
|BCC|<xref:System.Activities.InArgument%601>\<<xref:System.Net.Mail.MailAddressCollection>>|この電子メール メッセージの BCC (ブラインド カーボン コピー) 受信者を含むアドレス コレクション。|  
|トークン|<xref:System.Activities.InArgument%601><ディクショナリ\<文字列、文字列>>|本文で置換するトークン。 この機能を使用すると、本文にいくつかの値を指定した後、このプロパティを使用して提供されるトークンで置換できます。|  
|BodyTemplateFilePath|String|本文のテンプレートのパス。 `SendMail` アクティビティは、このファイルの内容をその body プロパティにコピーします。<br /><br /> テンプレートは、tokens プロパティの内容によって置き換えられるトークンを含めることができます。|  
|TestMailTo|<xref:System.Net.Mail.MailAddress>|このプロパティを設定すると、すべての電子メールが指定されたアドレスに送信されます。<br /><br /> このプロパティは、ワークフローをテストするときに使用するためのものです。 たとえば、すべてのメールが実際の受信者に送信されずに送信されるようにする場合などです。|  
|TestDropPath|String|このプロパティを設定すると、すべての電子メールも指定したファイルに保存されます。<br /><br /> このプロパティは、ワークフローをテストまたはデバッグするときに使用され、送信電子メールの形式と内容が適切であることを確認するためのものです。|  
  
## <a name="solution-contents"></a>ソリューションのコンテンツ  
 ソリューションには、次の 2 つのプロジェクトが含まれています。  
  
|Project|説明|重要なファイル|  
|-------------|-----------------|---------------------|  
|SendMail|SendMail アクティビティ|1. SendMail.cs: 主な活動の実施<br />2. 送信メールデザイナ.xaml とSendMailDesigner.xaml.cs: 送信メール アクティビティのデザイナー<br />3. メールテンプレートボディ.htm: 電子メールを送信するためのテンプレート。|  
|SendMailTestClient|SendMail アクティビティをテストするクライアント。  このプロジェクトでは、SendMail アクティビティを宣言的に起動する方法とプログラムで起動する方法を示します。|1. Sequence1.xaml: SendMail アクティビティを呼び出すワークフロー。<br />2. Program.cs: Sequence1 を呼び出し、SendMail を使用するワークフローをプログラムで作成します。|  
  
## <a name="further-configuration-of-the-sendmail-activity"></a>SendMail アクティビティの追加構成  
 サンプルには表示されませんが、SendMail アクティビティの追加構成を実行できます。 次の 3 つのセクションは、その方法を示しています。  
  
### <a name="sending-an-email-using-tokens-specified-in-the-body"></a>本文で指定されたトークンを使用した電子メールの送信  
 次のコード スニペットでは、本文のトークンを使用して電子メールを送信する方法を示します。 トークンが body プロパティに指定されていることに注目してください。 それらのトークンの値は、tokens プロパティに指定されています。  
  
```csharp  
IDictionary<string, string> tokens = new Dictionary<string, string>();  
tokens.Add("@name", "John Doe");  
tokens.Add("@date", DateTime.Now.ToString());  
tokens.Add("@server", "localhost");  
  
new SendMail  
{  
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Body = "Hello @name. This is a test email sent from @server. Current date is @date",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens)  
};  
```  
  
### <a name="sending-an-email-using-a-template"></a>テンプレートを使用した電子メールの送信  
 次のスニペットでは、本文のテンプレート トークンを使用して電子メールを送信する方法を示します。 `BodyTemplateFilePath` プロパティを設定するときに、Body プロパティの値を指定する必要がないことに注目してください (テンプレート ファイルのコンテンツは本文にコピーされます)。  
  
```csharp  
new SendMail  
{
    From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
    To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
    Subject = "Test email",  
    Host = "localhost",  
    Port = 25,  
    Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
    BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",
};  
```  
  
### <a name="sending-mails-in-testing-mode"></a>テスト モードでの電子メールの送信  
 このコード スニペットは、2 つのテスト プロパティを設定`TestMailTo`する方法を示します:`john.doe@contoso.con`すべてのメッセージを (To、Cc、BCC の値に関係なく) 送信します。 TestDropPath を設定すると、送信するすべての電子メールは、指定したパスにも記録されます。 これらのプロパティは、個別に設定できます (関連していません)。  
  
```csharp  
new SendMail  
{
   From = new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   To = new LambdaValue<MailAddressCollection>(  
                    ctx => new MailAddressCollection() { new MailAddress("someone@microsoft.com") }),  
   Subject = "Test email",  
   Host = "localhost",  
   Port = 25,  
   Tokens = new LambdaValue<IDictionary<string, string>>(ctx => tokens),  
   BodyTemplateFilePath = @"..\..\..\SendMail\Templates\MailTemplateBody.htm",  
   TestMailTo= new LambdaValue<MailAddress>(ctx => new MailAddress("john.doe@contoso.com")),  
   TestDropPath = @"c:\Samples\SendMail\TestDropPath\",  
};  
```  
  
## <a name="set-up-instructions"></a>セットアップ手順  
 このサンプルでは SMTP サーバーにアクセスする必要があります。  
  
 SMTP サーバーのセットアップの詳細については、次のリンクを参照してください。  
  
- [SMTP サービス (IIS 6.0) の構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784968(v=ws.10))  
  
- [IIS 7.0: SMTP 電子メールの構成](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772058(v=ws.10))  
  
- [SMTP サービスをインストールする方法](https://docs.microsoft.com/previous-versions/tn-archive/aa997480(v=exchg.65))  
  
 ダウンロードには、サードパーティで提供されている SMTP エミュレーターを使用できます。  
  
##### <a name="to-run-this-sample"></a>このサンプルを実行するには  
  
1. Visual Studio 2010 を使用して、SendMail.sln ソリューション ファイルを開きます。  
  
2. 有効な SMTP サーバーへのアクセス権があることを確認してください。 セットアップ手順を参照してください。  
  
3. サーバーのアドレスと差出人と宛先の電子メール アドレスを使用してプログラムを構成します。  
  
     このサンプルを正しく実行するには、Program.csおよび Sequence.xaml で、差出人と宛先の電子メール アドレスと SMTP サーバーのアドレスの値を構成する必要があります。 プログラムでは電子メールが 2 つの方法で送信されるため、両方の場所でアドレスを変更する必要があります。  
  
4. ソリューションをビルドするには、Ctrl キーと Shift キーを押しながら B キーを押します。  
  
5. ソリューションを実行するには、Ctrl キーを押しながら F5 キーを押します。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\SendMail`
