---
title: CustomChannelTester
ms.date: 03/30/2017
ms.assetid: ee1fa307-98b1-4647-8860-2e9217ba6082
ms.openlocfilehash: 9123167e0f97592592765f7b4a4aa768064fc173
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596605"
---
# <a name="customchannelstester"></a>CustomChannelTester
`CustomChannelsTester` は、カスタム チャネルの実装を、定義済みのサービス コントラクト セットに対してテストする際に使用できるツールです。 サービス コントラクト セットを選択し、XML ファイルを使用してこのツールに渡すことができます。 これを受け取ったツールは、メッセージ交換中にカスタム チャネル実装をテストするサービスとクライアントを生成します。  
  
### <a name="to-build-the-tool"></a>ツールをビルドするには  
  
1. ソリューションをビルドするには、「 [Windows Communication Foundation サンプルのビルド](building-the-samples.md)」の手順に従います。  
  
2. ソリューションをビルドすると、CustomChannelsTester.exe、TestSpec.xml、および SampleRun.cmd の 3 つのファイルが生成されます。 Samplerun.cmd ファイルには、このツールを使用して[Transport: UDP](transport-udp.md)サンプルをテストする方法を示すサンプルコマンドラインがあります。  
  
### <a name="to-run-the-tool"></a>ツールを実行するには  
  
- コマンド プロンプトに次のコマンドを入力します。  
  
    ```console  
    CustomChannelsTester.exe /binding:YourCustomBindngName /dll:TheAssemblyWhereThisTypeisDefined /testspec:XmlFileNameWhichContainsTestOptions  
    ```  
  
     `/binding` オプションを使用する必要があります。  
  
     `/dll`"binding" が Windows Communication Foundation (WCF) によって提供されるシステム指定のバインディングでない場合は、が必要です。  
  
     `/testspec` はオプションです。  
  
     これにより、テストの仕様とバインディングに基づくサーバーとクライアントが作成されます。  
  
     クライアントとサーバーを実行し、結果が返されます。  
  
     テストの仕様を説明する XML のサンプルを次に示します (testspec.xml)。  
  
    ```xml  
    <TestSpec xmlns="http://WCF/TestSpec" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" >  
    <ServiceContract>  
    <!-- Test a contract which has oneway / twoway operations. If you set ExpandAll = true, both types of contracts are tested -->    <IsOneWay ExpandAll="true">true</IsOneWay>  
    <!-- Test a contract with Asynchronous / Synchronous Operations-->  
        <IsAsync>false</IsAsync>
    <!-- Test a sessionful / sessionless contract-->
        <IsSession ExpandAll="true">true</IsSession>  
    <!-- If the Service Contract includes a CallBack Contract-->
        <IsCallBack ExpandAll="true">true</IsCallBack>  
    </ServiceContract>  
    <TestDetails>  
    <!-- Name of the machine that runs the server - required if you want to run the test crossmachine-->  
        <ServerName>ReplaceThisWithTheServerMachineName</ServerName>  
    <!-- Port Number - Optional-->  
        <Port>8000</Port>  
    <!--URI for the callBack address for the client. The client will receive the messages from the server on this address in case of a CallBack Contract-->  
        <ClientCallBackAddress/>
    <!-- Duration (in sec) after the server has started, it times out - optional(default = 300sec) -->  
        <ServerTimeout>300</ServerTimeout>  
    <!-- Duration (in sec) before the Client initializes -optional(default = 60sec) -->  
        <ClientTimeout>60</ClientTimeout>  
    <!-- Number of clients for each service - optional(default = 1) -->  
        <NumberOfClients>1</NumberOfClients>  
    <!-- Number of messages each client sends to the service - optional(default = 1) -->  
        <MessagesPerClient>1</MessagesPerClient>  
    </TestDetails>  
    </TestSpec>  
    ```  
