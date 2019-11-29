---
title: Windows ストア アプリのネットワーク分離
ms.date: 03/30/2017
ms.assetid: b064497c-d956-46b8-838d-7a0223c7e200
ms.openlocfilehash: 34b8865781079f45a68d3dd1aab7fbd66c703d50
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74447421"
---
# <a name="network-isolation-for-windows-store-apps"></a>Windows ストア アプリのネットワーク分離
<xref:System.Net>、<xref:System.Net.Http>、<xref:System.Net.Http.Headers> の各名前空間のクラスは、Windows ストア アプリまたはデスクトップ アプリを開発するために使用できます。 Windows ストア アプリで使用する場合、これらの名前空間のクラスは、[!INCLUDE[win8](../../../includes/win8-md.md)]で使用されるアプリケーション セキュリティ モデルの一部であるネットワーク分離の影響を受けます。 システムでネットワーク アクセスが許可されるように、Windows ストア アプリのアプリ マニフェストで適切なネットワーク機能を有効にする必要があります。  
  
## <a name="checklist-for-network-isolation"></a>ネットワーク分離のチェックリスト  
 Windows ストア アプリに対してネットワークの分離が適切に構成されているかどうかを、このチェックリストを使って確認してください。  
  
1. アプリが必要とするネットワーク アクセス要求の方向を確認します。 これには、クライアント側から開始される送信要求と、受信側が送信を要求していない受信要求とがあります。両方の種類のネットワーク要求を組み合わせたものもあります。  
  
2. アプリの通信相手となるネットワーク リソースの種類を確認します。 アプリの通信相手は、ホーム ネットワークまたは職場ネットワーク上の信頼済みリソースである場合があります。 または、インターネット上のリソースと通信することが必要な場合があります。 その両方の種類のネットワーク リソースにアクセスする場合もあります。  
  
3. アプリ マニフェストで、必要最小限のネットワーク分離機能を構成します。  
  
4. アプリを展開して実行し、トラブルシューティングのためのネットワーク分離ツールを使用してテストします。  
  
 ネットワーク機能の構成と、ネットワーク分離のトラブルシューティングに使用する分離ツールの詳細については、Windows 8.x Store 開発者向けドキュメントで、[ネットワーク分離の機能を構成する方法](https://docs.microsoft.com/previous-versions/windows/apps/hh770532(v=win.10))に関するページを参照してください。
  
## <a name="see-also"></a>関連項目

- [Web サービスへの接続](https://docs.microsoft.com/previous-versions/windows/apps/hh761504(v=win.10))
- [ネットワーク分離のガイドラインとチェックリスト](https://docs.microsoft.com/previous-versions/windows/apps/hh770532(v=win.10))
- [クイック スタート:HttpClient を使って接続する](https://docs.microsoft.com/previous-versions/windows/apps/hh781239(v=win.10))
- [HttpClient ハンドラーを使う方法](https://docs.microsoft.com/previous-versions/windows/apps/hh781241(v=win.10))
- [HttpClient の接続をセキュリティで保護する方法](https://docs.microsoft.com/previous-versions/windows/apps/hh781240(v=win.10))
- [HttpClient のサンプル](https://code.msdn.microsoft.com/windowsapps/HttpClient-sample-55700664)
