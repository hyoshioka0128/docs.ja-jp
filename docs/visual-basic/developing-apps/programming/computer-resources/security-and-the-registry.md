---
title: セキュリティとレジストリ
ms.date: 07/20/2015
helpviewer_keywords:
- security [Visual Basic], registry
- registry [Visual Basic], security issues
ms.assetid: 9980aff7-2f69-492b-8f66-29a9a76d3df5
ms.openlocfilehash: 2eba9d177769b22de3f931bc7af4905a80e316b5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84359969"
---
# <a name="security-and-the-registry-visual-basic"></a>セキュリティとレジストリ (Visual Basic)

ここでは、レジストリにデータを格納するときのセキュリティへの影響について説明します。  
  
## <a name="permissions"></a>アクセス許可  

 レジストリ キーがアクセス制御リスト (ACL) によって保護されていても、パスワードなど他人に知られたくないデータをプレーン テキストでレジストリに格納するのは危険です。  
  
 レジストリを操作すると、システム リソースや保護情報への不適切なアクセスが許可され、セキュリティが損なわれる場合があります。 これらのプロパティを使うには、<xref:System.Security.Permissions.RegistryPermissionAccess> 列挙型の読み書きアクセス許可が必要です。これは、レジストリ変数へのアクセスを制御します。 完全な信頼で実行されるコード (既定のセキュリティ ポリシーでは、これはユーザーのローカル ハード ディスクにインストールされているコードです) は、レジストリにアクセスするために必要なアクセス許可を持っています。 詳細については、<xref:System.Security.Permissions.RegistryPermission> クラスを参照してください。  
  
 レジストリ変数は、<xref:System.Security.Permissions.RegistryPermission> を持たないコードがアクセスできるメモリの場所には格納しないようにする必要があります。 同様に、アクセス許可を付与するときは、ジョブの実行に必要な最低限の特権を付与します。  
  
 レジストリ アクセス許可のアクセス値は <xref:System.Security.Permissions.RegistryPermissionAccess> 列挙型により定義されます。 次の表はそのメンバーの詳細です。  
  
|値|レジストリ変数へのアクセス|  
|-----------|----------------------------------|  
|`AllAccess`|作成、読み取り、書き込み|  
|`Create`|作成|  
|`NoAccess`|アクセス権なし|  
|`Read`|Read|  
|`Write`|Write|  
  
## <a name="checking-values-in-registry-keys"></a>レジストリ キーの値のチェック  

 レジストリの値を作成するときは、その値が既存の値である場合の処理を決めておく必要があります。 悪意のあるユーザーによって作成された別のプロセスが既に値を作成し、アクセス権を持っている可能性があります。 レジストリ値にデータを設定すると、そのデータを他のプロセスから利用できるようになります。 これを回避するには、`GetValue` メソッドを使います。 このメソッドは、キーがまだ存在しない場合、`Nothing` を返します。  
  
> [!IMPORTANT]
> Web アプリケーションからレジストリを読み取るとき、現在のユーザーの ID は Web アプリケーションに実装されている認証と偽装によって決まります。  
  
## <a name="see-also"></a>参照

- <xref:Microsoft.VisualBasic.MyServices.RegistryProxy>
- [レジストリからの読み取りとレジストリへの書き込み](reading-from-and-writing-to-the-registry.md)
