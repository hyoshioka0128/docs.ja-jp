---
title: プリンシパル オブジェクトと ID オブジェクト
description: .NET のユーザーを表す id オブジェクトについて説明します。 また、ロール & id オブジェクトの両方をカプセル化するプリンシパルオブジェクトについても説明します。
ms.date: 03/30/2017
ms.technology: dotnet-standard
helpviewer_keywords:
- WindowsIdentity objects
- GenericIdentity objects
- GenericPrincipal objects
- identity objects, about identity objects
- security [.NET Framework], identity objects
- principal objects, about principal objects
- security [.NET Framework], principals
- WindowsPrincipal objects
ms.assetid: aa5930ad-f3d7-40aa-b6f6-c6edcd5c64f7
ms.openlocfilehash: 5fd3f1c80f22c1ebe7b2c10653ee137f00321de8
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768847"
---
# <a name="principal-and-identity-objects"></a>プリンシパル オブジェクトと ID オブジェクト
マネージコードでは、オブジェクト <xref:System.Security.Principal.IPrincipal> への参照を含むオブジェクトを使用して、プリンシパルの id またはロールを検出でき <xref:System.Security.Principal.IIdentity> ます。 ID オブジェクトとプリンシパル オブジェクトは、ユーザーとグループ アカウントのようななじみのある概念と比較するとわかりやすいでしょう。 ほとんどのネットワーク環境で、ユーザー アカウントは人またはプログラムを表し、グループ アカウントは特定のカテゴリのユーザーやそのユーザーが所有する権限を表します。 同様に、.NET Framework の ID オブジェクトはユーザーを表し、ロールはメンバーシップやセキュリティ コンテキストを表します。 .NET Framework で、プリンシパル オブジェクトは、ID オブジェクトとロールの両方をカプセル化します。 .NET Framework アプリケーションは、ID または一般的にはロール メンバーシップに基づいてプリンシパルに権限を付与します。  
  
## <a name="identity-objects"></a>ID オブジェクト  
 ID オブジェクトは、検証対象のユーザーまたはエンティティに関する情報をカプセル化します。 ID オブジェクトの最も基本的なレベルには名前と認証の種類が含まれます。 名前はユーザー名または Windows アカウント名、認証の種類は、サポートされるログオン プロトコル (Kerberos V5 など) かカスタム値になります。 .NET Framework は、 <xref:System.Security.Principal.GenericIdentity> ほとんどのカスタムログオンシナリオに使用できるオブジェクトと、 <xref:System.Security.Principal.WindowsIdentity> アプリケーションが Windows 認証に依存する場合に使用できる、より特殊なオブジェクトを定義します。 また、カスタム ユーザー情報をカプセル化する独自の ID クラスを定義することもできます。  
  
 インターフェイスは、 <xref:System.Security.Principal.IIdentity> 名前と認証の種類 (Kerberos V5 や NTLM など) にアクセスするためのプロパティを定義します。 すべての **Identity** クラスでは **IIdentity** インターフェイスが実装されます。 **ID** オブジェクトと、スレッドが現在実行している Windows NT プロセス トークンの間に関係は必要ありません。 ただし、**ID** オブジェクトが **WindowsIdentity** オブジェクトである場合、ID は Windows NT セキュリティ トークンを表すと見なされます。  
  
## <a name="principal-objects"></a>プリンシパル オブジェクト  
 プリンシパル オブジェクトは、コードが実行されているセキュリティ コンテキストを表します。 ロールベースのセキュリティを実装するアプリケーションは、プリンシパル オブジェクトに関連付けられたロールに基づいて権限を付与します。 Id オブジェクトと同様に、.NET Framework にはオブジェクトとオブジェクトが用意されて <xref:System.Security.Principal.GenericPrincipal> <xref:System.Security.Principal.WindowsPrincipal> います。 独自のカスタム プリンシパル クラスを定義することもできます。  
  
 インターフェイスは、 <xref:System.Security.Principal.IPrincipal> 関連付けられた**id**オブジェクトにアクセスするためのプロパティと、**プリンシパル**オブジェクトによって識別されるユーザーが特定のロールのメンバーであるかどうかを判断するためのメソッドを定義します。 すべての**プリンシパル** クラスは、**IPrincipal** インターフェイスの他に、必要なその他のプロパティとメソッドを実装しています。 たとえば、共通言語ランタイムでは **WindowsPrincipal** クラスが提供されますが、これは Windows NT または Windows 2000 グループ メンバーシップをロールにマッピングする追加機能を実装します。  
  
 **プリンシパル**オブジェクトは、 <xref:System.Runtime.Remoting.Messaging.CallContext> アプリケーションドメイン () 内の呼び出しコンテキスト () オブジェクトにバインドされ <xref:System.AppDomain> ます。 常に既定の呼び出しコンテキストはそれぞれ新しい **AppDomain** を使用して作成されるため、**プリンシパル** オブジェクトを受け入れる呼び出しコンテキストが常に存在します。 新しいスレッドが作成されるとき、そのスレッドの **CallContext** オブジェクトも作成されます。 **プリンシパル** オブジェクトの参照は、作成スレッドから新しいスレッドの **CallContext** に自動的にコピーされます。 スレッドの作成者に所属する**プリンシパル** オブジェクトをランタイムが判別できない場合は、**プリンシパル** オブジェクトと **ID** オブジェクトの作成で既定のポリシーに従います。  
  
 構成可能なアプリケーション ドメイン固有のポリシーによって、新しいアプリケーション ドメインに関連付ける**プリンシパル** オブジェクトの種類を決める規則が定義されます。 セキュリティ ポリシーによって許可される場合、ランタイムは、現在の実行スレッドに関連するオペレーティング システム トークンを反映する**プリンシパル** オブジェクトと **ID** オブジェクトを作成できます。 ランタイムは既定では、認証されていないユーザーを表す**プリンシパル** オブジェクトと **ID** オブジェクトを使用します。 このような既定の**プリンシパル** オブジェクトと **ID** オブジェクトは、コードがアクセスを試行するまでランタイムによって作成されることはありません。  
  
 信頼されるコードが、アプリケーション ドメインを作成して、アプリケーション ドメイン ポリシーを作成できます。このポリシーによって、既定の**プリンシパル** オブジェクトと **ID** オブジェクトのコンストラクトが制御されます。 このアプリケーション ドメイン固有ポリシーは、そのアプリケーション ドメインのすべての実行スレッドに適用されます。 アンマネージの信頼されたホストには、本質的にこのポリシーを設定する機能がありますが、このポリシーを設定するマネージコードには、 <xref:System.Security.Permissions.SecurityPermission?displayProperty=nameWithType> ドメインポリシーを制御するためのが必要です。  
  
 **プリンシパル** オブジェクトを同じプロセス内 (つまり同じコンピューター上の) アプリケーション ドメイン間で送信するとき、リモート処理インフラストラクチャが、呼び出し元のコンテキストに関連する**プリンシパル** オブジェクトへの参照を呼び出し先のコンテキストにコピーします。  
  
## <a name="see-also"></a>関連項目

- [方法: WindowsPrincipal プロジェクトを作成する](how-to-create-a-windowsprincipal-object.md)
- [方法: GenericPrincipal オブジェクトと GenericIdentity オブジェクトを作成する](how-to-create-genericprincipal-and-genericidentity-objects.md)
- [プリンシパル オブジェクトの置き換え](replacing-a-principal-object.md)
- [偽装と復帰](impersonating-and-reverting.md)
- [ロール ベースのセキュリティ](role-based-security.md)
- [セキュリティの基本概念](key-security-concepts.md)
