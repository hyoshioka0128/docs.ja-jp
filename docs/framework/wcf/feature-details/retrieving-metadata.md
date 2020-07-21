---
title: メタデータを取得する
ms.date: 03/30/2017
helpviewer_keywords:
- metadata [WCF], retrieving
ms.assetid: 18d8ba4c-af0f-4827-a50b-4202d767bacc
ms.openlocfilehash: 5488e2b0778738927922edab0f948645b816a1f6
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84586222"
---
# <a name="retrieving-metadata"></a>メタデータを取得する
メタデータの取得は、WS-MetadataExchange (MEX) メタデータ エンドポイントや HTTP/GET メタデータ エンドポイントなどのメタデータ エンドポイントに対してメタデータを要求して取得する処理です。  
  
## <a name="retrieving-metadata-from-the-command-line-using-svcutilexe"></a>Svcutil.exe を使用した、コマンドラインからのメタデータの取得  
 [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)ツールを使用し、スイッチとアドレスを渡すことにより、ws-metadataexchange または HTTP/GET 要求を使用してサービスメタデータを取得でき `/target:metadata` ます。 Svcutil.exe は指定したアドレスでメタデータをダウンロードし、ディスクにファイルを保存します。 Svcutil.exe は内部的に <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> インスタンスを使用し、構成 (Svcutil.exe に入力として渡されたアドレスのスキーマに一致する名前の <xref:System.ServiceModel.Description.IMetadataExchange> エンドポイント構成) から読み込まれます。  
  
## <a name="retrieving-metadata-programmatically-using-the-metadataexchangeclient"></a>MetadataExchangeClient を使用した、プログラムによるメタデータの取得  
 Windows Communication Foundation (WCF) は、Ws-metadataexchange や HTTP/GET 要求などの標準化されたプロトコルを使用してサービスメタデータを取得できます。 これらのプロトコルはいずれも、<xref:System.ServiceModel.Description.MetadataExchangeClient> 型でサポートされます。 メタデータ エンドポイントのアドレスとオプションのバインディングを指定することにより、<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> 型を使用してサービス メタデータを取得します。 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> インスタンスで使用するバインディングは、<xref:System.ServiceModel.Description.MetadataExchangeBindings> 静的クラスの既定のバインディング、ユーザー指定のバインディング、`IMetadataExchange` コントラクト用のエンドポイント構成から読み込まれたバインディングのいずれかです。 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> は同様に、<xref:System.Net.HttpWebRequest> 型を使用して、メタデータへの HTTP URL 参照を解決できます。  
  
 既定では、<xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> インスタンスは、1 つの <xref:System.ServiceModel.ChannelFactory> インスタンスに結び付けられています。 <xref:System.ServiceModel.ChannelFactory?displayProperty=nameWithType> によって使用される <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> インスタンスは、<xref:System.ServiceModel.Description.MetadataExchangeClient.GetChannelFactory%2A> 仮想メソッドをオーバーライドすることによって変更または置換することができます。 同様に、<xref:System.Net.HttpWebRequest> 仮想メソッドをオーバーライドすることによって、HTTP/GET 要求を行うために <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> が使用する <xref:System.ServiceModel.Description.MetadataExchangeClient.GetWebRequest%2A?displayProperty=nameWithType> インスタンスを変更または置換できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: Svcutil.exe を使用してメタデータ ドキュメントをダウンロードする](how-to-use-svcutil-exe-to-download-metadata-documents.md)  
 Svcutil.exe を使用して、メタデータ ドキュメントをダウンロードする方法を示します。  
  
 [方法: MetadataResolver を使用してバインディング メタデータを動的に取得する](how-to-use-metadataresolver-to-obtain-binding-metadata-dynamically.md)  
 <xref:System.ServiceModel.Description.MetadataResolver?displayProperty=nameWithType> を使用して、実行時に動的にバインディング メタデータを取得する方法を示します。  
  
 [方法: MetadataExchangeClient を使用してメタデータを取得する](how-to-use-metadataexchangeclient-to-retrieve-metadata.md)  
 <xref:System.ServiceModel.Description.MetadataExchangeClient?displayProperty=nameWithType> クラスを使用して、<xref:System.ServiceModel.Description.MetadataSet?displayProperty=nameWithType> オブジェクトを含む <xref:System.ServiceModel.Description.MetadataSection?displayProperty=nameWithType> オブジェクトにメタデータ ファイルをダウンロードし、ファイルに書き込んだり、他の目的に使用したりする方法を示します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Description.MetadataExchangeClient>
