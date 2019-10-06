---
title: Visual Studio で AJAX 対応 WCF サービスと ASP.NET クライアントを作成する
ms.date: 08/17/2018
ms.assetid: 95012df8-2a66-420d-944a-8afab261013e
ms.openlocfilehash: a6d6e87de6200a5cb9bba566d595066673cdf9cf
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834785"
---
# <a name="how-to-create-an-ajax-enabled-wcf-service-and-an-aspnet-client-that-accesses-the-service"></a>方法: AJAX 対応 WCF サービスと、サービスにアクセスする ASP.NET クライアントを作成する

このトピックでは、Visual Studio を使用して、AJAX 対応の Windows Communication Foundation (WCF) サービスと、サービスにアクセスする ASP.NET クライアントを作成する方法について説明します。

## <a name="create-an-aspnet-web-app"></a>ASP.NET Web アプリを作成する

1. Visual Studio を開きます。

1. **[ファイル]** メニューの [**新しい** > **プロジェクト**] をクリックします。

1. **[新しいプロジェクト]** ダイアログで、[**インストールされ** > た > **ビジュアルC#**  **web** ] カテゴリを展開し、 **[ASP.NET Web Application (.NET Framework)]** を選択します。

1. プロジェクトに**SandwichServices**という名前を指定し、[ **OK]** をクリックします。

1. **[New ASP.NET Web Application]** ダイアログボックスで **[Empty]** を選択し、 **[OK]** を選択します。

   ![ASP.NET Visual Studio の [web アプリの種類] ダイアログボックス](./media/create-an-ajax-wcf-asp-net-client/new-asp-net-web-app-type.png)

## <a name="add-a-web-form"></a>Web フォームを追加する

1. **ソリューションエクスプローラー**で SandwichServices プロジェクトを右クリックし、[**新しい項目**の**追加** > ] を選択します。

1. **[新しい項目の追加]** ダイアログで、[**インストールされ** > た**ビジュアルC#**   >  **web** ] カテゴリを展開し、 **[Web フォーム]** テンプレートを選択します。

1. 既定の名前 (**WebForm1**) をそのまま使用し、 **[追加]** を選択します。

   **ソース**ビューで*WebForm1*が開きます。

1. **\<本文 >** タグ内に次のマークアップを追加します。

   ```html
   <input type="button" value="Price of 3 sandwiches" onclick="Calculate()"/>
   <br />
   <span id="additionResult"></span>
   ```

## <a name="create-an-ajax-enabled-wcf-service"></a>AJAX 対応 WCF サービスを作成する

1. **ソリューションエクスプローラー**で SandwichServices プロジェクトを右クリックし、[**新しい項目**の**追加** > ] を選択します。

1. **[新しい項目の追加]** ダイアログで、[**インストールされ** > た**ビジュアルC#**   > Web] カテゴリを展開し、 **[WCF サービス (AJAX 対応)]** テンプレートを選択します。

   ![Visual Studio での WCF サービス (AJAX 対応) 項目テンプレート](./media/create-an-ajax-wcf-asp-net-client/add-wcf-service.png)

1. サービスにサービスの**名前を指定**し、 **[追加]** を選択します。

   *CostService.svc.cs*がエディターで開きます。

1. サービスに操作を実装します。 サンドイッチの数量のコストを計算するには、次のメソッドを cost Service クラスに追加します。

    ```csharp
    [OperationContract]
    public double CostOfSandwiches(int quantity)
    {
        return 1.25 * quantity;
    }
    ```

## <a name="configure-the-client-to-access-the-service"></a>サービスにアクセスするようにクライアントを構成する

1. *WebForm1*ファイルを開き、 **[デザイン]** ビューを選択します。

2. **[表示]** メニューの **[ツールボックス]** をクリックします。

3. **[AJAX Extensions]** ノードを展開し、 **ScriptManager**をフォームにドラッグアンドドロップします。

4. **ソース**ビューに戻り、  **\<ScriptManager >** タグの間に次のコードを追加して、WCF サービスへのパスを指定します。

    ```xml
    <Services>
       <asp:ServiceReference Path="~/CostService.svc" />
    </Services>
    ```

5. Javascript 関数`Calculate()`のコードを追加します。 次のコードを web フォームの**head**セクションに配置します。

    ```html
    <script type="text/javascript">

        function Calculate() {
            CostService.CostOfSandwiches(3, onSuccess);
        }

        function onSuccess(result) {
            var myres = $get("additionResult");
            myres.innerHTML = result;
        }

    </script>
    ```

   このコードは、3つのサンドイッチの価格を計算するために、コストサービスのメソッドを呼び出し、 **additionResult**というスパンに結果を表示します。

## <a name="run-the-program"></a>プログラムを実行する

*WebForm1*にフォーカスがあることを確認し、 **[開始]** ボタンをクリックして web クライアントを起動します。 ボタンには緑色の三角形が表示され、 **IIS Express (Microsoft Edge)** のようなものが表示されます。 または、 <kbd>F5</kbd>キーを押します。 **[Price-3 サンドイッチ]** ボタンをクリックして、予想される出力 "3.75" を生成します。

## <a name="example"></a>例

*CostService.svc.cs*ファイルの完全なコードを次に示します。

```csharp
using System.ServiceModel;
using System.ServiceModel.Activation;

namespace SandwichServices
{
    [ServiceContract(Namespace = "")]
    [AspNetCompatibilityRequirements(RequirementsMode = AspNetCompatibilityRequirementsMode.Allowed)]
    public class CostService
    {
        [OperationContract]
        public double CostOfSandwiches(int quantity)
        {
            return 1.25 * quantity;
        }
    }
}
```

次に、 *WebForm1*ページの完全な内容を示します。

```aspx-csharp
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm1.aspx.cs" Inherits="SandwichServices.WebForm1" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
    <script type="text/javascript">

        function Calculate() {
            CostService.CostOfSandwiches(3, onSuccess);
        }

        function onSuccess(result) {
            var myres = $get("additionResult");
            myres.innerHTML = result;
        }

    </script>
</head>
<body>
    <form id="form1" runat="server">
        <div>
        </div>
        <asp:ScriptManager ID="ScriptManager1" runat="server">
            <Services>
                <asp:ServiceReference Path="~/CostService.svc" />
            </Services>
        </asp:ScriptManager>

        <input type="button" value="Price of 3 sandwiches" onclick="Calculate()" />
        <br />
        <span id="additionResult"></span>
    </form>
</body>
</html>
```
