---
title: '方法: .NET Framework 3.0 がインストールされているかどうかの確認'
ms.date: 03/30/2017
helpviewer_keywords:
- WinFX Runtime user-agent string
- presence of WPT [WPF], detecting
- detecting WPF presence [WPF]
ms.assetid: 7f71d652-1749-4379-945a-aa2e3994cb43
ms.openlocfilehash: 60868661df442849db3f5421f8ea33f790fd83fc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187363"
---
# <a name="how-to-detect-whether-the-net-framework-30-is-installed"></a>方法: .NET Framework 3.0 がインストールされているかどうかの確認
管理者が Microsoft .NET Framework アプリケーションをシステムに配置するには、まず、.NET Framework ランタイムが存在することを確認する必要があります。 このトピックでは、.NET Framework がシステムに存在するかどうかを確認するために管理者が使用できる HTML/JavaScript で記述されたスクリプトを提供します。  
  
> [!NOTE]
> Microsoft .NET Framework のインストール、配置、および検出の詳細については、「[Microsoft .NET Framework バージョン 3.0の配置](https://docs.microsoft.com/previous-versions/dotnet/articles/aa480198(v=msdn.10))」の説明を参照してください。  
  
<a name="content_expiration"></a>
## <a name="detect-the-net-clr-user-agent-string"></a>".NET CLR" ユーザー エージェント文字列の検出  
 .NET Framework がインストールされている場合、MSI によって UserAgent 文字列に ".NET CLR" とバージョン番号が追加されます。 次の例は、単純な HTML ページに埋め込まれたスクリプトを示しています。 このスクリプトでは、UserAgent 文字列を検索し .NET Framework がインストールされているかどうかを判断し、検索結果に状態メッセージを表示します。  
  
```html  
<HTML>  
  <HEAD>  
    <TITLE>Test for the .NET Framework 3.0</TITLE>  
    <META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8" />  
    <SCRIPT LANGUAGE="JavaScript">  
    <!--  
    var dotNETRuntimeVersion = "3.0.04425.00";  
  
    function window::onload()  
    {  
      if (HasRuntimeVersion(dotNETRuntimeVersion))  
      {  
        result.innerText =   
          "This machine has the correct version of the .NET Framework 3.0: "   
          + dotNETRuntimeVersion  
      }   
      else  
      {  
        result.innerText =   
          "This machine does not have the correct version of the .NET Framework 3.0."  
      }  
      result.innerText += "\n\nThis machine's userAgent string is: " +   
        navigator.userAgent + ".";  
    }  
  
    //  
    // Retrieve the version from the user agent string and   
    // compare with the specified version.  
    //  
    function HasRuntimeVersion(versionToCheck)  
    {  
      var userAgentString =   
        navigator.userAgent.match(/.NET CLR [0-9.]+/g);  
  
      if (userAgentString != null)  
      {  
        var i;  
  
        for (i = 0; i < userAgentString.length; ++i)  
        {  
          if (CompareVersions(GetVersion(versionToCheck),   
            GetVersion(userAgentString[i])) <= 0)  
            return true;  
        }  
      }  
  
      return false;  
    }  
  
    //  
    // Extract the numeric part of the version string.  
    //  
    function GetVersion(versionString)  
    {  
      var numericString =   
        versionString.match(/([0-9]+)\.([0-9]+)\.([0-9]+)/i);  
      return numericString.slice(1);  
    }  
  
    //  
    // Compare the 2 version strings by converting them to numeric format.  
    //  
    function CompareVersions(version1, version2)  
    {  
      for (i = 0; i < version1.length; ++i)  
      {  
        var number1 = new Number(version1[i]);  
        var number2 = new Number(version2[i]);  
  
        if (number1 < number2)  
          return -1;  
  
        if (number1 > number2)  
          return 1;  
      }  
  
      return 0;  
    }  
  
    -->  
    </SCRIPT>  
  </HEAD>  
  
  <BODY>  
    <div id="result" />  
  </BODY>  
</HTML>  
```  
  
 ".NET CLR" バージョンの検索に成功すると、次の種類の状態メッセージが表示されます。  
  
 `This machine has the correct version of the .NET Framework 3.0: 3.0.04425.00`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; .NET CLR 1.1.4322; InfoPath.1; .NET CLR 2.0.50727; .NET CLR 3.0.04425.00).`  
  
 それ以外の場合は、次の種類の状態メッセージが表示されます:  
  
 `This machine does not have correct version of the .NET Framework 3.0.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1; .NET CLR 1.1.4322; InfoPath.1; .NET CLR 2.0.50727).`
