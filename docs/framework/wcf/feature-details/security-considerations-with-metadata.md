---
title: メタデータを使用する場合のセキュリティ上の考慮事項
ms.date: 03/30/2017
ms.assetid: e78ef8ab-4f63-4656-ab93-b1deab2666d5
ms.openlocfilehash: c41ebf5c39e74932a4bade610c4e236b28444327
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601024"
---
# <a name="security-considerations-with-metadata"></a>メタデータを使用する場合のセキュリティ上の考慮事項
Windows Communication Foundation (WCF) のメタデータ機能を使用する場合は、サービスメタデータの公開、取得、および使用のセキュリティへの影響について検討してください。  
  
## <a name="when-to-publish-metadata"></a>メタデータを公開する場合と公開しない場合  
 既定では、WCF サービスはメタデータを公開しません。 WCF サービスのメタデータを公開するには、メタデータエンドポイントをサービスに追加してメタデータの公開を明示的に有効にする必要があります (「[メタデータの公開](publishing-metadata.md)」を参照)。 メタデータの公開を無効のままにしておけば、攻撃者にとっては侵入経路が少ないことになり、したがって情報漏洩の危険を減らすことができます。 メタデータを公開する必要のないサービスもあります。 必要ないのであれば無効のままにしておくようお勧めします。 [ServiceModel メタデータユーティリティツール (svcutil.exe)](../servicemodel-metadata-utility-tool-svcutil-exe.md)を使用して、サービスアセンブリから直接メタデータとクライアントコードを生成することもできます。 Svcutil.exe を使用してメタデータをエクスポートする方法の詳細については、「[方法: svcutil.exe を使用してコンパイル済みサービスコードからメタデータをエクスポートする](how-to-use-svcutil-exe-to-export-metadata-from-compiled-service-code.md)」を参照してください。  
  
## <a name="publishing-metadata-using-a-secure-binding"></a>セキュリティ保護されたバインディングによるメタデータの公開  
 WCF によって提供される既定のメタデータバインディングはセキュリティで保護されていないため、メタデータへの匿名アクセスが許可されます。 WCF サービスによって公開されるサービスメタデータには、サービスに関する詳細な説明が含まれており、意図的または意図せずに機密情報が含まれている可能性があります。 たとえば、一般に公開するべきではない、インフラストラクチャ操作に関する情報が入った状態で発行される可能性があるのです。 権限のないアクセスを拒否する方法として、メタデータ エンドポイントで、セキュリティ保護されたバインディングを使う、というものがあります。 メタデータ エンドポイントは HTTP/GET 要求に応答しますが、ここに SSL (Secure Sockets Layer) を使用すれば、メタデータを保護できます。 詳細については、「[方法: メタデータエンドポイントをセキュリティで保護](how-to-secure-metadata-endpoints.md)する」を参照してください。  
  
 メタデータ エンドポイントを保護することで、正当なユーザーが、改ざんやなりすましを恐れずに安全にサービス メタデータを取得できる手段も提供されます。  
  
## <a name="using-only-trusted-metadata"></a>信頼できるメタデータのみを使用  
 サービス メタデータを使用すると、サービスの呼び出しに必要なランタイム コンポーネントを自動構築できます。 たとえば、設計時には、クライアント アプリケーションを開発するためにメタデータを利用できます。また、実行時には、メタデータを利用して、クライアントがサービス呼び出しのために使用するバインディングを動的に更新できます。  
  
 サービス メタデータを取得する際、セキュリティ保護された方法を使わないと、改ざんやなりすましのおそれがあります。 メタデータが改ざんされると、知らない間に悪質なサービスに接続されたり、セキュリティ上問題のある設定に切り替えられたり、XML 構造が破壊されたりすることがあります。 メタデータ ドキュメントはかなりの容量になることがあるので、多くの場合、ファイル システムに保存することになります。 改ざんやなりすましを防ぐために、サービス メタデータを要求するときには、できるだけセキュリティで保護されたバインディングを使用してください。  
  
## <a name="using-safe-techniques-for-processing-metadata"></a>安全な技術を使ってメタデータを処理  
 サービス メタデータは多くの場合、MEX (WS-Metadata Exchange) などの標準的なプロトコルを使用して、ネットワーク経由で伝送されます。 メタデータの形式を見ると、多くの場合、他のメタデータを参照する旨の記述ができるようになっています。 <xref:System.ServiceModel.Description.MetadataExchangeClient> 型は、Web サービス記述言語 (WSDL) ドキュメント、XML スキーマ、および MEX ドキュメント内の参照を自動的に処理します。 取得したメタデータから生成される <xref:System.ServiceModel.Description.MetadataSet> オブジェクトのサイズは、使用されている <xref:System.ServiceModel.Description.MetadataExchangeClient.MaximumResolvedReferences%2A> インスタンスの <xref:System.ServiceModel.Description.MetadataExchangeClient> の値と、この `MaxReceivedMessageSize` インスタンスが使用するバインディングの <xref:System.ServiceModel.Description.MetadataExchangeClient> の値に比例します。 動作環境に合わせてこのクォータ値を適切に設定してください。  
  
 WCF では、サービスメタデータは XML として処理されます。 XML ドキュメントを処理するアプリケーションは、悪質な XML 構造が現れても破綻しないようになっていなければなりません。 XML を <xref:System.Xml.XmlDictionaryReader> 処理するときに、適切なクォータを持つを使用し、 <xref:System.Xml.XmlTextReader.DtdProcessing%2A> プロパティをに設定し <xref:System.Xml.DtdProcessing.Prohibit> ます。  
  
 WCF のメタデータシステムは拡張可能であり、メタデータ拡張をアプリケーション構成ファイルに登録できます (「[メタデータシステムの拡張](../extending/extending-the-metadata-system.md)」を参照してください)。 メタデータ拡張はどのようなコードでも実行できるので、適切なアクセス制御リスト (ACL) でアプリケーション構成ファイルを保護し、信頼できるメタデータ拡張以外は登録しないようにする必要があります。  
  
## <a name="validating-generated-clients"></a>生成されたクライアントの検証  
 信頼できないソースから取得したメタデータを基にクライアント コードを生成した場合、これがクライアント アプリケーションのセキュリティ ポリシーに合致しているかどうか検証する必要があります。 動作を検証するための専用クライアントを使うか、あるいはツールが生成したコードを目視で検査してください。 動作を検証するクライアントを実装する方法の例については、「[クライアントの検証](../samples/client-validation.md)」を参照してください。  
  
## <a name="protecting-application-configuration-files"></a>アプリケーション構成ファイルの保護  
 サービスのアプリケーション構成ファイルでは、メタデータを公開する方法、および公開の有無を制御できます。 攻撃者が設定を変更できないように、適切なアクセス制御リスト (ACL) でアプリケーション構成ファイルを保護することをお勧めします。  
  
## <a name="see-also"></a>関連項目

- [方法: セキュリティで保護されたメタデータ エンドポイント](how-to-secure-metadata-endpoints.md)
- [Security](security.md)
