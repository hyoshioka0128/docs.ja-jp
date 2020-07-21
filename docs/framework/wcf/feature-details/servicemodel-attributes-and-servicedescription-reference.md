---
title: ServiceModel 属性および ServiceDescription 参照
ms.date: 03/30/2017
ms.assetid: 4ab86b17-eab9-4846-a881-0099f9a7cc64
ms.openlocfilehash: 5e39a63d399edccc580b27ad4bfbc9ab05015ef9
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600349"
---
# <a name="servicemodel-attributes-and-servicedescription-reference"></a>ServiceModel 属性および ServiceDescription 参照
*説明ツリー*は、 <xref:System.ServiceModel.Description.ServiceDescription?displayProperty=nameWithType> サービスのすべての側面をまとめて記述する (クラスから始まる) 型の階層です。 Windows Communication Foundation (WCF) は、説明ツリーを使用して有効なサービスランタイムを構築し、Web サービス記述言語 (WSDL)、XML スキーマ定義言語 (XSD)、およびポリシーアサーション (メタデータ) を公開します。これにより、クライアントがサービスに接続して使用するために使用できるサービスについて、さまざまなコードと構成ファイルの表現を生成  
  
 ここでは、サービス コントラクトからコントラクトに関連するプロパティが取得されるしくみ、およびこれらのプロパティが実装され、説明ツリーに追加されるしくみについて説明します。 属性値が動作プロパティに変換された後、動作が説明ツリーに挿入される場合もあります。 説明ツリーの値をメタデータに変換する方法の詳細については、「 [ServiceDescription と WSDL リファレンス](servicedescription-and-wsdl-reference.md)」を参照してください。  
  
## <a name="mapping-operations-to-the-description-tree"></a>説明ツリーへの操作のマッピング  
 WCF アプリケーションでは、サービスコントラクトは、属性を使用してインターフェイスまたはクラスとそのメソッドを操作のグループとしてマークするインターフェイス (またはクラス) によってモデル化されます。 <xref:System.ServiceModel.ServiceHost> クラスを開くと、サービス コントラクトと実装が構成情報に反映され、構成情報とマージされて、説明ツリーに挿入されます。  
  
 操作モデルには、*パラメーター*モデルと*メッセージコントラクト*モデルの2種類があります。 パラメーター モデルでは、<xref:System.ServiceModel.MessageContractAttribute?displayProperty=nameWithType> クラスによってマークされたパラメーターまたは戻り値の型を持たないマネージド メソッドを使用します。 このモデルでは、開発者がパラメーターと戻り値のシリアル化を制御しますが、WCF によって、サービスとそのコントラクトの説明ツリーの設定に使用される値が生成されます。  
  
 構成ファイルで指定されたバインディングは、<xref:System.ServiceModel.Description.ServiceEndpoint.Binding%2A?displayProperty=nameWithType> プロパティに直接読み込まれます。  
  
|ServiceBehaviorAttribute プロパティ|影響を受ける説明ツリーの値|  
|---------------------------------------|-------------------------------------|  
|名前|<xref:System.ServiceModel.Description.ServiceDescription.Name%2A>|  
|名前空間|<xref:System.ServiceModel.Description.ServiceDescription.Namespace%2A>|  
|ConfigurationName|<xref:System.ServiceModel.Description.ServiceDescription.ConfigurationName%2A>|  
|IgnoreExtensionDataObject|すべての操作の <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.IgnoreExtensionDataObject%2A> プロパティを設定します。|  
|MaxItemsInObjectGraph|すべての操作の <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.MaxItemsInObjectGraph%2A> プロパティを設定します。|  
  
|ServiceContractAttribute プロパティ|影響を受ける説明ツリーの値|  
|---------------------------------------|-------------------------------------|  
|CallbackContract|すべての操作の <xref:System.ServiceModel.Description.ContractDescription.CallbackContractType%2A> に追加される <xref:System.ServiceModel.Description.MessageDescription>、<xref:System.ServiceModel.Description.OperationDescription.Messages%2A>|  
|ConfigurationName|<xref:System.ServiceModel.Description.ContractDescription.ConfigurationName%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.ContractDescription.ProtectionLevel%2A> と、場合によっては子の保護レベル。 保護レベルの階層の詳細については、「[保護レベル](../understanding-protection-level.md)について」を参照してください。|  
|SessionMode|<xref:System.ServiceModel.Description.ContractDescription.SessionMode%2A>|  
  
|ServiceKnownTypesAttribute 値|影響を受ける説明ツリーの値|  
|--------------------------------------|-------------------------------------|  
|MethodName|<xref:System.ServiceModel.Description.OperationDescription.KnownTypes%2A>|  
  
|OperationContractAttribute 値|影響を受ける説明ツリーの値|  
|--------------------------------------|-------------------------------------|  
|アクション|出力メッセージまたは入力メッセージの <xref:System.ServiceModel.Description.MessageDescription.Action%2A>。コントラクトまたはコールバック コントラクトによって異なります。|  
|AsyncPattern|true の場合は、<xref:System.ServiceModel.Description.OperationDescription.BeginMethod%2A> と <xref:System.ServiceModel.Description.OperationDescription.EndMethod%2A>|  
|IsOneWay|<xref:System.ServiceModel.Description.MessageDescription> の 1 つの <xref:System.ServiceModel.Description.OperationDescription.Messages%2A> にマップします。|  
|IsInitiating|<xref:System.ServiceModel.Description.OperationDescription.IsInitiating%2A>|  
|IsTerminating|<xref:System.ServiceModel.Description.OperationDescription.IsTerminating%2A>|  
|名前|<xref:System.ServiceModel.Description.OperationDescription.Name%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.OperationDescription.ProtectionLevel%2A> と、場合によっては子の保護レベル。 保護レベルの階層の詳細については、「[保護レベル](../understanding-protection-level.md)について」を参照してください。|  
|ReplyAction|出力メッセージまたは入力メッセージの <xref:System.ServiceModel.Description.MessageDescription.Action%2A>。コントラクトまたはコールバック コントラクトによって異なります。|  
  
