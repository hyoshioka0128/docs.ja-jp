---
title: '方法: DEVPATH を使用してアセンブリを指定する'
description: XML コンピューター構成ファイルと DEVPATH 環境変数を使用して、共有アセンブリが .NET の多くのアプリケーションで正しく動作することをテストします。
ms.date: 03/30/2017
helpviewer_keywords:
- DEVPATH
- .NET Framework application configuration, assemblies
- application configuration files, specifying assembly's location
- app.config files, assembly locations
- locating assemblies
- assemblies [.NET Framework], location
ms.assetid: 44d2eadf-7eec-443c-a2ac-d601fd919e17
ms.openlocfilehash: 50b61eedddabd660b1834565a61738f460ae9ff9
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85105372"
---
# <a name="how-to-locate-assemblies-by-using-devpath"></a>方法: DEVPATH を使用してアセンブリを指定する
開発者は、ビルドしている共有アセンブリが複数のアプリケーションで正しく動作することを確認したい場合があります。 開発サイクル中にアセンブリをグローバルアセンブリキャッシュに継続的に配置するのではなく、開発者はアセンブリのビルド出力ディレクトリを指す DEVPATH 環境変数を作成できます。  
  
 たとえば、MySharedAssembly という名前の共有アセンブリを作成し、出力ディレクトリを C:\MySharedAssembly\Debug. にするとします。 C:\MySharedAssembly\Debug を DEVPATH 変数に配置できます。 次 [\<developmentMode>](./file-schema/runtime/developmentmode-element.md) に、マシン構成ファイルで要素を指定する必要があります。 この要素は、アセンブリを検索するために DEVPATH を使用するように共通言語ランタイムに指示します。  
  
 共有アセンブリは、ランタイムによって検出可能である必要があります。  アセンブリ参照を解決するためのプライベートディレクトリを指定するには、「[アセンブリの場所の指定](specify-assembly-location.md)」で説明されているように、構成ファイル内の[ \<codeBase> 要素](./file-schema/runtime/codebase-element.md)または[ \<probing> 要素](./file-schema/runtime/probing-element.md)を使用します。  また、アセンブリをアプリケーションディレクトリのサブディレクトリに配置することもできます。 詳細については、「[ランタイムがアセンブリを検索する方法](../deployment/how-the-runtime-locates-assemblies.md)」を参照してください。  
  
> [!NOTE]
> これは高度な機能であり、開発のみを目的としています。  
  
 次の例は、DEVPATH 環境変数によって指定されたディレクトリ内のアセンブリをランタイムが検索する方法を示しています。  
  
## <a name="example"></a>例  
  
```xml  
<configuration>  
  <runtime>  
    <developmentMode developerInstallation="true"/>  
  </runtime>  
</configuration>  
```  
  
 この設定の既定値は false です。  
  
> [!NOTE]
> この設定は、開発時にのみ使用してください。 ランタイムは、DEVPATH で見つかった厳密な名前のアセンブリのバージョンをチェックしません。 単純に、最初に見つかったアセンブリを使用します。  
  
## <a name="see-also"></a>関連項目

- [構成ファイルを使用してアプリを構成する方法](index.md)
