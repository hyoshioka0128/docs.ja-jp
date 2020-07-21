---
title: '方法: C# のアプリケーションに複数の設定セットを追加する'
description: Visual Studio を使用して、C# のアプリケーションに複数の Windows フォーム設定のセットを追加する方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- application settings [Windows Forms], multiple sets
- application settings [Windows Forms], C#
ms.assetid: 45007ac6-cf07-4be7-bc38-3f0ef962faf9
ms.openlocfilehash: 579374ff101758b3224bc122c46b891280ed2609
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173446"
---
# <a name="how-to-add-multiple-sets-of-settings-to-your-application-in-c"></a>方法: C でアプリケーションに複数の設定セットを追加する\#

場合によっては、アプリケーションに複数の設定セットを含めることが必要になることがあります。 たとえば、特定の設定グループが頻繁に変更されることが予想されるアプリケーションを開発する場合は、ファイルをすべて1つのファイルに分割して、他の設定が影響を受けないようにすることをお勧めします。 Visual Studio では、プロジェクトに複数の設定セットを追加できます。 その他の設定セットは、オブジェクトを使用してアクセスでき `Properties.Settings` ます。

## <a name="add-an-additional-set-of-settings"></a>追加の設定セットを追加する

1. Visual Studio で、[**プロジェクト**] メニューの [**新しい項目の追加**] をクリックします。

   **[新しい項目の追加]** ダイアログ ボックスが開きます。

2. [**新しい項目の追加**] ダイアログボックスで、[**設定ファイル**] を選択し、ファイルの名前を入力して [**追加**] をクリックし、ソリューションに新しい設定ファイルを追加します。

3. **ソリューションエクスプローラー**で、新しい設定ファイルを**Properties**フォルダーにドラッグします。 これにより、新しい設定をコードで使用できるようになります。

4. 他の設定ファイルと同様に、このファイルに設定を追加して使用します。 この設定のグループには、オブジェクトを介してアクセスでき `Properties.Settings` ます。

## <a name="see-also"></a>関連項目

- [アプリケーション設定とユーザー設定の使用](using-application-settings-and-user-settings.md)
- [アプリケーション設定の概要](application-settings-overview.md)
