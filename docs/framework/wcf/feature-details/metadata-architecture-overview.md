---
title: メタデータ アーキテクチャの概要
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WCF], overview
ms.assetid: 1d37645e-086d-4d68-a358-f3c5b6e8205e
ms.openlocfilehash: a6bd41fa5aed4c2a22ee7c72087e2da0d7e4ea17
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598854"
---
# <a name="metadata-architecture-overview"></a>メタデータ アーキテクチャの概要
Windows Communication Foundation (WCF) は、サービスメタデータをエクスポート、公開、取得、およびインポートするための豊富なインフラストラクチャを提供します。 WCF サービスでは、メタデータを使用してサービスのエンドポイントと対話する方法を記述し、Svcutil.exe などのツールがサービスにアクセスするためのクライアントコードを自動的に生成できるようにします。  
  
 WCF メタデータインフラストラクチャを構成するほとんどの型は、名前空間に存在し <xref:System.ServiceModel.Description> ます。  
  
 WCF では、クラスを使用して <xref:System.ServiceModel.Description.ServiceEndpoint> サービス内のエンドポイントを記述します。 WCF を使用して、サービスエンドポイントのメタデータを生成したり、サービスメタデータをインポートしてインスタンスを生成したりでき <xref:System.ServiceModel.Description.ServiceEndpoint> ます。  
  
 WCF は、サービスのメタデータを型のインスタンスとして表し <xref:System.ServiceModel.Description.MetadataSet> ます。この構造体は、ws-metadataexchange で定義されたメタデータシリアル化形式に厳密に関連付けられています。 <xref:System.ServiceModel.Description.MetadataSet> 型は、Web サービス記述言語 (WSDL: Web Services Description Language) ドキュメント、XML スキーマ ドキュメント、WS-Policy 表現などの実際のサービス メタデータを <xref:System.ServiceModel.Description.MetadataSection> インスタンスのコレクションとしてバンドルします。 各 <xref:System.ServiceModel.Description.MetadataSection?displayProperty=nameWithType> インスタンスには、特定のメタデータ言語と識別子が含まれます。 <xref:System.ServiceModel.Description.MetadataSection?displayProperty=nameWithType> はその <xref:System.ServiceModel.Description.MetadataSection.Metadata%2A?displayProperty=nameWithType> プロパティに、次のアイテムを含むことができます。  
  
- 生のメタデータ。  
  
- <xref:System.ServiceModel.Description.MetadataReference> のインスタンス。  
  
- <xref:System.ServiceModel.Description.MetadataLocation> のインスタンス。  
  
 <xref:System.ServiceModel.Description.MetadataReference?displayProperty=nameWithType> インスタンスは別のメタデータ交換 (MEX) エンドポイントをポイントし、<xref:System.ServiceModel.Description.MetadataLocation?displayProperty=nameWithType> インスタンスは HTTP URL を使用してメタデータ ドキュメントをポイントします。 WCF では、サービスエンドポイント、サービスコントラクト、バインディング、メッセージ交換パターン、メッセージ、およびサービスによって実装されるエラーメッセージを記述するための WSDL ドキュメントの使用をサポートしています。 サービスで使用されるデータ型は、XML スキーマを使用して WSDL ドキュメントに記述されます。 詳細については、「[スキーマのインポートとエクスポート](schema-import-and-export.md)」を参照してください。 WCF を使用すると、サービス動作、コントラクト動作、およびバインド要素の WSDL 拡張をエクスポートおよびインポートして、サービスの機能を拡張できます。 詳細については、「 [WCF 拡張機能のカスタムメタデータのエクスポート](../extending/exporting-custom-metadata-for-a-wcf-extension.md)」を参照してください。  
  
