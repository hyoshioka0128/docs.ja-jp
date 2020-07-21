---
title: '方法: 一貫性を保って X.509 証明書を参照する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- certificates [WCF], referencing X.509 certificates
ms.assetid: a6de1c63-e450-4640-ad08-ad7302dbfbfc
ms.openlocfilehash: c13dd5ebb18df62ce64fc74da53f3f5a2e8cadb7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599088"
---
# <a name="how-to-consistently-reference-x509-certificates"></a>方法: 一貫性を保って X.509 証明書を参照する
証明書を識別する方法には、証明書のハッシュを使用する方法、発行者とシリアル番号を使用する方法、またはサブジェクト キー識別子 (SKI) を使用する方法があります。 SKI を使用すると、証明書のサブジェクト公開キーを一意に識別できます。SKI は、XML デジタル署名を処理する場合によく使用されます。 SKI 値は、通常、 *x.509 証明書拡張*として x.509 証明書の一部です。 Windows Communication Foundation (WCF) には、証明書に SKI 拡張機能がない場合に発行者とシリアル番号を使用する、既定の*参照スタイル*が設定されています。 証明書に SKI 拡張が含まれる場合、既定の参照スタイルは SKI を使用してその証明書を識別します。 アプリケーションの開発中に、SKI 拡張を使用しない証明書を使用して、SKI 拡張機能を使用する証明書に切り替えた場合、WCF によって生成されるメッセージで使用される参照スタイルも変更されます。  
  
 SKI 拡張が存在するかどうかに関係なく、一貫性のある参照スタイルが必要な場合は、次のコードに示されているような参照スタイルを構成できます。  
  
## <a name="example"></a>例  
 次の例では、1 つの一貫した参照スタイル (ユーザー名とシリアル番号) を使用するカスタム セキュリティ バインド要素を作成します。  
  
 [!code-csharp[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_referencingcertificatesconsistently/cs/source.cs#1)]
 [!code-vb[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_referencingcertificatesconsistently/vb/source.vb#1)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 コードのコンパイルには次の名前空間が必要です。  
  
- <xref:System>  
  
- <xref:System.ServiceModel>  
  
- <xref:System.ServiceModel.Channels>  
  
- <xref:System.ServiceModel.Security.Tokens>  
  
## <a name="see-also"></a>関連項目

- [証明書の使用](working-with-certificates.md)
