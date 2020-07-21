---
title: -win32manifest
ms.date: 03/13/2018
helpviewer_keywords:
- /win32manifest compiler option [Visual Basic]
- win32manifest compiler option [Visual Basic]
- -win32manifest compiler option [Visual Basic]
ms.assetid: 9e3191b4-90db-41c8-966a-28036fd20005
ms.openlocfilehash: 6f77649365f8ca7b163cd55854aa9960d88f2984
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414260"
---
# <a name="-win32manifest-visual-basic"></a>-win32manifest (Visual Basic)
プロジェクトのポータブル実行可能 (PE) ファイルに埋め込まれる、ユーザー定義の Win32 アプリケーション マニフェスト ファイルを識別します。  
  
## <a name="syntax"></a>構文  
  
```console  
-win32manifest: fileName  
```  
  
## <a name="arguments"></a>引数  
  
|用語|定義|  
|---|---|  
|`fileName`|カスタム マニフェスト ファイルのパス。|  
  
## <a name="remarks"></a>Remarks  
 既定では、asInvoker の要求実行レベルを指定するアプリケーション マニフェストが、Visual Basic コンパイラによって埋め込まれます。 マニフェストは、実行可能ファイルがビルドされたのと同じフォルダー (Visual Studio を使用している場合、通常は bin\Debug または bin\Release フォルダー) に作成されます。 カスタム マニフェストを指定する (たとえば、highestAvailable または requireAdministrator の要求実行レベルを指定する) 場合は、このオプションを使用してファイルの名前を指定します。  
  
> [!NOTE]
> このオプションと [-win32resource](win32resource.md) オプションは、相互に排他的です。 同じコマンド ラインで両方のオプションを使おうすると、ビルド エラーが発生します。  
  
 アプリケーション マニフェストを持たないアプリケーションは、要求実行レベルを指定した場合、Windows Vista のユーザー アカウント制御機能によって、ファイルまたはレジストリの仮想化の対象となります。 仮想化について詳しくは、「[Windows Vista の ClickOnce 配置](/visualstudio/deployment/clickonce-deployment-on-windows-vista)」を参照してください。  
  
 次の条件のいずれかに該当する場合、アプリケーションは仮想化の対象となります。  
  
1. `-nowin32manifest` オプションを使用していて、後のビルド手順でマニフェストを提供していないか、`-win32resource` オプションを使用して Windows リソース (.res) ファイルの一部としていない。  
  
2. 要求実行レベルが指定されていないカスタム マニフェストを提供している。  
  
 Visual Studio は、既定の .manifest ファイルを作成し、それを実行可能ファイルと一緒にデバッグ ディレクトリとリリース ディレクトリに保存します。 既定の app.manifest ファイルは、プロジェクト デザイナーの **[アプリケーション]** タブにある **[UAC 設定の表示]** をクリックして表示または編集することができます。 詳細については、「[[アプリケーション] ページ (プロジェクト デザイナー) (Visual Basic)](/visualstudio/ide/reference/application-page-project-designer-visual-basic)」を参照してください。  
  
 アプリケーション マニフェストは、カスタムのビルド後手順として提供するか、`-nowin32manifest` オプションを使用して、Win32 リソース ファイルの一部として提供できます。 アプリケーションを Windows Vista でファイルまたはレジストリの仮想化の対象にする場合は、これと同じオプションを使用します。 これにより、コンパイラで PE ファイル内に既定のマニフェストが作成されて埋め込まれなくなります。  
  
## <a name="example"></a>例  
 次の例は、Visual Basic コンパイラによって PE に挿入される既定のマニフェストを示しています。  
  
> [!NOTE]
> コンパイラによって、標準のアプリケーション名 MyApplication.app がマニフェスト XML に挿入されます。 これは、アプリケーションを Windows Server 2003 Service Pack 3 で実行できるようにするための回避策です。  
  
```xml  
<?xml version="1.0" encoding="utf-8" standalone="yes"?>  
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">  
  <assemblyIdentity version="1.0.0.0" name="MyApplication.app"/>  
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v2">  
    <security>  
      <requestedPrivileges xmlns="urn:schemas-microsoft-com:asm.v3">  
        <requestedExecutionLevel level="asInvoker"/>  
      </requestedPrivileges>  
    </security>  
  </trustInfo>  
</assembly>  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](index.md)
- [-nowin32manifest (Visual Basic)](nowin32manifest.md)
