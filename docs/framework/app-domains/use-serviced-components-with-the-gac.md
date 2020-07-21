---
title: サービス コンポーネントとグローバル アセンブリ キャッシュの使用
description: .NET のグローバル アセンブリ キャッシュで、サービス コンポーネント (マネージド コード COM+ コンポーネント) を使用します。 CLR および COM+ サービスで GAC 以外のコンポーネントを処理できるかどうかを確認します。
ms.date: 03/30/2017
helpviewer_keywords:
- assemblies [.NET Framework], global assembly cache
- GAC (global assembly cache), serviced components
- serviced components, global assembly cache
- global assembly cache, serviced components
ms.assetid: 3423e5d9-234c-4571-8161-e35f6d130128
ms.openlocfilehash: 6b7371865b7b1cedda0ee03b2cc28c74b5c3da0b
ms.sourcegitcommit: 1c37a894c923bea021a3cc38ce7cba946357bbe1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85104471"
---
# <a name="using-serviced-components-with-the-global-assembly-cache"></a>サービス コンポーネントとグローバル アセンブリ キャッシュの使用
サービス コンポーネント (マネージド コード COM+ コンポーネント) はグローバル アセンブリ キャッシュに配置する必要があります。 共通言語ランタイムと COM+ サービスは、シナリオによって、グローバル アセンブリ キャッシュに配置されていないサービス コンポーネントを処理できる場合と、処理できない場合があります。 これについて、次のシナリオで説明します。  
  
- COM+ サーバー アプリケーションのサービス コンポーネントの場合、コンポーネントを含むアセンブリがグローバル アセンブリ キャッシュに配置されている必要があります。これは、Dllhost.exe がサービス コンポーネントを格納するのと同じディレクトリで実行されないためです。  
  
- COM+ ライブラリ アプリケーションに含まれるサービス コンポーネントの場合、ランタイムと COM+ サービスは、現在のディレクトリで検索することにより、コンポーネントを含むアセンブリへの参照を解決できます。 この場合、アセンブリがグローバル アセンブリ キャッシュ内に配置されている必要はありません。  
  
- ASP.NET アプリケーションに含まれるサービス コンポーネントの場合、状況は異なります。 サービス コンポーネントを含むアセンブリをアプリケーション ベースの bin ディレクトリに配置し、オンデマンド登録を使用すると、アセンブリはダウンロード キャッシュにシャドウとしてコピーされます。これは、ASP.NET がランタイムのシャドウ機能を利用するためです。  
  
## <a name="see-also"></a>関連項目

- [アセンブリとグローバル アセンブリ キャッシュの使用](working-with-assemblies-and-the-gac.md)
- [Gacutil.exe (グローバル アセンブリ キャッシュ ツール)](../tools/gacutil-exe-gac-tool.md)
