---
title: '方法: COM+ サービス モデル構成ツールを使用する'
ms.date: 03/30/2017
helpviewer_keywords:
- COM+ [WCF], using service model configuration tool
ms.assetid: 7e68cd8d-5fda-4641-b92f-290db874376e
ms.openlocfilehash: f9e761bafd84726b51a2010a932c68c67c37f899
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595285"
---
# <a name="how-to-use-the-com-service-model-configuration-tool"></a>方法: COM+ サービス モデル構成ツールを使用する
適切なホスト モードを選択したら、COM+ サービス モデル構成コマンド ライン ツール (ComSvcConfig.exe) を使用して、Web サービスとして公開されるアプリケーション インターフェイスを構成します。  
  
> [!NOTE]
> 以下の各タスクを実行するには、コンピューターの管理者である必要があります。  
  
 Windows 7 コンピューターで ComSvcConfig.exe を使用して、最新のサービス モデル バージョン (現在 v4.5) を使用するように Web サービスを構成する場合は、次の手順を実行します。  
  
1. レジストリキーを `[HKEY_LOCAL_COMPUTER\SOFTWARE\Microsoft\.NETFramework]\OnlyUseLatestCLR` DWORD 値0x00000001 に設定します。  
  
2. comsvcconfig.exe を実行します。  
  
3. 手順 1. で追加したレジストリ キーを元の値に戻すか、存在しない場合は削除します。  
  
> [!IMPORTANT]
> このレジストリ キーを元に戻すことは重要です。 これは互換性のキーです。 この変更を元に戻さないと、コンピューターで実行している他の .NET アプリケーションで問題が発生する可能性があります。  
  
> [!WARNING]
> Windows 8 コンピューターで Comsvcconfig.exe/install を使用すると、ダイアログが表示されます。 "PC 上のアプリには、次の Windows 機能が必要です: .NET Framework 3.5 (.NET Framework 3.5 がインストールされていない場合は、.NET 2.0 と .NET 3.0 が含まれています。 このダイアログは無視してもかまいません。 また、OnlyUseLatestCLR レジストリ キーを DWORD 値 0x00000001 に設定することもできます。  
  
## <a name="to-add-an-interface-to-the-set-of-interfaces-exposed-as-web-services-using-the-com-hosting-mode"></a>COM + ホストモードを使用して、Web サービスとして公開されるインターフェイスのセットにインターフェイスを追加するには  
  
- 次の例に示すように、`/install` オプションと `/hosting:complus` オプションを使用して ComSvcConfig を実行します。  
  
    ```console  
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus /verbose  
    ```  
  
     このコマンドは、Web サービスとして公開されるインターフェイスのセットに (OnlineStore COM+ アプリケーションの) `IFinances` コンポーネントの `ItemOrders.IFinancial` インターフェイスを追加します。 サービスは COM+ ホスト モードを使用するため、アプリケーションを明示的にアクティブ化する必要があります。  
  
     コンポーネントとインターフェイスにはワイルドカードアスタリスク ( \* ) 文字を使用できますが、選択した機能のみを Web サービスとして公開することが必要になる場合があるため、使用しないでください。 ワイルドカードを使用すると、このコンポーネントの将来のバージョンを使用して実行したときに、構成構文の決定時には存在しなかったインターフェイスが誤って公開される可能性があります。  
  
     /verbose オプションを指定すると、ツールは、エラーだけでなく警告も表示します。  
  
     公開されたサービスのコントラクトには、`IFinances` インターフェイスのすべてのメソッドが含まれます。  
  
## <a name="to-add-only-specific-methods-from-an-interface-to-the-set-of-interfaces-exposed-as-web-services-using-the-com-hosting-mode"></a>COM + ホストモードを使用して、Web サービスとして公開されるインターフェイスのセットにインターフェイスの特定のメソッドのみを追加するには  
  
