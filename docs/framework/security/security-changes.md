---
title: .NET Framework におけるセキュリティの変更点
ms.date: 03/30/2017
helpviewer_keywords:
- Allow Partially Trusted Callers attribute
- .NET Framework 4, security changes
- .NET Framework security
- security-transparent code
- security-critical code
- code access security, changes
ms.assetid: 5e87881c-9c13-4b52-8ad1-e34bb46e8aaa
author: mairaw
ms.author: mairaw
ms.openlocfilehash: af2869e5ca3b41778c094b7a78a9493e74868811
ms.sourcegitcommit: 81ad1f09b93f3b3e6706a7f2e4ddf50ef229ea3d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2019
ms.locfileid: "74204506"
---
# <a name="security-changes-in-the-net-framework"></a>.NET Framework におけるセキュリティの変更点

.NET Framework 4.5 でのセキュリティの最も重要な変更点は、厳密な名前付けです。 これらの変更の詳細については、「 [Enhanced Strong Naming](../../standard/assembly/enhanced-strong-naming.md) 」を参照してください。  
  
.NET Framework は、マネージド アプリケーションに 2 階層のセキュリティ モデルを提供します。 Windows 8.x ストアアプリは、リソースへのアクセスを制限する Windows セキュリティコンテナーで実行されます。 そのコンテナー内では、マネージド アプリケーションは完全に信頼された状態で実行します。 コード アクセス セキュリティの (CAS) の観点からは、権限を昇格するために開発者が実行できる操作はありません。 Windows で与えられる権限の詳細については、Windows デベロッパー センターの「 [App capability declarations (Windows Store apps)](https://go.microsoft.com/fwlink/?LinkId=230436) 」 (アプリの機能宣言 (Windows ストア アプリ)) を参照してください。 Windows 8.x ストアアプリの作成の詳細については、「」[または「Visual Basic をC#使用した初めての windows ストアアプリの作成](https://go.microsoft.com/fwlink/?LinkId=230461)」を参照してください。
