---
title: '方法: .NET Framework 3.5 がインストールされているかどうかを確認する'
ms.date: 03/30/2017
helpviewer_keywords:
- verifying whether.NET Framework 3.5 is installed [WPF]
- detecting .NET Framework 3.5 installation [WPF]
- detecting whether.NET Framework 3.5 is installed [WPF]
- determining whether.NET Framework 3.5 is installed [WPF]
ms.assetid: 8556a9d2-1eb8-48ef-919c-5baf22a2a9a2
ms.openlocfilehash: 18e5c819eb4deb62208280816d11dce0940d134d
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053428"
---
# <a name="how-to-detect-whether-the-net-framework-35-is-installed"></a>方法: .NET Framework 3.5 がインストールされているかどうかを確認する
管理者は、.NET Framework 3.5 を対象とするシステムに Windows Presentation Foundation (WPF) アプリケーションを配置する前に、まず、.NET Framework 3.5 ランタイムが存在することを確認する必要があります。 このトピックでは、.NET Framework 3.5 がシステムに存在するかどうかを確認するために管理者が使用できる HTML/JavaScript で記述されたスクリプトを提供します。  
  
> [!NOTE]
> .NET Framework のインストール、配置、検出について詳しくは、「[開発者向けの .NET Framework のインストール](../../install/guide-for-developers.md)」をご覧ください。  
  
## <a name="example"></a>例  
 .NET Framework 3.5 がインストールされている場合、MSI によって UserAgent 文字列に ".NET CLR" とバージョン番号が追加されます。 次の例は、単純な HTML ページに埋め込まれたスクリプトを示しています。 このスクリプトでは、UserAgent 文字列を検索し .NET Framework 3.5 がインストールされているかどうかを判断し、検索結果に状態メッセージを表示します。  
  
> [!NOTE]
> このスクリプトは、Internet Explorer 向けに設計されています。 他のブラウザーでは、.NET CLR の情報が UserAgent 文字列に含まれていないことがあります。  
  
```html  
<HTML>  
  <HEAD>  
    <TITLE>Test for the .NET Framework 3.5</TITLE>  
    <META HTTP-EQUIV="Content-Type" CONTENT="text/html; charset=utf-8" />  
    <SCRIPT LANGUAGE="JavaScript">  
    <!--  
    var dotNETRuntimeVersion = "3.5.0.0";  
  
    function window::onload()  
    {  
      if (HasRuntimeVersion(dotNETRuntimeVersion))  
      {  
        result.innerText =   
          "This machine has the correct version of the .NET Framework 3.5."  
      }   
      else  
      {  
        result.innerText =   
          "This machine does not have the correct version of the .NET Framework 3.5." +  
          " The required version is v" + dotNETRuntimeVersion + ".";  
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
  
 `This machine has the correct version of the .NET Framework 3.5.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; .NET CLR 3.5.20726; MS-RTC LM 8).`  
  
 それ以外の場合は、次の種類の状態メッセージが表示されます。  
  
 `This machine does not have the correct version of the .NET Framework 3.5. The required version is v3.5.0.0.`  
  
 `This machine's userAgent string is: Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.0; SLCC1; .NET CLR 2.0.50727; .NET CLR 1.1.4322; InfoPath.2; .NET CLR 3.0.590; MS-RTC LM 8).`  
  
## <a name="see-also"></a>関連項目

- [.NET Framework 3.0 がインストールされているかどうかを確認する](how-to-detect-whether-the-net-framework-3-0-is-installed.md)