- 次の例に示すように、`/install` オプションと `/hosting:complus` オプション、および必要なメソッドの名前を明示的に指定して、ComSvcConfig を実行します。  
  
    ```console  
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances.{Credit,Debit} /hosting:complus /verbose  
    ```  
  
     このコマンドは、公開されたサービス コントラクトに `Credit` インターフェイスの `Debit` メソッドと `IFinances` メソッドだけを操作として追加します。 インターフェイスのその他のメソッドはすべてコントラクトから除外されるため、Web サービス クライアントから呼び出すことができません。  
  
## <a name="to-add-an-interface-to-the-set-of-interfaces-exposed-as-web-services-using-the-web-hosting-mode"></a>Web ホスティングモードを使用して、Web サービスとして公開されるインターフェイスのセットにインターフェイスを追加するには  
  
- 次の例に示すように、`/install` オプションと `/hosting:was` オプションを使用して ComSvcConfig を実行します。  
  
    ```console  
    ComSvcConfig.exe /install /application:OnlineWarehouse /contract:ItemInventory.Warehouse,IStockLevels /hosting:was /webDirectory:root/OnlineWarehouse /mex /verbose  
    ```  
  
     このコマンドは、Web サービスとして公開されるインターフェイスのセットに (OnlineWarehouse COM+ アプリケーションの) `IStockLevels` コンポーネントの `ItemInventory.Warehouse` インターフェイスを追加します。 サービスは、COM+ 内ではなく、IIS の OnlineWarehouse 仮想ディレクトリ内で Web ホストされるため、アプリケーションは、必要に応じて自動的にアクティブ化されます。  
  
     Web ホスト (インプロセス) 構成を使用するには、コンポーネント サービス管理コンソールを使用して、サーバー アプリケーションではなくライブラリ アプリケーションとして実行されるように COM+ アプリケーションを構成する必要があります。 サーバー アプリケーションとして構成されたアプリケーションは、標準の Web ホスト モードを使用するため、各要求の処理でプロセス ホップが発生します。  
  
     `/mex` オプションは、サービスからコントラクト定義を取得するクライアントをサポートするために、アプリケーションのサービス エンドポイントと同じトランスポートを使用する追加の Metadata Exchange (MEX) サービス エンドポイントを追加します。  
  
## <a name="to-remove-a-web-service-for-a-specified-interface"></a>指定したインターフェイスの Web サービスを削除するには  
  
- 次の例に示すように、`/uninstall` のオプションを使用して ComSvcConfig を実行します。  
  
    ```console  
    ComSvcConfig.exe /uninstall /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus  
    ```  
  
     このコマンドは、(OnlineStore COM+ アプリケーションから) `IFinances` コンポーネントの `ItemOrders.Financial` インターフェイスを削除します。  
  
## <a name="to-list-currently-exposed-interfaces"></a>現在公開されているインターフェイスを一覧表示するには  
  
- 次の例に示すように、`/list` のオプションを使用して ComSvcConfig を実行します。  
  
    ```console  
    ComSvcConfig.exe /list  
    ```  
  
     このコマンドは、ローカル コンピューターに関して、現在公開されているインターフェイス、および対応するアドレスとバインディングの詳細を一覧表示します。  
  
## <a name="to-list-specific-currently-exposed-interfaces"></a>現在公開されている特定のインターフェイスを一覧表示するには  
  
- 次の例に示すように、`/list` のオプションを使用して ComSvcConfig を実行します。  
  
    ```console  
    ComSvcConfig.exe /list /application:OnlineStore /hosting:complus  
    ```  
  
     このコマンドは、ローカル コンピューター上の OnlineStore COM+ アプリケーションの現在公開されている COM+ ホスト インターフェイスを、対応するアドレスやバインディングの詳細と共に一覧表示します。  
  
## <a name="to-display-help-on-the-options-that-can-be-used-with-the-utility"></a>ユーティリティで使用できるオプションに関するヘルプを表示するには  
  
- 次の例に示すように、/? オプションを 使用して ComSvcConfig を実行します。  
  
    ```console  
    ComSvcConfig.exe /?  
    ```  
  
## <a name="see-also"></a>関連項目

- [COM + アプリケーションとの統合の概要](integrating-with-com-plus-applications-overview.md)
