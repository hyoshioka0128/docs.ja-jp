---
title: '方法: アプリケーション セッション全体でアプリケーション スコープのプロパティを永続化および復元する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application-scope properties [WPF], persisting
- persisting application-scope properties [WPF]
- properties [WPF], persisting
- restoring application-scope properties [WPF]
- properties [WPF], restoring
- application-scope properties [WPF], restoring
ms.assetid: 55d5904a-f444-4eb5-abd3-6bc74dd14226
ms.openlocfilehash: d9c2dda2745e7528902b6b1c4f46d17264d1a8d8
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2019
ms.locfileid: "69666724"
---
# <a name="how-to-persist-and-restore-application-scope-properties-across-application-sessions"></a>方法: アプリケーション セッション全体でアプリケーション スコープのプロパティを永続化および復元する
この例では、アプリケーションがシャットダウンされるときにアプリケーション スコープのプロパティを永続化する方法と、次にアプリケーションが起動されるときにアプリケーション スコープのプロパティを復元する方法を示します。  
  
## <a name="example"></a>例  
 アプリケーションで、アプリケーション スコープのプロパティを分離ストレージに永続化し、そこから復元します。 分離ストレージは、ファイル アクセス許可のないアプリケーションでも安全に使用できる、保護されたストレージ領域です。  最初の例の強調表示された行で示されているように、*App.xaml* ファイルでは、<xref:System.Windows.Application.Startup?displayProperty=nameWithType> イベントのハンドラーとして `App_Startup` メソッドが定義されており、`App_Exit` イベントのハンドラーとして <xref:System.Windows.Application.Exit?displayProperty=nameWithType> メソッドが定義されています。 2 番目の例の *App.xaml.cs* ファイルと *App.xaml.vb* ファイルの強調表示されているコードの部分では、アプリケーション スコープのプロパティを復元する `App_Startup` メソッドと、アプリケーション スコープのプロパティを保存する `App_Exit` メソッドが示されています。

 [!code-xaml[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml?highlight=1-7)]
  
 [!code-csharp[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml.cs?highlight=17-55)]
 [!code-vb[HOWTOApplicationModelSnippets#PersistRestoreAppScopePropertiesCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/visualbasic/application.xaml.vb?highlight=14-45)]
