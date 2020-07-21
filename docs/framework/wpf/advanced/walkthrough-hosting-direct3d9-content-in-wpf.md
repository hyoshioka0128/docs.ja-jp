---
title: WPF で Direct3D9 コンテンツをホストする
titleSuffix: ''
ms.date: 03/30/2017
helpviewer_keywords:
- Direct3D9 [WPF interoperability], hosting Direct3D9 content
- WPF [WPF], hosting Direct3D9 content
ms.assetid: 60983736-0ab5-42cc-8b16-e9fbde261a43
ms.openlocfilehash: e65b0c59268b44abed289e54181bf0bda9355664
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76742608"
---
# <a name="walkthrough-hosting-direct3d9-content-in-wpf"></a>チュートリアル: WPF での Direct3D9 コンテンツのホスト

このチュートリアルでは、Windows Presentation Foundation (WPF) アプリケーションで Direct3D9 コンテンツをホストする方法について説明します。

このチュートリアルでは次のタスクを実行します。

- Direct3D9 コンテンツをホストする WPF プロジェクトを作成します。

- Direct3D9 コンテンツをインポートします。

- <xref:System.Windows.Interop.D3DImage> クラスを使用して Direct3D9 コンテンツを表示します。

 完了すると、WPF アプリケーションで Direct3D9 コンテンツをホストする方法がわかります。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio

- DirectX SDK 9 以降。

- WPF 互換形式の Direct3D9 コンテンツを含む DLL。 詳細については、「[WPF と Direct3D9 の相互運用性](wpf-and-direct3d9-interoperation.md)」と「[チュートリアル: WPF でホストするための Direct3D9 コンテンツの作成](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)」を参照してください。

## <a name="creating-the-wpf-project"></a>WPF プロジェクトの作成

最初の手順は、WPF アプリケーションのプロジェクトを作成することです。

### <a name="to-create-the-wpf-project"></a>WPF プロジェクトを作成するには

Visual C# で `D3DHost` という名前の新しい WPF アプリケーション プロジェクトを作成します。 詳細については、「[チュートリアル:初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)」を参照してください。

MainWindow.xaml が WPF デザイナーで開きます。

## <a name="importing-the-direct3d9-content"></a>Direct3D9 コンテンツのインポート

`DllImport` 属性を使用して、アンマネージド DLL から Direct3D9 コンテンツをインポートします。

### <a name="to-import-direct3d9-content"></a>Direct3D9 コンテンツをインポートするには

1. コード エディターで MainWindow.xaml.cs を開きます。

2. 自動生成されたコードを次のコードに置き換えます。

    [!code-csharp[System.Windows.Interop.D3DImage#1](~/samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml.cs#1)]

## <a name="hosting-the-direct3d9-content"></a>Direct3D9 コンテンツのホスト

最後に、<xref:System.Windows.Interop.D3DImage> クラスを使用して Direct3D9 コンテンツをホストします。

### <a name="to-host-the-direct3d9-content"></a>Direct3D9 コンテンツをホストするには

1. MainWindow.xaml で、自動生成された XAML を次の XAML に置き換えます。

    [!code-xaml[System.Windows.Interop.D3DImage#10](~/samples/snippets/csharp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/CS/window1.xaml#10)]

2. プロジェクトをビルドします。

3. Direct3D9 コンテンツを含む DLL を bin/Debug フォルダーにコピーします。

4. F5 キーを押してプロジェクトを実行します。

    Direct3D9 コンテンツが WPF アプリケーション内に表示されます。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 および WPF の相互運用性のパフォーマンスに関する考慮事項](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
