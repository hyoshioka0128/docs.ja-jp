---
title: 'トラブルシューティング: Windows コミュニケーション ファウンデーションのチュートリアルを使用する'
ms.date: 01/25/2019
ms.assetid: 69a21511-0871-4c41-9a53-93110e84d7fd
ms.openlocfilehash: 73aa0f5784784cb788a7532f8e22cbe925429c41
ms.sourcegitcommit: 99b153b93bf94d0fecf7c7bcecb58ac424dfa47c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "80249618"
---
# <a name="troubleshoot-the-get-started-with-windows-communication-foundation-tutorials"></a>トラブルシューティング: Windows コミュニケーション ファウンデーションのチュートリアルを使用する

この記事では、「[チュートリアル: Windows コミュニケーション ファウンデー](getting-started-tutorial.md)ション アプリケーションの概要」の手順に従って直面する可能性のある、最も一般的な問題とエラーに対する解決策を提供します。
  
## <a name="common-problems"></a>一般的な問題

**ハード ドライブにプロジェクト ファイルが見つかりません。**

 プロジェクト ファイルは *、C:\ユーザー\\&lt;ユーザー名&gt;\ソース\リポジトリ*に保存されます。  

***Svcutil.exe*によって生成された*App.config*ファイルが見つかりません。**

 Visual Studio では、[**既存項目の追加]** ウィンドウには、既定で次の拡張子を持つファイルのみが表示されます。

- *.cs*
- *.resx*
- *設定*
- *.xsd*
- *.wsdl*

すべてのファイルの種類を表示するには、[**既存項目の追加**] ウィンドウの右下隅にあるドロップダウン リストで [すべてのファイル ( **\*.)\*] を**選択します。  
  
## <a name="common-errors"></a>一般的なエラー

### <a name="compile-the-service-application"></a>サービス アプリケーションをコンパイルする

**エラー BC30420 'サブメイン' が 'GettingStartedHost.Module1' に見つかりませんでした。**

エントリ ポイントが Visual Basic アプリケーションに対して正しくありません。 次の変更を行います。

   1. **[ソリューション エクスプローラー** ] ウィンドウで **、"GettingStartedHost"** フォルダーを選択し、ショートカット メニューの **[プロパティ]** をクリックします。
    a. [**開始開始]** ウィンドウの **[スタートアップ オブジェクト**] で **、[Service.Program]** (または特定のアプリケーションのエントリ ポイント) を一覧から選択します。
    b. メイン メニューの [**ファイルをすべて** > **保存]** を選択します。

### <a name="run-the-service-application"></a>サービス アプリケーションを実行する

**HTTP は URL 'http:\//+:8000/開始/電卓サービス' を登録できませんでした。プロセスにこの名前空間へのアクセス権がありません。**

 適切なアクセスを行う場合は、管理特権を使用して、Windows 通信基盤 (WCF) サービスをホストするプロセスを開始します。

- Visual Studio の場合: **[スタート]** メニューで Visual Studio プログラムを選択し、ショートカット メニューから **[** > **管理者として**実行する] を選択します。
- コンソール ウィンドウの場合 **:[スタート]** メニューの **[コマンド プロンプト**] を選択し、ショートカット メニューの **[その他** > の**実行管理者**] を選択します。
- エクスプローラの場合: 実行可能ファイルを選択し、ショートカット メニューの **[管理者として実行**] を選択します。

### <a name="compile-the-client-application"></a>クライアント アプリケーションをコンパイルする

**'電卓クライアント' ' メソッド名>\<の定義が含まれておらず、拡張\<メソッド 'メソッド名>' 型 '電卓クライアント' の最初の引数を受け入れるメソッド 'メソッド名' が見つかりませんでした (using ディレクティブまたはアセンブリ参照が見つかりません)。**  

`ServiceOperationAttribute`属性でマークしたメソッドのみが公開されます。 インターフェイスのメソッドから`ServiceOperationAttribute`属性を省略すると、コンパイル中にこのエラー メッセージが表示されます。 `ICalculator`  

**型または名前空間名 '電卓クライアント' が見つかりませんでした (using ディレクティブまたはアセンブリ参照が見つかりません)。**

 *Svcutil.exe*ツールを使用して生成したときに *、クライアント*プロジェクトにgeneratedProxy.cs (または*生成された Proxy.vb)* ファイルを追加しなかった場合、このエラーが表示されます。  

### <a name="run-the-client-application"></a>クライアント アプリケーションを実行する

**処理されていない例外: システム.サービスモデル.エンドポイントNotFound例外: 'http:\//localhost:8000/開始/電卓サービス' に接続できませんでした。TCP エラー コード 10061: ターゲット マシンがアクティブに拒否したため、接続できませんでした。**

このエラーは、サービスを最初に開始せずにクライアント アプリケーションを実行した場合に発生します。 まず、ホスト アプリケーションを実行してサービスを開始し、クライアント アプリケーションを実行します。

### <a name="use-the-svcutilexe-tool"></a>ツールを使用する

**'Svcutil' は、内部または外部コマンド、操作可能なプログラム、またはバッチ ファイルとして認識されません。**

 *Svcutil.exe は*システム パスに含まれる必要があります。 最も簡単な解決策は、Visual Studio コマンド プロンプトを使用することです。 [**スタート]** メニューから**Visual \<Studio バージョン>** ディレクトリを選択し **、[VS\<バージョン>の開発者コマンド プロンプト**] を選択します。 このコマンド プロンプトでは、Visual Studio の一部として出荷されるすべてのツールの正しい場所にシステム パスを設定します。  
  
### <a name="run-the-service-and-client-applications"></a>サービスアプリケーションとクライアントアプリケーションを実行する

**ターゲット 'http: /localhost:8000/\/開始/電卓サービス'\/の SOAP セキュリティ ネゴシエーションが失敗しました。**  

このエラーは、ネットワークに接続していないドメインに参加しているコンピューターで発生します。 コンピュータをネットワークに接続するか、サービスとクライアントの両方のセキュリティをオフにします。

セキュリティをオフにするには:

- サービスの場合は、 を`WSHttpBinding`作成するコードを次のコードに置き換えます。  
  
    ```csharp
    // Step 3: Add a service endpoint.
    selfhost.AddServiceEndpoint(typeof(ICalculator), new WSHttpBinding(SecurityMode.None), "CalculatorService");  
    ```

- クライアントの場合、構成ファイルで、**\<バインディング>** 要素の下の**\<セキュリティ>** 要素を次のように更新します。  
  
    ```xml
    <binding name="WSHttpBinding_ICalculator">
      <security mode="None" />
    </binding
    ```  

## <a name="see-also"></a>関連項目  
 [WCF アプリケーションの概要](getting-started-tutorial.md)  
 [WCF トラブルシューティングのクイック スタート](wcf-troubleshooting-quickstart.md)  
 [セットアップの問題のトラブルシューティング](troubleshooting-setup-issues.md)
