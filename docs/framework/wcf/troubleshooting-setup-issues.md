---
title: セットアップに関する問題のトラブルシューティング
ms.date: 03/30/2017
ms.assetid: 1644f885-c408-4d5f-a5c7-a1a907bc8acd
ms.openlocfilehash: 2cd9ced4f0780b1a6f63e4a5833e20ac91870121
ms.sourcegitcommit: 43cbde34970f5f38f30c43cd63b9c7e2e83717ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81121578"
---
# <a name="troubleshoot-setup-issues"></a>セットアップの問題のトラブルシューティング

この資料では、Windows 通信基盤 (WCF) のセットアップの問題のトラブルシューティング方法について説明します。  
  
## <a name="some-windows-communication-foundation-registry-keys-are-not-repaired-by-performing-an-msi-repair-operation-on-the-net-framework-30"></a>.NET Framework 3.0 の MSI 修復操作の実行では修復されない一部の Windows Communication Foundation レジストリ キー  
 次のいずれかのレジストリ キーを削除した場合  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceModelService 3.0.0.0  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceModelOperation 3.0.0.0  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceModelEndpoint 3.0.0.0  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\SMSvcHost 3.0.0.0  
  
- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSDTC Bridge 3.0.0.0  
  
 **コントロール パネル**の **[プログラムの追加と削除**] アプレットから起動した .NET Framework 3.0 インストーラーを使用して修復を実行した場合、キーは再作成されません。 これらのキーを正しく再作成するには、.NET Framework 3.0 をアンインストール後、再インストールする必要があります。  
  
## <a name="wmi-service-corruption-blocks-installation-of-the-windows-communication-foundation-wmi-provider-during-installation-of-net-framework-30-package"></a>WMI サービスの破損により .NET Framework 3.0 パッケージのインストール中に Windows Communication Foundation WMI プロバイダーのインストールがブロックされる  
 WMI サービスの破損により、Windows Communication Foundation WMI プロバイダーのインストールがブロックされることがあります。 インストール中、Windows Communication Foundation インストーラーは mofcomp.exe コンポーネントを使用して WCF .mof ファイルを登録できません。 発生する現象を次に示します。  
  
1. .NET Framework 3.0 のインストールは正常に完了するのに、WCF WMI プロバイダーが登録されない。  
  
2. アプリケーション イベント ログに、WCF の WMI プロバイダーの登録、または mofcomp.exe の実行に関する問題を示すエラー イベントが表示される。  
  
3. ユーザーの %temp% ディレクトリの dd_wcf_retCA* という名前のセットアップ ログ ファイルに、WCF WMI プロバイダーの登録に失敗したことが示される。  
  
4. イベント ログまたはセットアップ トレース ログ ファイルに、次の例外のいずれかが記録される。  
  
     ServiceModelReg [11:09:59:046]: System.ApplicationException : "E:\WINDOWS\Microsoft.NET\Framework\v3.0\Windows Communication Foundation\ServiceModel.mof" で E:\WINDOWS\system32\wbem\mofcomp.exe を実行している間に予期しない結果 3 が発生しました  
  
     または  
  
     ServiceModelReg [07:19:33:843]: System.TypeInitializationException : 'System.Management.ManagementPath' の型初期化子が例外をスローしました。 ---> System.Runtime.InteropServices.COMException (0x80040154): CLSID {CF4CC405-E2C5-4DDD-B3CE-5E7582D8C9FA は次のエラーのため失敗しました: 80040154.  
  
     または  
  
     ServiceModelReg [07:19:32:750]: System.IO.FileNotFoundException : ファイルまたはアセンブリ 'C:\WINDOWS\system32\wbem\mofcomp.exe'、またはその依存関係の 1 つが読み込めませんでした。 指定されたファイルが見つかりません。  
  
     ファイル名 : C:\WINDOWS\system32\wbem\mofcomp.exe  
  
 上で説明した問題を解決するためには、次の手順を実行する必要があります。  
  
1. WMI[診断ユーティリティ](https://www.microsoft.com/download/details.aspx?id=7684)を実行して、WMI サービスを修復します。 このツールの使用の詳細については、「 [WMI 診断ユーティリティ](https://docs.microsoft.com/previous-versions/tn-archive/ff404265(v%3dmsdn.10))」を参照してください。  
  
 **コントロール パネル**の **[プログラムの追加と削除**] を使用して .NET Framework 3.0 のインストールを修復するか、.NET Framework 3.0 をアンインストールまたは再インストールします。  
  
## <a name="repairing-net-framework-30-after-net-framework-35-installation-removes-configuration-elements-introduced-by-net-framework-35-in-machineconfig"></a>.NET Framework 3.5 のインストール後に .NET Framework 3.0 を修復すると、.NET Framework 3.5 によって導入された machine.config 内の構成要素が削除される  
 .NET Framework 3.5 をインストールした後で .NET Framework 3.0 の修復を実行すると、machine.config で .NET Framework 3.5 によって導入された構成要素が削除されます。 ただし、web.config は元の状態のままになります。 回避策は、ARP を介してこの後に .NET Framework 3.5 を修復するか、またはワーク[フロー サービス登録ツール (WFServicesReg.exe) を](workflow-service-registration-tool-wfservicesreg-exe.md)スイッチと共に使用することです`/c`。  
  
 [ワークフロー サービス登録ツール (WFServicesReg.exe) は](workflow-service-registration-tool-wfservicesreg-exe.md)、%ウィンディル%\マイクロソフト.NET\フレームワーク\v3.5\または %ウィンディル%\マイクロソフト\フレームワーク64\v3.5\ にあります。  
  
## <a name="configure-iis-properly-for-wcfwf-webhost-after-installing-net-framework-35"></a>.NET Framework 3.5 のインストール後に WCF/WF Webhost に対して IIS を適切に構成する  
 .NET Framework 3.5 のインストールで WCF 関連の IIS 構成設定の追加構成が失敗すると、インストール ログにエラーが記録され、続行されます。 WorkflowServices アプリケーションを実行しようとしても、必要な構成設定がないため、実行することはできません。 たとえば、xoml やルール サービスの読み込みに失敗する可能性があります。  
  
 この問題を回避するには、[ワークフロー サービス登録ツール (WFServicesReg.exe)](workflow-service-registration-tool-wfservicesreg-exe.md) `/c`を使用して、コンピューター上の IIS スクリプト マップを適切に構成します。 [ワークフロー サービス登録ツール (WFServicesReg.exe) は](workflow-service-registration-tool-wfservicesreg-exe.md)、%ウィンディル%\マイクロソフト.NET\フレームワーク\v3.5\または %ウィンディル%\マイクロソフト\フレームワーク64\v3.5\ にあります。  
  
## <a name="could-not-load-type-systemservicemodelactivationhttpmodule-from-assembly-systemservicemodel-version-3000-cultureneutral-publickeytokenb77a5c561934e089"></a>アセンブリ 'システム.サービスモデル、バージョン 3.0.0.0、カルチャ=ニュートラル、公開キートークン=b77a5c561934e089' から型 'System.ServiceModel.Activation.HttpModule' を読み込むことができませんでした。  
 このエラーは、.NET Framework 4 がインストールされている場合に発生し、WCF HTTP のアクティブ化が有効になります。 この問題を解決するには、Visual Studio の開発者コマンド プロンプト内から次のコマンド ラインを実行します。  
  
```console
aspnet_regiis.exe -i -enable  
```  
  
## <a name="see-also"></a>関連項目

- [セットアップ手順](./samples/set-up-instructions.md)
