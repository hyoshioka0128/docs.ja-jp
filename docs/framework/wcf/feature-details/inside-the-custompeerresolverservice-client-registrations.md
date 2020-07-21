---
title: CustomPeerResolverService 内部:クライアント登録
ms.date: 03/30/2017
ms.assetid: 40236953-a916-4236-84a6-928859e1331a
ms.openlocfilehash: ce694408edbb40309d1750be49b8414ebcbce3f7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596839"
---
# <a name="inside-the-custompeerresolverservice-client-registrations"></a>CustomPeerResolverService 内部:クライアント登録
メッシュ内の各ノードは、`Register` 関数を介してエンドポイント情報をリゾルバー サービスに公開します。 リゾルバー サービスは、登録レコードとしてこの情報を保存します。 このレコードには、ノードの一意の識別子 (RegistrationID) およびエンドポイント情報 `(PeerNodeAddress) が格納されます。  
  
## <a name="stale-records-and-expiration-time"></a>古くなったレコードと有効期限  
 ノードがメッシュからの離脱時に `Unregister` 関数を呼び出し、それによってリゾルバー サービスで登録エントリが削除されるのが理想的ですが、 `Unregister` を呼び出す前に、ノードがシャットダウンしたりアクセスできなくなったりするために、古い登録レコードが残ることがあります。  
  
 リゾルバー サービス内の古くなったレコードは、接続障害の原因となる場合があります。 メッシュへの接続時に、ノードがリゾルバー サービスから古い接続情報を受け取った場合、メッシュへの参加に時間がかかることがあります。 古いレコードはメモリも消費します。 効率的なクリーンアップ処理がなければ、登録の保存に使用したキャッシュがオーバーフローしてリゾルバー サービスがクラッシュする可能性があります。  
  
 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> は、各レコードを有効期限 (DateTime) でマークし、レコードの一部としてその情報を保存します。 サービスは、有効期限を使用してレコードを識別します。 カスタム実装でも同様な処理が必要です。  
  
## <a name="refreshinterval-and-cleanupinterval"></a>RefreshInterval および CleanupInterval  
 `RefreshInterval` の <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> プロパティは、サービスの登録ルックアップ テーブルで登録レコードが有効である期間を定義します。 特定のレコードについて、このプロパティで指定された時間が経過すると、そのレコードは古くなり、削除対象としてマークされます。  
  
 `CleanupInterval` の <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> プロパティは、古くなったレコードの検索と削除の頻度をサービスに指示します。 `CleanupInterval` は、サービスに設定されている `RefreshInterval` 以上の時間に設定する必要があります。  
  
 独自のリゾルバー サービスを実装するためには、古い登録レコードを削除するメンテナンス関数を作成する必要があります。 これにはいくつかの方法があります。  
  
- **定期的なメンテナンス**: タイマーが定期的にオフになるように設定し、データストアを使用して古いレコードを削除します。 <xref:System.ServiceModel.PeerResolvers.CustomPeerResolverService> では、この方法を使用します。  
  
- **パッシブな削除**: 古いレコードを定期的に検索するのではなく、サービスが既に別の機能を実行している場合は、古いレコードを特定して削除できます。 この方法では、リゾルバー クライアントからの要求に対する応答時間が遅くなる可能性がありますが、タイマーの必要がなくなるほか、一部のノードが `Unregister` を呼び出さずに離脱することが予想される場合には効果的です。  
  
## <a name="registrationlifetime-and-refresh"></a>RegistrationLifetime および Refresh  
 リゾルバー サービスに登録されると、ノードはサービスから <xref:System.ServiceModel.PeerResolvers.RegisterResponseInfo> オブジェクトを受け取ります。 このオブジェクトには、`RegistrationLifetime` プロパティが含まれます。このプロパティは、登録の期限が切れてリゾルバー サービスによって削除されるまでに、どれだけの時間があるかを示します。 たとえば、`RegistrationLifetime` が 2 分である場合、レコードが古くならず、削除されないようにするためには、ノードは 2 分以内に `Refresh` を呼び出す必要があります。 リゾルバー サービスは `Refresh` 要求を受け取ると、レコードを検索し、有効期限をリセットします。 Refresh は、<xref:System.ServiceModel.PeerResolvers.RefreshResponseInfo> プロパティのある `RegistrationLifetime` オブジェクトを返します。  
  
## <a name="see-also"></a>関連項目

- [ピア リゾルバー](peer-resolvers.md)
