---
title: '方法: コントラクト インターフェイスを使用してサービスを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7b6803f6-d6f9-4cc2-9f1b-6f4c920475d5
ms.openlocfilehash: c7d4bce174790b97db6b95aa5d15af455f261f82
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597164"
---
# <a name="how-to-create-a-service-with-a-contract-interface"></a>方法: コントラクト インターフェイスを使用してサービスを作成する
Windows Communication Foundation (WCF) コントラクトを作成するには、インターフェイスを使用することをお勧めします。 このコントラクトでは、サービスが提供する操作にアクセスするために必要なメッセージのコレクションと構造を指定します。 このインターフェイスでは、インターフェイスに <xref:System.ServiceModel.ServiceContractAttribute> クラスを適用し、公開するメソッドに <xref:System.ServiceModel.OperationContractAttribute> クラスを適用して、入力と出力の種類を定義します。  
  
 サービスコントラクトの詳細については、「[サービスコントラクトの設計](../designing-service-contracts.md)」を参照してください。  
  
### <a name="creating-a-wcf-contract-with-an-interface"></a>インターフェイスを使用した WCF コントラクトの作成  
  
1. Visual Basic、C#、またはその他の共通言語ランタイム言語を使用して、新しいインターフェイスを作成します。  
  
2. インターフェイスに <xref:System.ServiceModel.ServiceContractAttribute> クラスを適用します。  
  
3. インターフェイスのメソッドを定義します。  
  
4. <xref:System.ServiceModel.OperationContractAttribute>パブリック WCF コントラクトの一部として公開する必要がある各メソッドにクラスを適用します。  
  
## <a name="example"></a>例  
 次のコード例は、サービス コントラクトを定義するインターフェイスを示しています。  
  
 [!code-csharp[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createcontractwithinterface/cs/source.cs#1)]
 [!code-vb[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_createcontractwithinterface/vb/source.vb#1)]  
  
 <xref:System.ServiceModel.OperationContractAttribute> クラスが適用されたメソッドは、既定で要求/応答メッセージ パターンを使用します。 このメッセージパターンの詳細については、「[方法: 要求/応答コントラクトを作成](how-to-create-a-request-reply-contract.md)する」を参照してください。 属性のプロパティを設定することにより、他のメッセージ パターンを作成および使用できるようになります。 その他の例については、「[方法: 一方向コントラクトを作成](how-to-create-a-one-way-contract.md)する」および「[方法: 双方向コントラクトを作成する](how-to-create-a-duplex-contract.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
