---
title: '方法: 実行時にユーザー設定を C# で書き込む'
description: Save メソッドを呼び出して、アプリケーションセッション間で設定の変更を永続化することで、実行時に設定を C# で記述する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], run time
- application settings [Windows Forms], writing user settings
- application settings [Windows Forms], C#
ms.assetid: 9d061c7d-b33b-470f-a36d-edccb1d6f9a3
ms.openlocfilehash: 6154ff1b92d6c2d4c788299e59eb8f73e6b69c4b
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904326"
---
# <a name="how-to-write-user-settings-at-run-time-with-c"></a>方法: 実行時に C を使用してユーザー設定を書き込む\#

アプリケーション スコープの設定は読み取り専用であり、デザイン時、またはアプリケーション セッション間に .config ファイルを変更することによってのみ変更できます。 ただし、ユーザー スコープの設定は、プロパティ値を変更する場合と同様に、実行時に書き込むことができます。 新しい値は、アプリケーションのセッションの実行中に永続化します。 Save メソッドを呼び出すことによって、アプリケーション セッション間で、設定の変更を永続化することができます。  
  
## <a name="how-to-write-and-persist-user-settings-at-run-time-with-c"></a>方法: 実行時にユーザー設定を C で書き込み、永続化する\#
  
1. この設定にアクセスし、この例で示すように、新しい値を割り当てます。  
  
   ```csharp
   Properties.Settings.Default.myColor = Color.AliceBlue;  
   ```  
  
2. アプリケーション セッション間で、設定の変更を永続化する場合は、この例で示すように Save メソッドを呼び出します。  
  
    ```csharp
    Properties.Settings.Default.Save();  
    ```  
  
ユーザー設定は、ユーザーの非表示のローカル アプリケーション データ フォルダーのサブフォルダー内のファイルに保存されます。  
  
## <a name="see-also"></a>こちらもご覧ください

- [アプリケーション設定とユーザー設定の使用](using-application-settings-and-user-settings.md)
- [方法: 実行時に設定を C# で読み取る](how-to-read-settings-at-run-time-with-csharp.md)
- [アプリケーション設定の概要](application-settings-overview.md)
