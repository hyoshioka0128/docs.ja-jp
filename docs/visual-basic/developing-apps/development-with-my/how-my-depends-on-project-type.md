---
title: プロジェクトの種類に応じた My の機能
ms.date: 07/20/2015
helpviewer_keywords:
- _MYTYPE
ms.assetid: c188b38e-bd9d-4121-9983-41ea6a94d28e
ms.openlocfilehash: 740185d8030c09e8813bc7680b451f6326588593
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84411715"
---
# <a name="how-my-depends-on-project-type-visual-basic"></a>プロジェクトの種類に応じた My の機能 (Visual Basic)

`My` は、特定のプロジェクト タイプに必要なオブジェクトのみを公開します。 たとえば、`My.Forms` オブジェクトは Windows フォームアプリケーションで使用できますが、コンソール アプリケーションでは使用できません。 このトピックでは、さまざまなプロジェクト タイプで使用できる `My` オブジェクトについて説明します。  
  
## <a name="my-in-windows-applications-and-web-sites"></a>Windows アプリケーションおよび Web サイトの My  

 `My` は、現在のプロジェクト タイプで有用なオブジェクトのみを公開します。適用できないオブジェクトは公開されません。 たとえば、次の図は、Windows フォーム プロジェクトの `My` オブジェクト モデルを示しています。  
  
 ![Windows フォーム アプリケーションの My オブジェクト モデルを示す図。](./media/how-my-depends-on-project-type/my-object-model-windows-forms.png)  
  
 Web サイト プロジェクトでは、`My` は、Web 開発者に関連するオブジェクト (`My.Request` オブジェクトや `My.Response` オブジェクトなど) を公開しますが、関連のないオブジェクト (`My.Forms` オブジェクトなど) は公開しません。 次の図は、Web サイト プロジェクトの `My` オブジェクト モデルを示しています。  
  
 ![Web アプリケーションの My オブジェクト モデルを示す図。](./media/how-my-depends-on-project-type/my-object-model-web.png)  
  
## <a name="project-details"></a>プロジェクトの詳細  

 次の表は、8 種類のプロジェクトで既定により有効になっている `My` オブジェクト (Windows アプリケーション、クラス ライブラリ、コンソール アプリケーション、Windows コントロール ライブラリ、Web コントロール ライブラリ、Windows サービス、空、Web サイト) を示しています。  
  
 3 つのバージョンの `My.Application` オブジェクト、2 つのバージョンの `My.Computer` オブジェクト、2 つのバージョンの `My.User` オブジェクトがあります。これらのバージョンの詳細については、表の後の脚注で説明しています。  
  
|My オブジェクト|Windows アプリケーション|クラス ライブラリ|コンソール アプリケーション|Windows コントロール ライブラリ|Web コントロール ライブラリ|Windows サービス|空|Web サイト|  
|---|---|---|---|---|---|---|---|---|  
|`My.Application`|**はい** <sup>1</sup>|**はい** <sup>2</sup>|**はい** <sup>3</sup>|**はい** <sup>2</sup>|いいえ|**はい** <sup>3</sup>|いいえ|いいえ|  
|`My.Computer`|**はい** <sup>4</sup>|**はい** <sup>4</sup>|**はい** <sup>4</sup>|**はい** <sup>4</sup>|**はい** <sup>5</sup>|**はい** <sup>4</sup>|いいえ|**はい** <sup>5</sup>|  
|`My.Forms`|**はい**|いいえ|いいえ|**はい**|いいえ|いいえ|いいえ|いいえ|  
|`My.Log`|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|**はい**|  
|`My.Request`|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|**はい**|  
|`My.Resources`|**はい**|**はい**|**はい**|**はい**|**はい**|**はい**|いいえ|いいえ|  
|`My.Response`|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|いいえ|**はい**|  
|`My.Settings`|**はい**|**はい**|**はい**|**はい**|**はい**|**はい**|いいえ|いいえ|  
|`My.User`|**はい** <sup>6</sup>|**はい** <sup>6</sup>|**はい** <sup>6</sup>|**はい** <sup>6</sup>|**はい** <sup>7</sup>|**はい** <sup>6</sup>|いいえ|**はい** <sup>7</sup>|  
|`My.WebServices`|**はい**|**はい**|**はい**|**はい**|**はい**|**はい**|いいえ|いいえ|  
  
 <sup>1</sup> `My.Application` の Windows フォーム バージョン。 コンソール バージョン (注 3 を参照) から派生します。アプリケーションのウィンドウとやり取りするためのサポートが追加され、Visual Basic アプリケーション モデルを提供します。  
  
 <sup>2</sup> `My.Application` のライブラリ バージョン。 アプリケーションで必要とされる基本機能を提供します。アプリケーション ログへの書き込みおよびアプリケーション情報へのアクセスのためのメンバーを提供します。  
  
 <sup>3</sup> `My.Application` のコンソール バージョン。 ライブラリ バージョン (注 2 を参照) から派生し、アプリケーションのコマンドライン引数および ClickOnce 配置情報にアクセスするためのメンバーを追加します。  
  
 <sup>4</sup> `My.Computer` の Windows バージョン。 サーバー バージョン (注 5 を参照) から派生し、キーボード、画面、マウスなど、クライアント コンピューター上の有用なオブジェクトへのアクセスを提供します。  
  
 <sup>5</sup> `My.Computer` のサーバー バージョン。 コンピューターに関する基本情報 (名前など)、時計へのアクセスなどを提供します。  
  
 <sup>6</sup> `My.User` の Windows バージョン。 このオブジェクトは、スレッドの現在の ID に関連付けられます。  
  
 <sup>7</sup> `My.User` の Web バージョン。 このオブジェクトは、アプリケーションの現在の HTTP 要求のユーザー ID に関連付けられます。  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.ApplicationServices.ApplicationBase>
- <xref:Microsoft.VisualBasic.Devices.Computer>
- <xref:Microsoft.VisualBasic.Logging.Log>
- <xref:Microsoft.VisualBasic.ApplicationServices.User>
- [My で利用可能なオブジェクトのカスタマイズ](../customizing-extending-my/customizing-which-objects-are-available-in-my.md)
- [条件付きコンパイル](../../programming-guide/program-structure/conditional-compilation.md)
- [-define (Visual Basic)](../../reference/command-line-compiler/define.md)
- [My.Forms オブジェクト](../../language-reference/objects/my-forms-object.md)
- [My.Request オブジェクト](../../language-reference/objects/my-request-object.md)
- [My.Response オブジェクト](../../language-reference/objects/my-response-object.md)
- [My.WebServices オブジェクト](../../language-reference/objects/my-webservices-object.md)
