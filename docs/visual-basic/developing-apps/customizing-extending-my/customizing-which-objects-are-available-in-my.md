---
title: My で利用可能なオブジェクトのカスタマイズ (Visual Basic)
ms.date: 07/20/2015
helpviewer_keywords:
- My namespace [Visual Basic], customizing
- My namespace
ms.assetid: 4e8279c2-ed5b-4681-8903-8a6671874000
ms.openlocfilehash: caddad463f7c525c8b715d70f49bf8bebcc7cfbd
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701265"
---
# <a name="customizing-which-objects-are-available-in-my-visual-basic"></a>My で利用可能なオブジェクトのカスタマイズ (Visual Basic)

このトピックでは、プロジェクトの @no__t 1 つの条件付きコンパイル定数を設定することによって、有効にする @no__t 0 オブジェクトを制御する方法について説明します。 Visual Studio 統合開発環境 (IDE) では、プロジェクトの種類と同期しているプロジェクトに対して、@no__t 0 の条件付きコンパイル定数が保持されます。  
  
## <a name="predefined-_mytype-values"></a>定義済みの @no__t 0MYTYPE 値  

@No__t-0 コンパイラオプションを使用して、`_MYTYPE` の条件付きコンパイル定数を設定する必要があります。 @No__t 0 定数に独自の値を指定する場合は、文字列値を円記号/引用符 (\\ ") のシーケンスで囲む必要があります。 たとえば、次のように使用できます。  
  
```console  
/define:_MYTYPE=\"WindowsForms\"  
```  
  
 次の表は、いくつかのプロジェクトの種類に対して、@no__t 0 の条件付きコンパイル定数がどのように設定されているかを示しています。  
  
|プロジェクトの種類|@no__t 0MYTYPE 値|  
|------------------|--------------------|  
|クラス ライブラリ|ウィンドウ|  
|コンソール アプリケーション|コンソール|  
|Web|Www|  
|Web コントロールライブラリ|WebControl|  
|Windows アプリケーション|WindowsForms|  
|Windows アプリケーション (カスタム @no__t で開始する場合)-0|"Windowsフォーム Withcustomsubmain"|  
|Windows コントロールライブラリ|ウィンドウ|  
|Windows サービス|コンソール|  
|Empty|指定|  
  
> [!NOTE]
> @No__t-0 ステートメントの設定方法に関係なく、すべての条件付きコンパイル文字列の比較では大文字と小文字が区別されます。  
  
## <a name="dependent-_my-compilation-constants"></a>依存 \_MY コンパイル定数  

さらに、@no__t 0 の条件付きコンパイル定数は、他のいくつかの `_MY` コンパイル定数の値を制御します。  
  
|\_MYTYPE|\_MYAPPLICATIONTYPE|\_MYCOMPUTERTYPE|\_MYFORMS|\_MYUSERTYPE|\_MYWEBSERVICES 場合|  
|--------------|-------------------------|----------------------|---------------|------------------|---------------------|  
|コンソール|コンソール|ウィンドウ|未定義。|ウィンドウ|true|  
|ショー|未定義。|未定義。|未定義。|未定義。|未定義。|  
|指定|未定義。|未定義。|未定義。|未定義。|未定義。|  
|Www|未定義。|Www|false|Www|false|  
|WebControl|未定義。|Www|false|Www|true|  
|"Windows" または ""|ウィンドウ|ウィンドウ|未定義。|ウィンドウ|true|  
|WindowsForms|WindowsForms|ウィンドウ|true|ウィンドウ|true|  
|"Windowsフォーム Withcustomsubmain"|コンソール|ウィンドウ|true|ウィンドウ|true|  
  
 既定では、未定義の条件付きコンパイル定数は `FALSE` に解決されます。 プロジェクトをコンパイルするときに、未定義の定数の値を指定して、既定の動作をオーバーライドできます。  
  
> [!NOTE]
> @No__t-0 が "Custom" に設定されている場合、プロジェクトには `My` の名前空間が含まれますが、オブジェクトは含まれません。 ただし、`_MYTYPE` を "Empty" に設定すると、コンパイラで `My` の名前空間とそのオブジェクトを追加できなくなります。  
  
 次の表では、`_MY` コンパイル定数の定義済みの値の影響について説明します。  
  
|定数|説明|  
|--------------|-------------|  
|`_MYAPPLICATIONTYPE`|定数が "Console"、"Windows"、または "WindowsForms" の場合、`My.Application` を有効にします。<br /><br /> -"Console" バージョンは <xref:Microsoft.VisualBasic.ApplicationServices.ConsoleApplicationBase> から派生します。 とには、"Windows" バージョンよりも少数のメンバーがあります。<br />-"Windows" のバージョンは @no__t 横-0 から派生し、"WindowsForms" バージョンよりも少数のメンバーを持ちます。<br />-@No__t-0 の "WindowsForms" バージョンは <xref:Microsoft.VisualBasic.ApplicationServices.WindowsFormsApplicationBase> から派生します。 @No__t 0 の定数が "winexe" に定義されている場合、クラスには `Sub Main` メソッドが含まれます。|  
|`_MYCOMPUTERTYPE`|定数が "Web" または "Windows" の場合、`My.Computer` を有効にします。<br /><br /> -"Web" バージョンは <xref:Microsoft.VisualBasic.Devices.ServerComputer> から派生し、"Windows" バージョンよりも少数のメンバーを持ちます。<br />-"Windows" バージョンの `My.Computer` は <xref:Microsoft.VisualBasic.Devices.Computer> から派生します。|  
|`_MYFORMS`|定数が-1 @no__t の場合、`My.Forms` を有効にします。|  
|`_MYUSERTYPE`|定数が "Web" または "Windows" の場合、`My.User` を有効にします。<br /><br /> -@No__t-0 の "Web" バージョンは、現在の HTTP 要求のユーザー id に関連付けられています。<br />-"Windows" バージョンの `My.User` は、スレッドの現在のプリンシパルに関連付けられています。|  
|`_MYWEBSERVICES`|定数が-1 @no__t の場合、`My.WebServices` を有効にします。|  
|`_MYTYPE`|定数が "Web" の場合、`My.Log`、`My.Request`、および `My.Response` を有効にします。|  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.Logging.Log>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [プロジェクトの種類に応じた My の機能](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)
- [条件付きコンパイル](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)
- [/define (Visual Basic)](../../../visual-basic/reference/command-line-compiler/define.md)
- [My.Forms オブジェクト](../../../visual-basic/language-reference/objects/my-forms-object.md)
- [My.Request オブジェクト](../../../visual-basic/language-reference/objects/my-request-object.md)
- [My.Response オブジェクト](../../../visual-basic/language-reference/objects/my-response-object.md)
- [My.WebServices オブジェクト](../../../visual-basic/language-reference/objects/my-webservices-object.md)