|FaultContractAttribute 値|影響を受ける説明ツリーの値|  
|----------------------------------|-------------------------------------|  
|アクション|<xref:System.ServiceModel.Description.FaultDescription.Action%2A>。コントラクトまたはコールバック コントラクトによって異なります。|  
|DetailType|<xref:System.ServiceModel.Description.FaultDescription.DetailType%2A>|  
|名前|<xref:System.ServiceModel.Description.FaultDescription.Name%2A>|  
|名前空間|<xref:System.ServiceModel.Description.FaultDescription.Namespace%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.FaultDescription.ProtectionLevel%2A>|  
  
|DataContractFormatAttribute 値|影響を受ける説明ツリーの値|  
|---------------------------------------|-------------------------------------|  
|使用|操作の <xref:System.ServiceModel.DataContractFormatAttribute.Style%2A> に <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> 値が設定されます。|  
  
|XmlSerializerFormatAttribute 値|影響を受ける説明ツリーの値|  
|----------------------------------------|-------------------------------------|  
|スタイル|操作の <xref:System.ServiceModel.XmlSerializerFormatAttribute> に、この <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> プロパティが設定されます。|  
|使用|操作の <xref:System.ServiceModel.XmlSerializerFormatAttribute> に、<xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> が設定されます。|  
  
|TransactionFlowAttribute 値|影響を受ける説明ツリーの値|  
|------------------------------------|-------------------------------------|  
|TransactionFlowOption|<xref:System.ServiceModel.TransactionFlowAttribute> が <xref:System.ServiceModel.Description.OperationDescription.Behaviors%2A> プロパティに操作の動作として追加されます。|  
  
|MessageContractAttribute 値|影響を受ける説明ツリーの値|  
|------------------------------------|-------------------------------------|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessageDescription.ProtectionLevel%2A>|  
|WrapperName|<xref:System.ServiceModel.Description.MessageBodyDescription.WrapperName%2A>|  
|WrapperNamespace|<xref:System.ServiceModel.Description.MessageBodyDescription.WrapperNamespace%2A>|  
  
|MessageHeaderAttribute 値|影響を受ける説明ツリーの値|  
|----------------------------------|-------------------------------------|  
|Actor|<xref:System.ServiceModel.Description.MessageHeaderDescription.Actor%2A>の対応するヘッダー<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|MustUnderstand|<xref:System.ServiceModel.Description.MessageHeaderDescription.MustUnderstand%2A>の対応するヘッダー<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|名前|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A>の対応するヘッダー<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|名前空間|<xref:System.ServiceModel.Description.MessagePartDescription.Namespace%2A>の対応するヘッダー<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessagePartDescription.ProtectionLevel%2A>の対応するヘッダー<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
|リレー|<xref:System.ServiceModel.Description.MessageHeaderDescription.Relay%2A>の対応するヘッダー<xref:System.ServiceModel.Description.MessageDescription.Headers%2A>|  
  
|MessageBodyMemberAttribute 値|影響を受ける説明ツリーの値|  
|--------------------------------------|-------------------------------------|  
|名前|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A>の対応する部分<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
|名前空間|<xref:System.ServiceModel.Description.MessagePartDescription.Namespace%2A>の対応する部分<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
|Order|<xref:System.ServiceModel.Description.MessagePartDescription.Index%2A>の対応する部分<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessagePartDescription.ProtectionLevel%2A>の対応する部分<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
  
|MessageHeaderArrayAttribute 値|影響を受ける説明ツリーの値|  
|---------------------------------------|-------------------------------------|  
|Actor|<xref:System.ServiceModel.Description.MessageHeaderDescription.Actor%2A>|  
|MustUnderstand|<xref:System.ServiceModel.Description.MessageHeaderDescription.MustUnderstand%2A>|  
|名前|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A>|  
|名前空間|<xref:System.ServiceModel.Description.MessagePartDescription.Namespace%2A>|  
|ProtectionLevel|<xref:System.ServiceModel.Description.MessagePartDescription.ProtectionLevel%2A>|  
|リレー|<xref:System.ServiceModel.Description.MessageHeaderDescription.Relay%2A>|  
  
|MessagePropertyAttribute 値|影響を受ける説明ツリーの値|  
|------------------------------------|-------------------------------------|  
|名前|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A>|  
  
|MessageParameterAttribute 値|影響を受ける説明ツリーの値|  
|-------------------------------------|-------------------------------------|  
|名前|<xref:System.ServiceModel.Description.MessagePartDescription.Name%2A>の対応する部分<xref:System.ServiceModel.Description.MessageBodyDescription.Parts%2A>|  
  
 説明ツリーの値をメタデータに変換する方法の詳細については、「 [ServiceDescription と WSDL リファレンス](servicedescription-and-wsdl-reference.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ServiceDescription と WSDL 参照](servicedescription-and-wsdl-reference.md)