## <a name="exporting-service-metadata"></a>サービス メタデータのエクスポート  
 WCF では、*メタデータのエクスポート*は、サービスエンドポイントを記述し、それらを並列的に投影するプロセスであり、クライアントがサービスの使用方法を理解するために使用できます。 メタデータを <xref:System.ServiceModel.Description.ServiceEndpoint> インスタンスからエクスポートするには、<xref:System.ServiceModel.Description.MetadataExporter> 抽象クラスの実装を使用します。 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=nameWithType> の実装によって、<xref:System.ServiceModel.Description.MetadataSet> インスタンスにカプセル化されたメタデータが生成されます。  
  
 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=nameWithType> クラスには、エンドポイント バインディングの機能と要件、エンドポイントに関連付けられた処理、メッセージ、エラーを記述するポリシー式を生成するためのフレームワークが用意されています。 これらのポリシー式は、<xref:System.ServiceModel.Description.PolicyConversionContext> インスタンスにキャプチャされます。 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=nameWithType> を実装すると、生成したメタデータにこれらのポリシー式を結び付けることができます。  
  
 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=nameWithType> は、<xref:System.ServiceModel.Channels.BindingElement?displayProperty=nameWithType> オブジェクトを <xref:System.ServiceModel.Description.IPolicyExportExtension> の実装で使用するために生成するときに、<xref:System.ServiceModel.Description.ServiceEndpoint> のバインディングで <xref:System.ServiceModel.Description.PolicyConversionContext> インターフェイスを実装する各 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=nameWithType> を呼び出します。 <xref:System.ServiceModel.Description.IPolicyExportExtension> 型のカスタム実装の <xref:System.ServiceModel.Channels.BindingElement> インターフェイスを実装することで、新規のポリシー アサーションをエクスポートできます。  
  
 <xref:System.ServiceModel.Description.WsdlExporter>型は、 <xref:System.ServiceModel.Description.MetadataExporter?displayProperty=nameWithType> WCF に含まれる抽象クラスの実装です。 <xref:System.ServiceModel.Description.WsdlExporter> 型は、結び付けられたポリシー式を使用して WSDL メタデータを生成します。  
  
 サービス エンドポイントでのエンドポイント動作、コントラクト動作、またはバインド要素のカスタム WSDL メタデータまたは WSDL 拡張をエクスポートするには、<xref:System.ServiceModel.Description.IWsdlExportExtension> インターフェイスを実装する必要があります。 <xref:System.ServiceModel.Description.WsdlExporter> は WSDL ドキュメントの生成時に、<xref:System.ServiceModel.Description.ServiceEndpoint> インターフェイスを実装するバインディング要素、処理動作、コントラクト動作、およびエンドポイント動作の <xref:System.ServiceModel.Description.IWsdlExportExtension> インスタンスを参照します。  
  
## <a name="publishing-service-metadata"></a>サービス メタデータの公開  
 WCF サービスは、1つまたは複数のメタデータエンドポイントを公開してメタデータを公開します。 サービス メタデータを公開すると、サービス メタデータで MEX や HTTP/GET 要求などの標準化プロトコルを使用できるようになります。 メタデータ エンドポイントは、アドレス、バインディング、およびコントラクトを持つという点で、他のサービス エンドポイントと似ています。 メタデータ エンドポイントは、構成またはコードを使用してサービス ホストに追加できます。  
  
 WCF サービスのメタデータエンドポイントを公開するには、最初にサービス動作のインスタンスをサービスに追加する必要があり <xref:System.ServiceModel.Description.ServiceMetadataBehavior> ます。 サービスに <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> インスタンスを追加することによって、1 つ以上のメタデータ エンドポイントを公開することでメタデータを公開する機能がサービスに追加されます。 <xref:System.ServiceModel.Description.ServiceMetadataBehavior?displayProperty=nameWithType> サービス動作を追加すると、MEX プロトコルをサポートするメタデータ エンドポイント、または HTTP/GET 要求に応答するメタデータ エンドポイントを公開できます。  
  
 MEX プロトコルを使用するメタデータエンドポイントを追加するには、IMetadataExchange という名前のサービスコントラクトを使用するサービスエンドポイントをサービスホストに追加します。 WCF <xref:System.ServiceModel.Description.IMetadataExchange> は、このサービスコントラクト名を持つインターフェイスを定義します。 Ws-metadataexchange エンドポイントまたは MEX エンドポイントは、クラスの静的ファクトリメソッドによって公開されている4つの既定のバインディングのいずれかを使用して、 <xref:System.ServiceModel.Description.MetadataExchangeBindings> svcutil.exe などの WCF ツールで使用される既定のバインディングに一致させることができます。 また、カスタム バインドを使用して MEX メタデータ エンドポイントを構成することもできます。  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> は <xref:System.ServiceModel.Description.WsdlExporter?displayProperty=nameWithType> を使用して、サービス内のすべてのサービス エンドポイント用のメタデータをエクスポートします。 サービスからメタデータをエクスポートする方法の詳細については、「[メタデータのエクスポートとインポート](exporting-and-importing-metadata.md)」を参照してください。  
  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> は、<xref:System.ServiceModel.Description.ServiceMetadataExtension> インスタンスを拡張としてサービス ホストに追加することで、サービス ホストを拡張します。 <xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=nameWithType> により、メタデータ公開プロトコルを実装することができます。 また、<xref:System.ServiceModel.Description.ServiceMetadataExtension?displayProperty=nameWithType> を使用して、<xref:System.ServiceModel.Description.ServiceMetadataExtension.Metadata%2A> プロパティにアクセスすることにより、実行時にサービスのメタデータを取得できます。  
  
