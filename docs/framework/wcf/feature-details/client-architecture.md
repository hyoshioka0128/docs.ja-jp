---
title: クライアント アーキテクチャ
ms.date: 03/30/2017
ms.assetid: 02624403-0d77-41cb-9a86-ab55e98c7966
ms.openlocfilehash: c873368b82551312d203eb28d208eb6e3f50c89b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84587002"
---
# <a name="client-architecture"></a>クライアント アーキテクチャ
アプリケーションは、Windows Communication Foundation (WCF) クライアントオブジェクトを使用してサービス操作を呼び出します。 このトピックでは、WCF クライアントオブジェクト、WCF クライアントチャネル、および基になるチャネルアーキテクチャとの関係について説明します。 WCF クライアントオブジェクトの基本的な概要については、「 [Wcf クライアントの概要](../wcf-client-overview.md)」を参照してください。 チャネルレイヤーの詳細については、「[チャネルレイヤーの拡張](../extending/extending-the-channel-layer.md)」を参照してください。  
  
## <a name="overview"></a>概要  
 サービスモデルの実行時には、次のような WCF クライアントが作成されます。  
  
- 自動的に生成される、サービス コントラクトのクライアント実装。これは、アプリケーション コードからの呼び出しを送信メッセージに変換すると共に、応答メッセージを出力パラメーターに変換して、アプリケーションが取得できる値を返します。  
  
- コントロール インターフェイス (<xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType>) の実装。これは、さまざまなインターフェイスをグループ化し、コントロールの機能 (特に、クライアント セッションの終了機能とチャネルの破棄機能) へのアクセスを提供します。  
  
- クライアント チャネル。これは、使用するバインディングによって指定される構成設定に基づいて構築されます。  
  
 アプリケーションは、を使用するか、 <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> <xref:System.ServiceModel.ClientBase%601> [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)によって生成される派生クラスのインスタンスを作成することによって、このようなクライアントをオンデマンドで作成できます。 これらの作成済みのクライアント クラスは、<xref:System.ServiceModel.ChannelFactory> によって動的に構築されるクライアント チャネル実装にカプセル化され、処理が代行されます。 したがって、クライアント チャネルと、クライアント チャネルを生成するチャネル ファクトリが、このトピックの説明の中心となります。  
  
## <a name="client-objects-and-client-channels"></a>クライアント オブジェクトとクライアント チャネル  
 WCF クライアントの基本インターフェイスは、の <xref:System.ServiceModel.IClientChannel?displayProperty=nameWithType> 主要なクライアント機能だけでなく、の基本的な通信オブジェクト機能、の <xref:System.ServiceModel.ICommunicationObject?displayProperty=nameWithType> コンテキスト機能、 <xref:System.ServiceModel.IContextChannel?displayProperty=nameWithType> およびの拡張可能な動作を公開するインターフェイスです <xref:System.ServiceModel.IExtensibleObject%601?displayProperty=nameWithType> 。  
  
 ただし、<xref:System.ServiceModel.IClientChannel> インターフェイスではサービス コントラクトそのものは定義しません。 これらは、サービスコントラクトインターフェイスによって宣言されます (通常、 [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)などのツールを使用してサービスメタデータから生成されます)。 WCF クライアント型は、 <xref:System.ServiceModel.IClientChannel> とターゲットのサービスコントラクトインターフェイスの両方を拡張して、アプリケーションが操作を直接呼び出すことができ、クライアント側の実行時機能にもアクセスできるようにします。 WCF クライアントを作成すると、WCF オブジェクトは、 <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> 構成されたサービスエンドポイントに接続して操作できる実行時間を作成するために必要な情報を提供します。  
  
 前述のように、2つの WCF クライアントの種類は、使用する前に構成する必要があります。 最も単純な WCF クライアントの種類は、から派生するオブジェクト <xref:System.ServiceModel.ClientBase%601> ( <xref:System.ServiceModel.DuplexClientBase%601> サービスコントラクトが双方向コントラクトの場合) です。 これらのクライアント型はコンストラクターを使用して作成し、プログラムで構成するか、または構成ファイルを使用して構成します。また、サービス操作を呼び出すために直接呼び出されます。 オブジェクトの基本的な概要につい <xref:System.ServiceModel.ClientBase%601> ては、「 [WCF クライアントの概要](../wcf-client-overview.md)」を参照してください。  
  
 2 番目のクライアント型は、実行時に <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A> メソッドへの呼び出しから生成されます。 通信の詳細を厳重に制御しているアプリケーションは、通常、*クライアントチャネルオブジェクト*と呼ばれるこのクライアントの種類を使用します。これは、基になるクライアントランタイムおよびチャネルシステムよりも直接的なやり取りを可能にするためです。  
  
