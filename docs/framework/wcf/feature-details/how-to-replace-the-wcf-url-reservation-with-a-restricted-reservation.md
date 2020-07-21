---
title: '方法: WCF URL 予約を制限付きの予約に置き換える'
ms.date: 03/30/2017
ms.assetid: 2754d223-79fc-4e2b-a6ce-989889f2abfa
ms.openlocfilehash: 780a2c7fe240ed624ff106e8157661f8b76b32bd
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84202371"
---
# <a name="how-to-replace-the-wcf-url-reservation-with-a-restricted-reservation"></a>方法: WCF URL 予約を制限付きの予約に置き換える

URL 予約を使用すると、特定の URL または URL セットからメッセージを受信するユーザーを制限できます。 予約は、URL テンプレート、アクセス制御リスト (ACL)、およびフラグのセットで構成されます。 URL テンプレートは、予約の対象となる URL を定義します。 URL テンプレートの処理方法の詳細については、「[受信要求のルーティング](/windows/win32/http/routing-incoming-requests)」を参照してください。 ACL は、指定された URL からメッセージを受信できるユーザーまたはユーザー グループを制御します。 フラグは、その予約で、ユーザーまたはグループに URL を直接リッスンする権限を与えるか、リッスンを他のプロセスに委任する権限を与えるかを指定します。  
  
 既定のオペレーティングシステム構成の一部として、Windows Communication Foundation (WCF) は、ポート80のグローバルにアクセス可能な予約を作成して、すべてのユーザーが双方向通信にデュアル HTTP バインディングを使用するアプリケーションを実行できるようにします。 この予約の ACL はすべてのユーザー向けなので、管理者は URL または URL セットをリッスンする権限を明示的に許可または拒否することはできません。 このトピックでは、この予約を削除し、制限された ACL を使用する予約を再作成する方法について説明します。  
  
Windows Vista または Windows Server 2008 では、「」と入力すると、管理者特権でのコマンドプロンプトからすべての HTTP URL 予約を表示でき `netsh http show urlacl` ます。 WCF URL 予約の例を次に示します。

```
Reserved URL : http://+:80/Temporary_Listen_Addresses/  
        User: \Everyone  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;WD)  
```

 この予約は、WCF アプリケーションが双方向通信に HTTP デュアルバインドを使用するときに使用される URL テンプレートで構成されます。 このフォームの Url は、HTTP デュアルバインドを介して通信するときに wcf サービスが WCF クライアントにメッセージを返信するために使用されます。 すべてのユーザーに対して、URL をリッスンする権限が与えられていますが、リッスンを他のプロセスに委任する権限は与えられていません。 また、ACL は SSDL (Security Descriptor Definition Language) で記述されています。 SSDL の詳細については、「 [ssdl](/windows/win32/secauthz/security-descriptor-definition-language) 」を参照してください。  
  
## <a name="to-delete-the-wcf-url-reservation"></a>WCF URL 予約を削除するには  
  
1. [**スタート**] ボタンをクリックして [**すべてのプログラム**] をポイントし、[**アクセサリ**] をクリックします。 [**コマンドプロンプト**] を右クリックし、表示されるコンテキストメニューの [**管理者として実行**] をクリックします。 ユーザーアカウント制御 (UAC) ウィンドウで [**続行**] をクリックして、アクセス許可を続行するように指示します。  
  
2. `netsh http delete urlacl url=http://+:80/Temporary_Listen_Addresses/`コマンドプロンプトウィンドウで、「」と入力します。  
  
3. 予約が正常に削除されると、次のメッセージが表示されます。 **URL 予約を正常に削除しました**  
  
## <a name="creating-a-new-security-group-and-new-restricted-url-reservation"></a>新しいセキュリティ グループおよび新しい制限付き URL 予約の作成  
 WCF URL 予約を制限付き予約に置き換えるには、最初に新しいセキュリティグループを作成する必要があります。 この操作は、コマンド プロンプトを使用する方法か、コンピューターの管理コンソールを使用する方法で行うことができます。 行う必要があるのはいずれか一方のみです。  
  
### <a name="to-create-a-new-security-group-from-a-command-prompt"></a>コマンド プロンプトで新しいセキュリティ グループを作成するには  
  
1. [**スタート**] ボタンをクリックして [**すべてのプログラム**] をポイントし、[**アクセサリ**] をクリックします。 [**コマンドプロンプト**] を右クリックし、表示されるコンテキストメニューの [**管理者として実行**] をクリックします。 ユーザーアカウント制御 (UAC) ウィンドウで [**続行**] をクリックして、アクセス許可を続行するように指示します。  
  
2. `net localgroup "<security group name>" /comment:"<security group description>" /add`コマンドプロンプトで「」と入力します。 を **\<security group name>** 作成するセキュリティグループの名前に置き換え、 **\<security group description>** セキュリティグループに適切な説明を付けます。  
  
3. セキュリティ グループが正常に作成されると、次のメッセージが表示されます。 **コマンドは正常に完了しました。**  
  
### <a name="to-create-a-new-security-group-from-the-computer-management-console"></a>コンピューターの管理コンソールで新しいセキュリティ グループを作成するには  
  
1. [**スタート**]、[**コントロールパネル**]、[**管理ツール**]、[**コンピュータの管理**] の順にクリックして、コンピュータの管理コンソールを開きます。 ユーザーアカウント制御 (UAC) ウィンドウで [**続行**] をクリックして、アクセス許可を続行するように指示します。  
  
2. [**システムツール**]、[**ローカルユーザーとグループ**] の順にクリックし、[**グループ**] フォルダーを右クリックして、コンテキストメニューの [**新しいグループ**] をクリックします。 目的の**グループ名**、**説明**、およびこの新しいセキュリティグループのその他の詳細を入力し、[**作成**] ボタンをクリックしてセキュリティグループを作成します。  
  
### <a name="to-create-the-restricted-url-reservation"></a>制限付き URL 予約を作成するには  
  
1. [**スタート**] ボタンをクリックして [**すべてのプログラム**] をポイントし、[**アクセサリ**] をクリックします。 [**コマンドプロンプト**] を右クリックし、表示されるコンテキストメニューの [**管理者として実行**] をクリックします。 ユーザーアカウント制御 (UAC) ウィンドウで [**続行**] をクリックして、アクセス許可を続行するように指示します。  
  
2. `netsh http add urlacl url=http://+:80/Temporary_Listen_Addresses/ user="<machine name>\<security group name>`コマンドプロンプトで「」と入力します。 **\<machine name>** は、グループを作成する必要があるコンピューター名と、前に作成した **\<security group name>** セキュリティグループの名前に置き換えます。  
  
3. 予約が正常に作成されると、 **URL 予約が正常に追加されました**。