> [!CAUTION]
> MEX エンドポイントをアプリケーション構成ファイルに追加した後で、<xref:System.ServiceModel.Description.ServiceMetadataBehavior> をコード内のサービス ホストに追加しようとすると、次の例外が発生します。  
>
> System.InvalidOperationException: コントラクト名 'IMetadataExchange' は、サービス Service1 によって実装されたコントラクトの一覧に見つかりませんでした。 ServiceMetadataBehavior を構成ファイルまたは ServiceHost ディレクトリに直接追加してこのコントラクトのサポートを有効にしてください。  
>
> <xref:System.ServiceModel.Description.ServiceMetadataBehavior> を構成ファイルに追加するか、またはエンドポイントと <xref:System.ServiceModel.Description.ServiceMetadataBehavior> の両方をコードに追加することにより、この問題を回避できます。  
>
> アプリケーション構成ファイルにを追加する例につい <xref:System.ServiceModel.Description.ServiceMetadataBehavior> ては、[はじめに](../samples/getting-started-sample.md)を参照してください。 をコードに追加する例については、 <xref:System.ServiceModel.Description.ServiceMetadataBehavior> [自己ホスト](../samples/self-host.md)のサンプルを参照してください。  

> [!CAUTION]
> それぞれに同じ名前の操作が含まれている 2 つ異なるサービス コントラクトを公開するサービスのメタデータを公開すると、例外がスローされます。 たとえば、Get(Car c) 操作を含む ICarService という名前のサービス コントラクトを公開するサービスがあり、その同じサービスが Get(Book b) 操作を含む IBookService という名前のサービス コントラクトを公開する場合、サービスのメタデータを生成するときに、例外がスローされるか、エラー メッセージが表示されます。 この問題を回避するには、次のいずれかの操作を実行します。  
>
> - 操作の名前を変更する。
> - <xref:System.ServiceModel.OperationContractAttribute.Name%2A> を別の名前に設定する。  
> - <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> プロパティを使用して、操作の名前空間のいずれかを別の名前空間に設定する。  
  
## <a name="retrieving-service-metadata"></a>サービス メタデータの取得  
 WCF では、Ws-metadataexchange や HTTP などの標準化されたプロトコルを使用してサービスメタデータを取得できます。 これらのプロトコルはいずれも、<xref:System.ServiceModel.Description.MetadataExchangeClient> 型でサポートされます。 アドレスとオプションのバインディングを提供することによって、<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> 型を使用して、サービス メタデータを取得します。 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> インスタンスで使用するバインディングは、<xref:System.ServiceModel.Description.MetadataExchangeBindings> 静的クラスの既定のバインディング、ユーザー指定のバインディング、`IMetadataExchange` コントラクト用のエンドポイント構成から読み込まれたバインディングのいずれかです。 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> は同様に、<xref:System.Net.HttpWebRequest> 型を使用して、メタデータへの HTTP URL 参照を解決できます。  
  
 既定では、<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> インスタンスは、1 つの <xref:System.ServiceModel.Channels.ChannelFactoryBase> インスタンスに結び付けられています。 <xref:System.ServiceModel.Channels.ChannelFactoryBase> によって使用される <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> インスタンスは、<xref:System.ServiceModel.Description.MetadataExchangeClient.GetChannelFactory%2A> 仮想メソッドをオーバーライドすることによって変更または置換することができます。 同様に、<xref:System.Net.HttpWebRequest?displayProperty=nameWithType> 仮想メソッドをオーバーライドすることによって、HTTP/GET 要求を行うために <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> が使用する <xref:System.ServiceModel.Description.MetadataExchangeClient.GetWebRequest%2A?displayProperty=nameWithType> インスタンスを変更または置換できます。  
  
 Ws-metadataexchange または HTTP/GET 要求を使用してサービスメタデータを取得するには、Svcutil.exe ツールを使用し、 **/target: metadata**スイッチと address を渡します。 Svcutil.exe は指定したアドレスでメタデータをダウンロードし、ディスクにファイルを保存します。 Svcutil.exe は、<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> インスタンスを内部的に使用し、Svcutil.exe に渡されたアドレスのスキームに一致する名前を持つ MEX エンドポイント構成が存在する場合は、これをアプリケーション構成ファイルから読み込みます。 存在しない場合、Svcutil.exe は、<xref:System.ServiceModel.Description.MetadataExchangeBindings> 静的ファクトリ型によって定義されたバインディングの 1 つを既定で使用します。  
  