## <a name="channel-factories"></a>チャネル ファクトリ  
 クライアント呼び出しをサポートする、基になるランタイムを作成するクラスは、<xref:System.ServiceModel.ChannelFactory%601?displayProperty=nameWithType> クラスです。 WCF クライアントオブジェクトと WCF クライアントチャネルオブジェクトは、どちらもオブジェクトを使用して <xref:System.ServiceModel.ChannelFactory%601> インスタンスを作成します。 <xref:System.ServiceModel.ClientBase%601> 派生クライアントオブジェクトは、チャネルファクトリの処理をカプセル化しますが、多くのシナリオでは、チャネルファクトリを直接使用するのが適切です。 よくあるシナリオとしては、既存のファクトリから新しいクライアント チャネルを繰り返し作成する必要がある場合です。 クライアントオブジェクトを使用している場合は、プロパティを呼び出すことによって、WCF クライアントオブジェクトから基になるチャネルファクトリを取得でき <xref:System.ServiceModel.ClientBase%601.ChannelFactory%2A?displayProperty=nameWithType> ます。  
  
 チャネル ファクトリに関して覚えておく必要のある重要なことは、これらのファクトリが、<xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType> を呼び出す前に、指定されている構成のクライアント チャネルの新しいインスタンスを作成するという点です。 <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A>(または、、 <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType> <xref:System.ServiceModel.ClientBase%601.CreateChannel%2A?displayProperty=nameWithType> 、またはいずれかの WCF クライアントオブジェクトに対する任意の操作) を呼び出した後、チャネルファクトリを変更することはできません。また、ターゲットエンドポイントアドレスを変更するだけの場合でも、異なるサービスインスタンスにチャネルを取得することが想定されます。 異なる構成でクライアント オブジェクトやクライアント チャネルを作成するには、まず新しいチャネル ファクトリを作成する必要があります。  
  
 Wcf クライアントオブジェクトと WCF クライアントチャネルを使用したさまざまな問題の詳細については、「 [Wcf クライアントを使用したサービスへのアクセス](accessing-services-using-a-client.md)」を参照してください。  
  
 次の2つのセクションでは、WCF クライアントチャネルオブジェクトの作成と使用について説明します。  
  
#### <a name="creating-a-new-wcf-client-channel-object"></a>新しい WCF クライアント チャネル オブジェクトの作成  
 次のサービス コントラクトが生成されていることを前提に、クライアント チャネルの使用方法を説明します。  
  
 [!code-csharp[C_GeneratedCodeFiles#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#12)]  
  
 `ISampleService` サービスに接続するには、チャネル ファクトリ (<xref:System.ServiceModel.ChannelFactory%601>) を直接使用して生成したコントラクト インターフェイスを使用します。 特定のコントラクトのチャネル ファクトリを作成して構成した後は、<xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A> メソッドを呼び出して、`ISampleService` サービスとの通信に使用できるクライアント チャネル オブジェクトを返すことができます。  
  
 サービス コントラクト インターフェイスで <xref:System.ServiceModel.ChannelFactory%601> クラスを使用する場合、明示的にチャネルを開いたり、閉じたり、中止したりするには、 <xref:System.ServiceModel.IClientChannel> インターフェイスにキャストする必要があります。 処理を容易にするために、Svcutil.exe ツールでは、サービス コントラクト インターフェイスと <xref:System.ServiceModel.IClientChannel> の両方を実装するヘルパー インターフェイスも生成されます。これにより、キャストを行わずにクライアント チャネル インフラストラクチャとのやりとりを実現できます。 上記のサービス コントラクトを実装するヘルパー クライアント チャネルの定義を、次のコード例に示します。  
  
 [!code-csharp[C_GeneratedCodeFiles#13](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_generatedcodefiles/cs/proxycode.cs#13)]  
  
#### <a name="creating-a-new-wcf-client-channel-object"></a>新しい WCF クライアント チャネル オブジェクトの作成  
 クライアント チャネルを使用して `ISampleService` サービスに接続するには、チャネル ファクトリを直接使用して生成したコントラクト インターフェイス (またはヘルパー バージョン) を使用して、コントラクト インターフェイスの型を型パラメーターとして渡します。 特定のコントラクトのチャネル ファクトリを作成して構成したら、<xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType> メソッドを呼び出して、`ISampleService` サービスとの通信に使用できるクライアント チャネル オブジェクトを返すことができます。  
  
 作成したクライアント チャネル オブジェクトで <xref:System.ServiceModel.IClientChannel> とコントラクト インターフェイスを実装します。 その結果、これらを使用して、このコントラクトをサポートするサービスと対話する操作を直接呼び出すことができます。  
  
 クライアント オブジェクトを使用するかクライアント チャネル オブジェクトを使用するかは、開発者がきめ細かな制御を優先するか容易さを優先するかの違いだけです。 クラスやオブジェクトの操作に慣れている多くの開発者は、WCF クライアントチャネルではなく、WCF クライアントオブジェクトを使用することをお勧めします。  
  
 例については、「[方法: ChannelFactory を使用する](how-to-use-the-channelfactory.md)」を参照してください。
