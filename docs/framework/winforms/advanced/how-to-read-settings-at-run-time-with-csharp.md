---
title: '方法: 実行時に設定を C# で読み取る'
description: プロパティオブジェクトを使用して、C# を使用して、アプリケーションスコープの設定とユーザースコープ設定の両方を実行時に読み取る方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], reading
- application settings [Windows Forms], run time
- application settings [Windows Forms], C#
ms.assetid: dbe8bf09-5e1c-49da-9192-154033d7240b
ms.openlocfilehash: d784544e018bb693c501e35ea36fcae1946ef5eb
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84903354"
---
# <a name="how-to-read-settings-at-run-time-with-c"></a>方法: 実行時に C を使用して設定を読み取る\#

アプリケーション スコープの設定とユーザー スコープの設定は、どちらも実行時に Properties オブジェクトを使用して読み取ることができます。 Properties オブジェクトは、プロジェクトのすべての既定の設定を、定義されているプロジェクトの既定の名前空間にある default メンバーを介して公開します。  
  
## <a name="to-read-settings-at-run-time-with-c"></a>実行時に C を使用して設定を読み取るには\#
  
Properties.Settings.Default メンバーを介して適切な設定にアクセスします。 BackColor プロパティに `myColor` という名前の設定を割り当てる方法を次の例に示します。 この例を実行する前に、`myColor` という名前の `System.Drawing.Color` 型の設定を含む設定ファイルを作成しておく必要があります。 設定ファイルの作成の詳細については、「[方法: デザイン時に新しい設定を作成](how-to-create-a-new-setting-at-design-time.md)する」を参照してください。  
  
```csharp
this.BackColor = Properties.Settings.Default.myColor;  
```  
  
## <a name="see-also"></a>こちらもご覧ください

- [アプリケーション設定とユーザー設定の使用](using-application-settings-and-user-settings.md)
- [方法: 実行時にユーザー設定を C# で書き込む](how-to-write-user-settings-at-run-time-with-csharp.md)
- [アプリケーション設定の概要](application-settings-overview.md)
