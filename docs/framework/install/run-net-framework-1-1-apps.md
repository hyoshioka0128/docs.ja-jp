---
title: Windows 8、Windows 8.1、または Windows 10 での .NET Framework 1.1 アプリの実行
description: Windows オペレーティング システムの多くのバージョンではサポートされなくなった、.NET Framework 1.1 を必要とするアプリに対応する方法について説明します。
ms.date: 05/26/2017
helpviewer_keywords:
- Windows 8, running .NET Framework 1.1 apps
- .NET Framework 1.1, running on Windows 8
ms.assetid: fb14e195-fea5-4561-b9a8-60a67283edb9
ms.openlocfilehash: 6d1cb2f9251bba96d0a378bf4dbab9f7da267037
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111791"
---
# <a name="run-net-framework-11-apps-on-windows-8-windows-81-or-windows-10"></a>Windows 8、Windows 8.1、または Windows 10 での .NET Framework 1.1 アプリの実行

.NET Framework 1.1 は、Windows 8、Windows 8.1、Windows Server 2012、Windows Server 2012 R2、または Windows 10 の各オペレーティング システムではサポートされていません。 場合によっては、アプリを実行するために .NET Framework 1.1 が必要になります。 このような場合は、.NET Framework 3.5 SP1 以降のバージョンで実行するようにアプリケーションをアップグレードするように、独立系ソフトウェア ベンダー (ISV) 問い合わせてください。 詳細については、[.NET Framework 1.1 からの移行](../migration-guide/migrating-from-the-net-framework-1-1.md)に関する記事をご覧ください。

## <a name="install-net-framework-11-from-a-cd-or-download-center"></a>CD またはダウンロード センターから .NET Framework 1.1 をインストールする

CD またはダウンロード センターから、Windows 8、Windows 8.1、Windows Server 2012、Windows Server 2012 R2、または Windows 10 に .NET Framework 1.1 を手動でインストールすることはできません。 その機能はサポートされなくなりました。 パッケージをインストールしようとすると、「このバージョンの .NET Framework は以前にインストールしたバージョンと互換性がないため、セットアップを続行できません。」というエラー メッセージが表示されます。 この問題を解決するには、[.NET Framework 3.5 SP1](https://www.microsoft.com/download/details.aspx?id=22) をインストールしてください。 このバージョンには .NET Framework 2.0 (.NET Framework 1.1 の次のリリース) が含まれています。これは、Windows 8、Windows 8.1、および Windows 10 でサポートされています。 .NET Framework の新しいバージョンに自動的に更新されるかどうかを確認するために、常に最初にアプリケーションのインストールを試す必要があります。 更新されない場合は、アプリケーションの更新について ISV に問い合わせてください。

## <a name="see-also"></a>関連項目

- [.NET Framework 1.1 からの移行](../migration-guide/migrating-from-the-net-framework-1-1.md)
- [Windows 10、Windows 8.1、および Windows 8 への .NET Framework 3.5 のインストール](dotnet-35-windows-10.md)
