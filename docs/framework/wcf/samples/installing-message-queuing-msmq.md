---
title: メッセージ キュー (MSMQ) のインストール
description: 1回限りのセットアップ手順の一部として、WFC サンプルで使用するメッセージキュー4.0 とメッセージキュー3.0 をインストールする方法について説明します。
ms.date: 03/30/2017
ms.assetid: 7ddcd497-3e04-427e-bc04-3610ad98b01e
ms.openlocfilehash: 0d0cb87b40b1cb11eb7692c2fa1e890ec815b13d
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244466"
---
# <a name="installing-message-queuing-msmq"></a>メッセージ キュー (MSMQ) のインストール
メッセージ キュー 4.0 およびメッセージ キュー 3.0 をインストールする方法を次の手順に示します。  
  
> [!NOTE]
> Windows XP および Windows Server 2003 では、メッセージキュー4.0 は使用できません。  
  
#### <a name="to-install-message-queuing-40-on-windows-server-2008-or-windows-server-2008-r2"></a>Windows Server 2008 または Windows Server 2008 R2 にメッセージ キュー 4.0 をインストールするには  
  
1. サーバーマネージャーで、[**機能**] をクリックします。  
  
2. 右側のウィンドウの [機能の**概要**] で、[**機能の追加**] をクリックします。  
  
3. 結果のウィンドウで、[**メッセージキュー**] を展開します。  
  
4. [**メッセージキューサービス**] を展開します。  
  
5. [**ディレクトリサービスの統合**] (ドメインに参加しているコンピューターの場合) をクリックし、[ **HTTP サポート**] をクリックします。  
  
6. [**次へ**] をクリックし、[**インストール**] をクリックします。  
  
#### <a name="to-install-message-queuing-40-on-windows-7-or-windows-vista"></a>Windows 7 または Windows Vista にメッセージ キュー 4.0 をインストールするには  
  
1. **[コントロール パネル]** を開きます。  
  
2. [**プログラム**] をクリックし、[**プログラムと機能**] で [ **Windows の機能の有効化または無効化**] をクリックします。  
  
3. [Microsoft Message Queue (MSMQ) Server]、[Microsoft Message Queue (MSMQ) Server Core] の順に展開して、インストールする次のメッセージ キュー機能のチェック ボックスをオンにします。  
  
    - [MSMQ Active Directory Domain Services Integration] (ドメインに参加するコンピューターの場合)  
  
    - [MSMQ HTTP サポート]  
  
4. **[OK]** をクリックします。  
  
5. コンピューターの再起動を求めるメッセージが表示されたら、[ **OK** ] をクリックしてインストールを完了します。  
  
#### <a name="to-install-message-queuing-30-on-windows-xp-and-windows-server-2003"></a>Windows XP および Windows Server 2003 にメッセージ キュー 3.0 をインストールするには  
  
1. **[コントロール パネル]** を開きます。  
  
2. [**プログラムの追加と削除**] をクリックし、[ **Windows コンポーネントの追加**] をクリックします。  
  
3. [メッセージキュー] を選択し、[**詳細**] をクリックします。  
  
    > [!NOTE]
    > Windows Server 2003 を実行している場合は、[アプリケーションサーバー] を選択してメッセージキューにアクセスします。  
  
4. 詳細ページで、[MSMQ HTTP サポート] オプションが選択されていることを確認します。  
  
5. [ **OK** ] をクリックして詳細ページを終了し、[**次へ**] をクリックします。 インストールを完了します。  
  
6. コンピューターの再起動を求めるメッセージが表示されたら、[ **OK** ] をクリックしてインストールを完了します。  
  
## <a name="see-also"></a>関連項目

- [セットアップ手順](set-up-instructions.md)
