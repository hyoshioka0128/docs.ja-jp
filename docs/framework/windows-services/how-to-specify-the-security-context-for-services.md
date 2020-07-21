---
title: '方法: サービスのセキュリティ コンテキストを指定する'
ms.date: 03/30/2017
helpviewer_keywords:
- Windows Service applications, security
- security [Visual Studio], contexts
- contexts, Visual Studio security
- security [Visual Studio], service applications
- ServiceProcessInstaller class, security context
- services, security
- ServiceInstaller class, security context
ms.assetid: 02187c7b-dbf2-45f2-96c2-e11010225a22
author: ghogen
ms.openlocfilehash: dd2a9c4485e151d4cb1c9d5ae3a95a69fcc416d4
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053578"
---
# <a name="how-to-specify-the-security-context-for-services"></a>方法: サービスのセキュリティ コンテキストを指定する
既定では、サービスはログインしているユーザーのセキュリティ コンテキストとは異なるセキュリティ コンテキストで実行します。 サービスは `LocalSystem` という名前の既定のシステム アカウントのコンテキストで実行し、このコンテキストはサービスに対してユーザーとは異なるシステム リソースへのアクセス特権を付与します。 この動作を変更し、サービスの実行が異なるユーザー アカウントで行われるように指定することができます。  
  
 サービスが実行しているプロセスの <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> プロパティを操作することで、セキュリティ コンテキストを設定します。 このプロパティでは、次の 4 種類のアカウントのいずれかに、サービスを設定できます。  
  
- `User`: システムは、サービスのインストール時に有効なユーザー名とパスワードの指定を要求し、ネットワーク上の 1 人のユーザーによって指定されたアカウントのコンテキストで実行します。  
  
- `LocalService`: ローカル コンピューター上で非特権ユーザーとして機能し、リモート サーバーに匿名の資格情報を提示するアカウントのコンテキストで実行します。  
  
- `LocalSystem`: 広範なローカル特権を提供し、リモート サーバーにコンピューターの資格情報を提示するアカウントのコンテキストで実行します。  
  
- `NetworkService`: ローカル コンピューター上で非特権ユーザーとして機能し、リモート サーバーにコンピューターの資格情報を提示するアカウントのコンテキストで実行します。  
  
 詳細については、<xref:System.ServiceProcess.ServiceAccount> 列挙型のページをご覧ください。  
  
### <a name="to-specify-the-security-context-for-a-service"></a>サービスのセキュリティ コンテキストを指定するには  
  
1. サービスの作成後、必要なインストーラーを追加します。 詳細については、[サービス アプリケーションにインストーラーを追加する](how-to-add-installers-to-your-service-application.md)」を参照してください。  
  
2. デザイナーで、`ProjectInstaller` クラスにアクセスし、対象となるサービスのサービス プロセス インストーラーをクリックします。  
  
    > [!NOTE]
    > すべてのサービス アプリケーションについて、`ProjectInstaller` クラスには少なくとも 2 つのインストール コンポーネントがあります。プロジェクト内のすべてのサービスに対するプロセスをインストールするものと、アプリケーションに含まれるサービスごとに 1 つのインストーラーです。 このインスタンスでは、<xref:System.ServiceProcess.ServiceProcessInstaller> を選びます。  
  
3. **[プロパティ]** ウィンドウで、<xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> を適切な値に設定します。  
  
## <a name="see-also"></a>関連項目

- [Windows サービス アプリケーションの概要](introduction-to-windows-service-applications.md)
- [方法: サービス アプリケーションにインストーラーを追加する](how-to-add-installers-to-your-service-application.md)
- [方法: Windows サービスを作成する](how-to-create-windows-services.md)
