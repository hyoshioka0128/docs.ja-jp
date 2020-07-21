---
title: Windows Communication Foundation バインディング
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], bindings
- Windows Communication Foundation [WCF], bindings
- bindings [WCF]
ms.assetid: 83639133-89f7-43f0-b4ef-8d9e57c08d25
ms.openlocfilehash: fd6b942dcabad07feda81af63bde23d3b663ce0f
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84587613"
---
# <a name="windows-communication-foundation-bindings"></a>Windows Communication Foundation バインディング
Windows Communication Foundation (WCF) は、アプリケーション用のソフトウェアが他のソフトウェアと通信する方法からどのように記述されるかを分離します。 バインディングを使用して、クライアントとサービスが相互に通信するために必要なトランスポート、エンコーディング、およびプロトコルの詳細を指定します。 WCF はバインディングを使用してエンドポイントの基になるワイヤ表現を生成するため、バインディングの詳細のほとんどは、通信しているパーティによって合意されている必要があります。 これを実現する最も簡単な方法は、サービスのクライアントがサービスのエンドポイントと同じバインディングを使用することです。 これを行う方法の詳細については、「バインドを使用した[サービスとクライアントの構成](../using-bindings-to-configure-services-and-clients.md)」を参照してください。  
  
 バインディングは、バインド要素のコレクションで構成されます。 各要素は、エンドポイントがクライアントと通信する方法の一部分を記述します。 バインディングには、1 つ以上のトランスポート バインド要素、1 つ以上のメッセージ エンコーディング バインド要素 (既定では、トランスポート バインド要素によって提供されます)、および任意の数の他のプロトコル バインド要素が含まれている必要があります。 このように、ランタイムをビルドするプロセスでは、各バインド要素からランタイムにコードを提供できます。  
  
 WCF には、バインド要素の共通選択を含むバインディングが用意されています。 これらのバインディングは、既定の設定で使用することも、ユーザーの要件に応じて既定値を変更することもできます。 これらのシステム指定のバインディングには、バインド要素およびその設定を直接制御できるプロパティが含まれます。 また、バインディングの各バージョンに独自の名前を付けることで、複数のバージョンを同時に使用することもできます。 詳細については、「[システム指定のバインディングの構成](configuring-system-provided-bindings.md)」を参照してください。  
  
 システム指定のバインディングに用意されていないバインド要素のコレクションが必要になった場合には、その必要なバインド要素のコレクションで構成されるカスタム バインドを作成できます。 このようなカスタム バインドは簡単に作成でき、新しいクラスも必要ありませんが、バインド要素およびその設定を制御するためのプロパティは提供されません。 バインド要素へのアクセスと設定の変更は、バインド要素を含むコレクションを通じて行います。 詳細については、「[カスタムバインド](../extending/custom-bindings.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [システムが提供するバインディングの構成](configuring-system-provided-bindings.md)  
 一般的なシナリオをサポートするために WCF が提供するバインディングを使用および変更する方法について説明します。  
  
 [サービスとクライアントを構成するためのバインディングの使用](../using-bindings-to-configure-services-and-clients.md)  
 サービスとクライアントの Windows Communication Foundation (WCF) バインドをコード内で強制的に定義し、構成を使用して宣言する方法について説明します。  
  
 [カスタム バインディング](../extending/custom-bindings.md)  
 <xref:System.ServiceModel.Channels.CustomBinding> の概要と使用する状況について説明します。  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel.Channels.Binding>  
  
 <xref:System.ServiceModel.Channels.BindingElement>  
  
 <xref:System.ServiceModel.Channels.CustomBinding>  
  
## <a name="related-sections"></a>関連項目  
 [バインディングの拡張](../extending/extending-bindings.md)
