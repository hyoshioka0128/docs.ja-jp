---
title: アセンブリの配置
description: ディレクトリ内 (グローバル アセンブリ キャッシュ内、またはアプリケーションのディレクトリ内またはサブディレクトリ内) の .NET アセンブリの配置に関するガイドラインについて確認します。
ms.date: 03/30/2017
helpviewer_keywords:
- <codeBase> element
- locating assemblies
- assemblies [.NET Framework], placement
- assemblies [.NET Framework], location
ms.assetid: ff8d48bc-f606-484f-9fe1-d0af264269fb
ms.openlocfilehash: 3106f6f01229057725cbc2e8e689a4e2247f95e6
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85104964"
---
# <a name="assembly-placement"></a>アセンブリの配置
多くの .NET Framework アプリケーションの場合、アプリケーションを構成するアセンブリは、そのアプリケーションのディレクトリ、アプリケーション ディレクトリのサブディレクトリ、またはグローバル アセンブリ キャッシュ (アセンブリが共有されている場合) に配置します。 構成ファイルの [\<codeBase> 要素](../configure-apps/file-schema/runtime/codebase-element.md)を使用すると、共通言語ランタイムがアセンブリを検索する場所をオーバーライドできます。 アセンブリが厳密な名前を持たない場合、[\<codeBase> 要素](../configure-apps/file-schema/runtime/codebase-element.md)を使用して指定できる場所は、そのアプリケーションのディレクトリまたはサブディレクトリに制限されます。 アセンブリが厳密な名前を持つ場合は、[\<codeBase> 要素](../configure-apps/file-schema/runtime/codebase-element.md)を使用してコンピューターまたはネットワーク上の任意の場所を指定できます。  
  
 また、アンマネージ コード アプリケーションや COM 相互運用アプリケーションで使用するアセンブリを検索する場所についても似たような規則が適用されます。アセンブリを複数のアプリケーションで共有する場合、そのアセンブリの検索場所はグローバル アセンブリ キャッシュになります。 アンマネージ コードで使用するアセンブリは、型ライブラリとしてエクスポートし、登録する必要があります。 COM 相互運用で使用するアセンブリは、カタログに登録する必要がありますが、場合によっては、この登録が自動的に行われることもあります。  
  
## <a name="see-also"></a>関連項目

- [ランタイムがアセンブリを検索する方法](../deployment/how-the-runtime-locates-assemblies.md)
- [アプリの構成](../configure-apps/index.md)
- [アンマネージ コードとの相互運用](../interop/index.md)
- [.NET のアセンブリ](index.md)
