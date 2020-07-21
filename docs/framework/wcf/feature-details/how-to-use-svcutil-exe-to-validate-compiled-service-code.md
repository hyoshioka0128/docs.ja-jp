---
title: '方法: Svcutil.exe を使用してコンパイル済みサービス コードを検証する'
ms.date: 03/30/2017
ms.assetid: d0d820fb-41c2-45b8-8f22-0fa5aeebbbaa
ms.openlocfilehash: 6f2064c696e3186c3208a7e57dc51655056d23ea
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595350"
---
# <a name="how-to-use-svcutilexe-to-validate-compiled-service-code"></a>方法: Svcutil.exe を使用してコンパイル済みサービス コードを検証する
[ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を使用して、サービスをホストせずにサービスの実装と構成のエラーを検出できます。  
  
### <a name="to-validate-a-service"></a>サービスを検証するには  
  
1. サービスを実行可能ファイルおよび 1 つ以上の依存アセンブリにコンパイルします。  
  
2. SDK コマンド プロンプトを開きます。  
  
3. コマンド プロンプトで、次の形式を使用して Svcutil.exe ツールを起動します。 さまざまなパラメーターの詳細については、「 [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md) 」トピックの「サービスの検証」セクションを参照してください。  
  
    ```console
    svcutil.exe /validate /serviceName:<serviceConfigName>  <assemblyPath>*  
    ```  
  
     `/serviceName` オプションを使用して、検証するサービスの構成名を指定する必要があります。  
  
     `assemblyPath` 引数には、検証対象のサービスの実行可能ファイルへのパス、およびサービス型を格納している 1 つ以上のアセンブリへのパスを指定します。 実行可能アセンブリに、サービス構成を提供する関連構成ファイルが存在している必要があります。 標準のコマンドライン ワイルドカードを使用して、複数のアセンブリを指定できます。  
  
## <a name="example"></a>例  
 次のコマンドでは、myServiceHost.exe 実行可能ファイルに実装されたサービス myServiceName を検証します。  サービスの構成ファイル (myServiceHost.exe.config) は自動的に読み込まれます。  
  
```console  
svcutil /validate /serviceName:myServiceName myServiceHost.exe  
```  
  
## <a name="see-also"></a>関連項目

- [ServiceModel メタデータ ユーティリティ ツール (Svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)
