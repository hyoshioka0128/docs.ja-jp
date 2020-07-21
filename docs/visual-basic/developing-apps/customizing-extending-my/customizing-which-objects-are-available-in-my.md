---
title: My で利用可能なオブジェクトのカスタマイズ
ms.date: 07/20/2015
helpviewer_keywords:
- My namespace [Visual Basic], customizing
- My namespace
ms.assetid: 4e8279c2-ed5b-4681-8903-8a6671874000
ms.openlocfilehash: 5245c129281bc8c7c1c6fe9215a221889380a901
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410219"
---
# <a name="customizing-which-objects-are-available-in-my-visual-basic"></a>My で利用可能なオブジェクトのカスタマイズ (Visual Basic)

このトピックでは、プロジェクトの `_MYTYPE` 条件付きコンパイル定数を設定して、どの `My` オブジェクトを有効にするかを制御する方法について説明します。 Visual Studio 統合開発環境 (IDE) では、プロジェクトに対して、プロジェクト タイプと同期して、`_MYTYPE` 条件付きコンパイル定数が保持されます。  
  
## <a name="predefined-_mytype-values"></a>定義済みの \_MYTYPE 値  

`_MYTYPE` 条件付きコンパイル定数を設定するには、`/define` コンパイラ オプションを使用する必要があります。 `_MYTYPE` 定数に独自の値を指定する場合は、文字列値をバックスラッシュと引用符のシーケンス (\\") で囲む必要があります。 たとえば、次のように使用できます。  
  
```console  
/define:_MYTYPE=\"WindowsForms\"  
```  
  
 次の表は、いくつかのプロジェクト タイプに対して `_MYTYPE` 条件付きコンパイル定数を何に設定するかを示しています。  
  
|プロジェクトの種類|\_MYTYPE 値|  
|------------------|--------------------|  
|クラス ライブラリ|"Windows"|  
|コンソール アプリケーション|"Console"|  
|Web|"Web"|  
|Web コントロール ライブラリ|"WebControl"|  
|Windows アプリケーション|"WindowsForms"|  
|Windows アプリケーション (カスタム `Sub Main` を使って起動する場合)|"WindowsFormsWithCustomSubMain"|  
|Windows コントロール ライブラリ|"Windows"|  
|Windows サービス|"Console"|  
|空|"Empty"|  
  
> [!NOTE]
> すべての条件付きコンパイル文字列の比較では、`Option Compare` ステートメントの設定方法に関係なく、大文字と小文字が区別されます。  
  
## <a name="dependent-_my-compilation-constants"></a>依存型の \_MY コンパイル定数  

さらに、`_MYTYPE` 条件付きコンパイル定数を使用して、他のいくつかの `_MY` コンパイル定数の値を制御します。  
  
|\_MYTYPE|\_MYAPPLICATIONTYPE|\_MYCOMPUTERTYPE|\_MYFORMS|\_MYUSERTYPE|\_MYWEBSERVICES|  
|--------------|-------------------------|----------------------|---------------|------------------|---------------------|  
|"Console"|"Console"|"Windows"|未定義|"Windows"|true|  
|"Custom"|未定義|未定義|未定義|未定義|未定義|  
|"Empty"|未定義|未定義|未定義|未定義|未定義|  
|"Web"|未定義|"Web"|false|"Web"|false|  
|"WebControl"|未定義|"Web"|false|"Web"|true|  
|"Windows" または ""|"Windows"|"Windows"|未定義|"Windows"|true|  
|"WindowsForms"|"WindowsForms"|"Windows"|true|"Windows"|true|  
|"WindowsFormsWithCustomSubMain"|"Console"|"Windows"|true|"Windows"|true|  
  
 既定では、未定義の条件付きコンパイル定数は `FALSE` に解決されます。 プロジェクトのコンパイル時に未定義の定数に値を指定して、既定の動作をオーバーライドできます。  
  
> [!NOTE]
> `_MYTYPE` を "Custom" に設定すると、プロジェクトには `My` 名前空間が含まれ、オブジェクトは含まれません。 一方、`_MYTYPE` を "Empty" に設定すると、コンパイラで `My` 名前空間とそのオブジェクトを追加できなくなります。  
  
 次の表は、`_MY` コンパイル定数の定義済みの値の影響を示しています。  
  
|定数|説明|  
|--------------|-------------|  
|`_MYAPPLICATIONTYPE`|定数が "Console"、"Windows"、または "WindowsForms" の場合、`My.Application` を有効にします。<br /><br /> - "Console" バージョンは、<xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase> から派生します。 "Windows" バージョンよりも少ないメンバーが含まれます。<br />- "Windows" バージョンは、<xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase> から派生します。"WindowsForms" バージョンよりも少ないメンバーが含まれます。<br />- "WindowsForms" バージョンの `My.Application` は、<xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> から派生します。 `TARGET` 定数が "winexe" に定義されている場合、クラスには `Sub Main` メソッドが含まれます。|  
|`_MYCOMPUTERTYPE`|定数が "Web" または "Windows" の場合、`My.Computer` を有効にします。<br /><br /> - "Web" バージョンは、<xref:Microsoft.VisualBasic.Devices.ServerComputer> から派生し、"Windows" バージョンよりも少ないメンバーが含まれます。<br />- "Windows" バージョンの`My.Computer` は、<xref:Microsoft.VisualBasic.Devices.Computer> から派生します。|  
|`_MYFORMS`|定数が `TRUE` の場合、`My.Forms` を有効にします。|  
|`_MYUSERTYPE`|定数が "Web" または "Windows" の場合、`My.User` を有効にします。<br /><br /> - "Web" バージョンの `My.User` は、現在の HTTP 要求のユーザー ID に関連付けられます。<br />- "Windows" バージョンの `My.User` は、スレッドの現在のプリンシパルに関連付けられます。|  
|`_MYWEBSERVICES`|定数が `TRUE` の場合、`My.WebServices` を有効にします。|  
|`_MYTYPE`|定数が "Web" の場合、`My.Log`、`My.Request`、`My.Response` を有効にします。|  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.Logging.Log>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [プロジェクトの種類に応じた My の機能](../development-with-my/how-my-depends-on-project-type.md)
- [条件付きコンパイル](../../programming-guide/program-structure/conditional-compilation.md)
- [-define (Visual Basic)](../../reference/command-line-compiler/define.md)
- [My.Forms オブジェクト](../../language-reference/objects/my-forms-object.md)
- [My.Request オブジェクト](../../language-reference/objects/my-request-object.md)
- [My.Response オブジェクト](../../language-reference/objects/my-response-object.md)
- [My.WebServices オブジェクト](../../language-reference/objects/my-webservices-object.md)
