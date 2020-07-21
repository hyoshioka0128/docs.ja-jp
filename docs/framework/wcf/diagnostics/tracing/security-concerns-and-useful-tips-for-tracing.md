---
title: トレースに関するセキュリティの考慮事項と役立つヒント
ms.date: 03/30/2017
ms.assetid: 88bc2880-ecb9-47cd-9816-39016a07076f
ms.openlocfilehash: 0a09e387a4f964441f11d07a84bd492345d5b691
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84578878"
---
# <a name="security-concerns-and-useful-tips-for-tracing"></a>トレースに関するセキュリティの考慮事項と役立つヒント
ここでは、機密情報を漏洩の危険から守る方法と共に、WebHost を使用する場合の便利なヒントについて説明します。  
  
## <a name="using-a-custom-trace-listener-with-webhost"></a>WebHost でのカスタム トレース リスナーの使用  
 独自のリスナーを作成している場合、WebHost サービスではトレースが失われる可能性があることを認識する必要があります。 WebHost をリサイクルすると、実行中のプロセスがシャットダウンされ、複製されたプロセスに引き継がれます。 この 2 つのプロセスは、しばらくの間、引き続き同じリソースにアクセスできる必要がありますが、これはリスナーの種類に依存します。 この場合、`XmlWriterTraceListener` は、2 番目のプロセスに対して新しいトレース ファイルを作成します。一方、Windows のイベント トレースは、同じセッションの複数のプロセスを管理して、同じファイルへのアクセス権を付与します。 したがって、独自に作成したリスナーが同様の機能を提供しない場合、この 2 つのプロセスによってファイルがロックされたときにトレースが失われる可能性があります。  
  
 カスタム トレース リスナーがネットワーク上で (たとえば、リモート データベースに) トレースとメッセージを送信する場合があることを認識する必要もあります。 アプリケーションを展開するユーザーは、適切なアクセス制御を提供するカスタム リスナーを構成する必要があります。 また、遠隔地で公開される可能性があるすべての個人情報にセキュリティ制御を適用する必要もあります。  
  
## <a name="logging-sensitive-information"></a>機密情報のログ記録  
 スコープ内のメッセージに含まれるメッセージ ヘッダーをトレースします。 トレースが有効になっていると、アプリケーション固有のヘッダー内にある個人情報 (クエリ文字列など)、および本文情報 (クレジット カード番号など) をログで確認できるようになります。 アプリケーションを展開するユーザーは、構成ファイルとトレース ファイルに対するアクセス制御を実施する必要があります。 この種の情報を表示しないようにするには、トレースを無効にします。トレース ログを共有する場合は、表示しないデータをフィルターで除外します。  
  
 トレース ファイルの内容が意図せず公開されることを防ぐために、次のヒントに従ってください。  
  
- WebHost および自己ホストの両方のシナリオにおいて、ログ ファイルがアクセス制御リスト (ACL) によって保護されていることを確認します。  
  
- Web 要求を使用して簡単に処理できないファイル拡張子を選択します。 たとえば、.xml ファイルの拡張子を選ぶのは安全ではありません。 IIS の管理ガイドを参照して、処理できる拡張子のリストを確認します。  
  
- ログ ファイルのある場所への絶対パスを指定します。この場所は、部外者が Web ブラウザーを使用してアクセスできないように、WebHost の vroot パブリック ディレクトリの外にします。  
  
 既定では、キーおよびユーザー名やパスワードなどの個人を特定できる情報 (PII) は、トレースおよびログに記録するメッセージではありません。 しかし、コンピューターの管理者は、Machine.config ファイルの `enableLoggingKnownPII` 要素にある `machineSettings` 属性を使用して、コンピューター上で実行されているアプリケーションに対し、既知の PII (個人を特定できる情報) のログ記録を許可できます。次のコード例を参照してください。  
  
```xml  
<configuration>  
   <system.ServiceModel>  
      <machineSettings enableLoggingKnownPii="Boolean"/>  
   </system.ServiceModel>  
</configuration>
```  
  
 アプリケーションを配置するユーザーが App.config ファイルか Web.config ファイルのいずれかで `logKnownPii` 属性を使用することで 、PII ログを可能にする方法を次に示します。  
  
```xml  
<system.diagnostics>  
  <sources>  
      <source name="System.ServiceModel.MessageLogging"  
        logKnownPii="true">  
        <listeners>  
                 <add name="messages"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="c:\logs\messages.svclog" />  
          </listeners>  
      </source>  
  </sources>  
</system.diagnostics>  
```  
  
 両方の設定が `true` の場合にのみ、PII はログに記録されます。 2 種類のスイッチを組み合わせることで、各アプリケーションで既知の PII のログを柔軟に記録できるようになります。  
  
 構成ファイルで 2 種類以上のカスタム ソースを指定しても、最初のソースの属性のみが読み込まれることに注意してください。 他の属性は無視されます。 つまり、2 番目以降の App.config ファイルでは、PII はいずれのソースでもログに記録されなくなります。これは 2 番目のソースで PII のログ記録を明示的に有効にした場合でも同様です。  
  
```xml  
<system.diagnostics>  
  <sources>  
      <source name="System.ServiceModel.MessageLogging"  
        logKnownPii="false">  
        <listeners>  
           <add name="messages"  
                type="System.Diagnostics.XmlWriterTraceListener"  
                initializeData="c:\logs\messages.svclog" />  
          </listeners>  
      </source>  
      <source name="System.ServiceModel"
         logKnownPii="true">  
         <listeners>  
            <add name="xml" />  
         </listeners>  
      </source>  
  </sources>  
</system.diagnostics>  
```  
  
 `<machineSettings enableLoggingKnownPii="Boolean"/>` の要素が Machine.config ファイルに含まれていない場合、システムは <xref:System.Configuration.ConfigurationErrorsException> をスローします。  
  
 変更点はアプリケーションが開始されるか、再起動されるまで、反映されません。 両方の属性も `true` に設定されている場合は、イベントは開始時にログに記録されます。 また、`logKnownPii` が `true` に設定され、`enableLoggingKnownPii` が `false` に設定されている場合にも、イベントはログに記録されます。  
  
 PII のログ記録の詳細については、「 [Pii Security Lockdown](../../samples/pii-security-lockdown.md) sample」を参照してください。  
  
 コンピューターの管理者およびアプリケーションを配置するユーザーは、これらの 2 種類のスイッチを使用する場合に注意する必要があります。 PII のログ記録が有効になっている場合は、セキュリティ キーと PII がログに記録されます。 ログ記録を無効にしても、機密情報およびアプリケーション固有のデータは、依然としてメッセージのヘッダーと本体に記録されています。 プライバシーの詳細および PII の公開を防止する方法については、「[ユーザーのプライバシー](https://docs.microsoft.com/previous-versions/dotnet/articles/aa480490(v=msdn.10))」を参照してください。  
  
 また、接続が確立されるたび (接続指向トランスポートの場合)、またはメッセージが送信されるたび (それ以外の場合) に、メッセージ送信者の IP アドレスが記録されます。 これは、送信者の同意を得ずに行われます。 ただし、このログ記録は Information レベルまたは Verbose レベルだけで実行されます。これらのトレース レベルは既定ではありません。また、ライブ デバッグを行う場合を除き、運用環境ではお勧めしません。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