## <a name="importing-service-metadata"></a>サービス メタデータのインポート  
 WCF では、メタデータのインポートは、サービスまたはそのコンポーネントの部分の抽象表現をメタデータから生成するプロセスです。 たとえば、WCF では、 <xref:System.ServiceModel.Description.ServiceEndpoint> <xref:System.ServiceModel.Channels.Binding> <xref:System.ServiceModel.Description.ContractDescription> サービスの WSDL ドキュメントからインスタンス、インスタンス、またはインスタンスをインポートできます。 WCF でサービスメタデータをインポートするには、抽象クラスの実装を使用し <xref:System.ServiceModel.Description.MetadataImporter> ます。 クラスから派生する型は <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=nameWithType> 、WCF の ws-policy インポートロジックを利用するメタデータ形式をインポートするためのサポートを実装します。  
  
 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=nameWithType> の実装は、<xref:System.ServiceModel.Description.PolicyConversionContext> オブジェクトでサービス メタデータに結び付けられたポリシー表現を収集します。 その後、<xref:System.ServiceModel.Description.MetadataImporter?displayProperty=nameWithType> は、<xref:System.ServiceModel.Description.IPolicyImportExtension> プロパティ内の <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A> インターフェイスの実装を呼び出すことによって、メタデータのインポートの一部として、ポリシーを処理します。  
  
 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=nameWithType> インスタンスの <xref:System.ServiceModel.Description.IPolicyImportExtension> コレクションに <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A> インターフェイスの独自の実装を追加することによって、新しいポリシー アサーションをインポートするためのサポートを <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=nameWithType> に追加できます。 または、クライアント アプリケーション構成ファイルにポリシー インポート拡張を登録できます。  
  
 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType>型は、 <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=nameWithType> WCF に含まれる抽象クラスの実装です。 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> 型は、<xref:System.ServiceModel.Description.MetadataSet> オブジェクトにまとめられた、結び付けられているポリシーを使用して WSDL メタデータをインポートします。  
  
 <xref:System.ServiceModel.Description.IWsdlImportExtension> インターフェイスを実装し、この実装を <xref:System.ServiceModel.Description.WsdlImporter.WsdlImportExtensions%2A> インスタンスの <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> プロパティに追加することで、WSDL 拡張のインポートのサポートを追加できます。 <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> は、クライアント アプリケーション構成ファイルに登録された <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType> インターフェイスの実装を読み込むこともできます。  
  
## <a name="dynamic-bindings"></a>動的なバインド  
 エンドポイントのバインドが変化するイベントでサービス エンドポイントへのチャネルを作成する、または、同じコントラクトを使用しているがバインドが異なるエンドポイントへのチャネルを作成するために使用するバインドを動的に更新することができます。 <xref:System.ServiceModel.Description.MetadataResolver> 静的クラスを使用して、特定のコントラクトを実装しているサービス エンドポイントのメタデータを、実行時に取得またはインポートできます。 その後、インポートした <xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=nameWithType> オブジェクトを使用して、必要なエンドポイントに対するクライアントまたはチャネル ファクトリを作成できます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Description>
- [メタデータ形式](metadata-formats.md)
- [メタデータのエクスポートとインポート](exporting-and-importing-metadata.md)
- [メタデータの公開](publishing-metadata.md)
- [メタデータの取得](retrieving-metadata.md)
- [メタデータを使用する](using-metadata.md)
- [メタデータを使用する場合のセキュリティ上の考慮事項](security-considerations-with-metadata.md)
- [メタデータ システムの拡張](../extending/extending-the-metadata-system.md)
