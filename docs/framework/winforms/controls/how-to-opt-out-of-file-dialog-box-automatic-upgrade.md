---
title: '方法 : ファイル関連のダイアログ ボックスの自動アップグレードを無効にする'
ms.date: 03/30/2017
helpviewer_keywords:
- OpenFileDialog [Windows Forms], opt out of automatic upgrade
- file dialog box [Windows Forms], opt out of automatic upgrade
- Windows Vista file dialog box [Windows Forms], opt out of automatic upgrade
- SaveFileDialog [Windows Forms], opt out of automatic upgrade
- AutoUpgradeEnabled property
ms.assetid: 522e482e-cc01-48b1-8d59-9617dc2c4ac1
ms.openlocfilehash: bbde260cc7f05226c9b06325b45708e1cde3cf8c
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73976880"
---
# <a name="how-to-opt-out-of-file-dialog-box-automatic-upgrade"></a>方法 : ファイル関連のダイアログ ボックスの自動アップグレードを無効にする
<xref:System.Windows.Forms.OpenFileDialog> クラスと <xref:System.Windows.Forms.SaveFileDialog> クラスをアプリケーションで使用する場合、その外観と動作は、アプリケーションが実行されている Windows のバージョンによって異なります。 .NET Framework 2.0 以前で作成されたアプリケーションが Windows Vista に表示されると、<xref:System.Windows.Forms.OpenFileDialog> と <xref:System.Windows.Forms.SaveFileDialog> が Windows Vista の外観と動作で自動的に表示されます。 .NET Framework 3.0 以降では、自動アップグレードを無効にして、<xref:System.Windows.Forms.OpenFileDialog> と <xref:System.Windows.Forms.SaveFileDialog> を [!INCLUDE[winxp](../../../../includes/winxp-md.md)]スタイルの外観と動作によって表示することができます。  
  
### <a name="to-opt-out-of-file-dialog-box-automatic-upgrade"></a>ファイル関連のダイアログ ボックスの自動アップグレードを無効にするには  
  
1. ダイアログボックスを表示する前に、<xref:System.Windows.Forms.OpenFileDialog> または <xref:System.Windows.Forms.SaveFileDialog> の <xref:System.Windows.Forms.FileDialog.AutoUpgradeEnabled%2A> プロパティを `false` に設定します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.FileDialog>
