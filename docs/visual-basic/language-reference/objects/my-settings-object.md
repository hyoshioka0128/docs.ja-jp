---
title: My.Settings オブジェクト
ms.date: 07/20/2015
f1_keywords:
- My.MySettingsProperty.Settings
- My.Settings
helpviewer_keywords:
- My.Settings object
ms.assetid: 41f30dc1-202a-4273-b9b7-5728941f996c
ms.openlocfilehash: c905ff85c8e9729dd4d6068f0d34f729962bbb57
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84372402"
---
# <a name="mysettings-object"></a>My.Settings オブジェクト
アプリケーションの設定にアクセスするためのプロパティとメソッドを提供します。  
  
## <a name="remarks"></a>Remarks  
 `My.Settings` オブジェクトは、アプリケーションの設定へのアクセスを提供し、アプリケーションのプロパティ設定やその他の情報を動的に格納し、取得できるようにします。 詳細については、「[アプリケーションの設定の管理 (.NET)](/visualstudio/ide/managing-application-settings-dotnet)」を参照してください。  
  
## <a name="properties"></a>プロパティ  
 `My.Settings` オブジェクトのプロパティを使用すると、アプリケーションの設定にアクセスできます。 設定を追加または削除するには、**設定デザイナー**を使用します。  
  
 各設定には **[名前]** 、 **[型]** 、 **[スコープ]** 、および **[値]** が含まれ、これらの設定によって、各設定にアクセスするためのプロパティが `My.Settings` オブジェクトにどのように表示されるかが決まります。  
  
- **[名前]** は、プロパティの名前を決定します。  
  
- **[型]** は、プロパティの型を決定します。  
  
- **[スコープ]** は、プロパティが読み取り専用かどうかを示します。 値が **[アプリケーション]** の場合、プロパティは読み取り専用です。値が **[ユーザー]** の場合、プロパティは読み取り/書き込みです。  
  
- **[値]** はプロパティの既定値です。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|---|---|  
|`Reload`|最後に保存した値からユーザー設定を再度読み込みます。|  
|`Save`|現在のユーザー設定を保存します。|  
  
 `My.Settings` オブジェクトは、<xref:System.Configuration.ApplicationSettingsBase> クラスから継承された高度なプロパティやメソッドも提供します。  
  
## <a name="tasks"></a>タスク  
 次の表に、`My.Settings` オブジェクトに関連するタスクの例を示します。  
  
|終了|解決方法については、|  
|---|---|  
|アプリケーション設定を読み取る|[方法: Visual Basic でアプリケーション設定を読み取る](../../developing-apps/programming/app-settings/how-to-read-application-settings.md)|  
|ユーザー設定を変更する|[方法: Visual Basic でユーザー設定を変更する](../../developing-apps/programming/app-settings/how-to-change-user-settings.md)|  
|ユーザー設定を永続化する|[方法: Visual Basic でユーザー設定を永続化する](../../developing-apps/programming/app-settings/how-to-persist-user-settings.md)|  
|ユーザー設定のためのプロパティ グリッドを作成する|[方法: Visual Basic でユーザー設定のためのプロパティ グリッドを作成する](../../developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)|  
  
## <a name="example"></a>例  
 次の例は、`Nickname` の設定値を表示します。  
  
 [!code-vb[VbVbalrMyResources#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrMyResources/VB/Form1.vb#14)]  
  
 この例を実行するには、アプリケーションで `String` 型の `Nickname` を設定する必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Configuration.ApplicationSettingsBase>
- [方法: Visual Basic でアプリケーション設定を読み取る](../../developing-apps/programming/app-settings/how-to-read-application-settings.md)
- [方法: Visual Basic でユーザー設定を変更する](../../developing-apps/programming/app-settings/how-to-change-user-settings.md)
- [方法: Visual Basic でユーザー設定を永続化する](../../developing-apps/programming/app-settings/how-to-persist-user-settings.md)
- [方法: Visual Basic でユーザー設定のためのプロパティ グリッドを作成する](../../developing-apps/programming/app-settings/how-to-create-property-grids-for-user-settings.md)
- [アプリケーションの設定の管理 (.NET)](/visualstudio/ide/managing-application-settings-dotnet)
